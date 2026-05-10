# API Contract Practice

## Scope
- Dokumen ini menyelesaikan bagian `practice` dari task `ARCH-15`.
- Fokusnya adalah generate random practice session dan submit answer sampai hasil grading serta progress impact siap dipakai UI.
- Dokumen ini diturunkan dari sequence diagram practice generation/answer evaluation, progress handoff, dan ERD `practice_sessions`, `practice_questions`, `practice_answers`.

## Source References
- Sequence random question generation dan grading: [random-question-generator-and-answer-evaluation.md](../sequence-diagram/random-question-generator-and-answer-evaluation.md)
- Sequence progress handoff: [update-progress-snapshot.md](../sequence-diagram/update-progress-snapshot.md)
- ERD learning activity: [learning-activity.md](../erd/learning-activity.md)

## Domain ID
- `06` untuk `practice`

## Design Goals
- Menjaga `practice` tetap menjadi owner untuk session generation, question storage, answer grading, dan session progress update.
- Membuat request generate tetap ringan, karena recommendation spec utama datang dari `personalization` dan `progress`.
- Menyertakan `progressImpact` pada response answer untuk mendukung feedback loop write-through.

## Endpoint Summary

| Method | Path | Purpose | Access Requirement |
| --- | --- | --- | --- |
| `POST` | `/api/v1/practice/sessions/generate` | Menghasilkan practice session acak untuk current user | Authenticated + onboarding completed |
| `POST` | `/api/v1/practice/sessions/{sessionId}/answer` | Menilai jawaban practice dan menjalankan progress handoff | Authenticated + onboarding completed |

## Authorization Rules
- Semua endpoint di dokumen ini membutuhkan session valid dan `APP_READY`.
- Bila session tidak valid, kembalikan `401`.
- Bila session valid tetapi onboarding belum selesai, kembalikan `403`.

## Endpoint Details

### `POST /api/v1/practice/sessions/generate`
Menghasilkan practice session acak berbasis recommendation spec user saat ini.

Request body:

```json
{
  "questionCount": 5
}
```

Behavior:
- `questionCount` opsional, default `5`.
- `practice` meminta recommendation spec dari `personalization`.
- `practice` memuat constraint katalog dari `syllabus`.
- AI dipakai untuk generate session payload terstruktur.
- Generator question untuk MVP hanya boleh menghasilkan `SLOT_FILL`, `SHORT_FREE_RESPONSE`, atau `ARRANGE_TOKEN`.
- `SLOT_FILL` selalu memiliki tepat empat opsi jawaban.
- Pada `SLOT_FILL`, prompt berupa kalimat bahasa Jepang dengan satu slot kosong, dan seluruh opsi jawaban juga dalam bahasa Jepang.
- `SHORT_FREE_RESPONSE` dikunci ke prompt bahasa Inggris dan jawaban bahasa Jepang.
- `SHORT_FREE_RESPONSE` mengandalkan input method yang menerima romaji lalu mentransform jawaban ke kana atau kanji sebelum submit final.
- `ARRANGE_TOKEN` meminta user menyusun token/kata menjadi jawaban akhir dan boleh dipakai untuk arah `EN_TO_JA` maupun `JA_TO_EN`.
- `practice` tidak lagi menghasilkan `MULTIPLE_CHOICE` karena pattern itu sudah dicakup oleh `flashcards`.
- Response mengembalikan session beserta daftar question yang siap dirender UI.

Success response:

```json
{
  "status": {
    "traceId": "uuid",
    "code": 120006000,
    "message": "Success!",
    "errorDetails": []
  },
  "data": {
    "id": "uuid",
    "status": "GENERATED",
    "difficultyBand": "STANDARD",
    "questionMix": {
      "WEAK": 0.6,
      "REINFORCEMENT": 0.3,
      "STRETCH": 0.1
    },
    "totalQuestions": 5,
    "answeredQuestionsCount": 0,
    "startedAt": "2026-04-04T10:00:00Z",
    "questions": [
      {
        "id": "uuid",
        "skillCode": "n5_particles_wa_ga_o",
        "questionType": "SLOT_FILL",
        "gradingStrategy": "DETERMINISTIC",
        "difficultyBand": "STANDARD",
        "promptText": "わたし___がくせいです。",
        "promptPayload": {
          "schemaVersion": 1,
          "promptLanguage": "JA",
          "optionLanguage": "JA",
          "slotCount": 1,
          "sentenceTemplate": "わたし___がくせいです。",
          "options": [
            { "id": "a", "label": "は" },
            { "id": "b", "label": "が" },
            { "id": "c", "label": "を" },
            { "id": "d", "label": "に" }
          ]
        },
        "sortOrder": 1
      }
    ]
  }
}
```

