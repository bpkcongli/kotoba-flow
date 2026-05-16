# Tech Debt Register

## Purpose
- Dokumen ini menampung tech debt aktif yang sudah dikenali selama fase dokumentasi dan perancangan KotobaHub.
- Tujuannya agar perubahan requirement atau arsitektur yang belum sempat diselaraskan ke semua artefak tidak hilang sebagai asumsi lisan.

## Status Rules
- `OPEN`: debt sudah dikenali tetapi belum ditangani.
- `PLANNED`: debt sudah punya arah penyelesaian, tetapi belum dieksekusi.
- `DONE`: debt sudah diselesaikan dan item bisa dipindahkan ke bagian arsip bila register nanti berkembang.

## Active Items

### `TD-001` System Design Alignment For Lesson Explanation Paragraphs
- Status: `OPEN`
- Created at: `2026-05-16`
- Trigger:
  - ERD syllabus kini menambahkan tabel `lesson_content_blocks`.
  - API syllabus kini perlu menyediakan lesson detail yang membawa `contentBlocks`.
  - Seed schema syllabus kini perlu membawa `lesson.contentBlocks`.
- Affected artifacts:
  - [low-fidelity-wireframes-core-flows.md](./system-design/low-fidelity-wireframes-core-flows.md)
  - [high-fidelity-system-design.md](./system-design/high-fidelity-system-design.md)
- Debt summary:
  - Wireframe dan hi-fi saat ini belum secara eksplisit memodelkan surface lesson study yang menampilkan paragraf penjelasan materi berurutan.
  - Struktur screen `Syllabus` masih lebih menekankan `track -> unit -> lesson` overview dan CTA activity, belum menjelaskan bagaimana blok penjelasan lesson dibaca sebelum masuk atau saat berada di activity flow.
- Expected follow-up:
  - Tambahkan lesson study surface atau detail panel yang eksplisit pada low-fidelity.
  - Selaraskan high-fidelity agar hierarchy, scroll behavior, heading, dan treatment paragraph blocks konsisten dengan schema baru.
  - Validasi apakah lesson explanation muncul sebagai halaman lesson tersendiri, expandable panel di unit detail, atau pre-activity study step.