### `POST /api/v1/practice/sessions/{sessionId}/answer`
Menilai jawaban practice, menyimpan `practice_answer`, lalu mengirim structured learning event ke `progress`.

Path params:

| Name | Type | Required | Notes |
| --- | --- | --- | --- |
| `sessionId` | `string` | yes | ID practice session milik current user. |

Request body:

```json
{
  "questionId": "uuid",
  "userAnswer": {
    "selectedOptionId": "a"
  },
  "responseTimeMs": 4200
}
```

Behavior:
- Memuat question dan session context.
- Bentuk `userAnswer` mengikuti `questionType`:
  - `SLOT_FILL`: kirim `selectedOptionId`.
  - `ARRANGE_TOKEN`: kirim `arrangedTokenIds` sesuai urutan final.
  - `SHORT_FREE_RESPONSE`: kirim `rawInputRomaji`, `normalizedKana`, dan opsional `normalizedKanji` bila IME di client berhasil menghasilkan kandidat final.
- Jika `gradingStrategy = DETERMINISTIC`, grading dilakukan di module `practice`.
- Jika `gradingStrategy = AI`, `practice` memanggil AI provider untuk grading dan short feedback.
- Setelah answer tersimpan, `practice` menjalankan handoff ke `progress`.

Success response:

```json
{
  "status": {
    "traceId": "uuid",
    "code": 120006000,
    "message": "Success!",
    "errorDetails": []
  },
  "data": {
    "sessionId": "uuid",
    "questionId": "uuid",
    "answerId": "uuid",
    "isCorrect": true,
    "numericScore": 100,
    "feedbackText": "Correct particle choice.",
    "gradingSource": "RULE_ENGINE",
    "gradingMetadata": {
      "gradingStrategy": "DETERMINISTIC",
      "matchedAnswerKeys": ["selectedOptionId"],
      "accepted": true
    },
    "sessionProgress": {
      "answeredQuestionsCount": 1,
      "totalQuestions": 5,
      "isCompleted": false
    },
    "nextQuestionId": "uuid",
    "progressImpact": {
      "progressEventId": "uuid",
      "skillCode": "n5_particles_wa_ga_o",
      "masteryScore": 58.4,
      "masteryState": "DEVELOPING",
      "recommendedDifficultyBand": "STANDARD"
    }
  }
}
```

## Question Type Contract

### `SLOT_FILL`
- Prompt menampilkan kalimat dengan satu slot kosong.
- User memilih satu jawaban dari tepat empat opsi.
- Kalimat prompt dan seluruh opsi jawaban sama-sama dalam bahasa Jepang.
- `gradingStrategy` default: `DETERMINISTIC`.
- Bentuk minimum `userAnswer`:

```json
{
  "selectedOptionId": "a"
}
```

### `SHORT_FREE_RESPONSE`
- Prompt selalu berupa kalimat penuh dalam bahasa Inggris.
- User menjawab dalam bahasa Jepang melalui input field.
- Client input method menerima romaji lalu mentransform jawaban ke kana atau kanji sebelum final submit.
- Payload jawaban sebaiknya tetap menyertakan bentuk mentah romaji dan hasil normalisasi agar grading AI bisa diaudit.
- `gradingStrategy` default: `AI`.
- Bentuk minimum `userAnswer`:

```json
{
  "rawInputRomaji": "watashi wa gakusei desu",
  "normalizedKana": "わたしはがくせいです",
  "normalizedKanji": "私は学生です"
}
```

### `ARRANGE_TOKEN`
- Prompt meminta user menyusun token/kata menjadi jawaban akhir.
- Arah soal boleh `EN_TO_JA` atau `JA_TO_EN`.
- `gradingStrategy` default: `DETERMINISTIC`.
- Bentuk minimum `userAnswer`:

```json
{
  "arrangedTokenIds": ["t1", "t2", "t3", "t4"]
}
```

## Suggested Error Code Seeds

| HTTP Status | Application Code | Meaning |
| --- | --- | --- |
| `200` | `120006000` | Practice success |
| `401` | `140106001` | Session tidak ada atau tidak valid untuk practice API |
| `403` | `140306001` | Onboarding belum selesai untuk practice API |
| `404` | `140406001` | Practice session tidak ditemukan atau bukan milik user |
| `422` | `142206001` | Validation error generic |
| `422` | `142206002` | `questionId` tidak cocok dengan session aktif |
| `500` | `150006999` | Unhandled practice exception |

## OpenAPI Artifact
- Swagger/OpenAPI contract untuk area ini disimpan di `docs/api-contract/openapi.practice.yaml`.

## Notes For Follow-up Tasks
- Jika nanti session review atau retry mode ditambahkan, lebih aman memperluas request generate daripada mengubah shape response answer yang sudah dipakai UI.
- `gradingMetadata` yang dikembalikan API sebaiknya tetap ringkas; observability detail AI tetap berada di log internal.
