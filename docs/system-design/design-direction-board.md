# KotobaHub Design Direction Board

## Status
- Dokumen ini menyelesaikan task `DS-02`.
- Dokumen ini menurunkan arah dari [brand-identity-brief.md](./brand-identity-brief.md) menjadi board kerja untuk visual system awal.
- Scope dokumen ini belum masuk ke high-fidelity screen. Fokusnya adalah tone, keyword, visual cues, dan personality produk belajar.

## Dependencies
- [brand-identity-brief.md](./brand-identity-brief.md)
- [mvp-plan.md](../mvp-plan.md)

## Figma Reference
- System design canvas untuk DS-02 dan DS-03 ada di Figma: https://www.figma.com/design/iCvRU1So1SOrAl58xFZurg/KotobaHub?node-id=0-1&p=f&t=ddPurcNfdFspetWW-0
- Board ini dipakai sebagai canvas visual pendamping untuk direction board dan token foundation, bukan pengganti source of truth di repo.

## Direction Summary
- KotobaHub harus terasa seperti produk belajar bahasa Jepang yang rapi, cerdas, dan memotivasi, tetapi tetap cukup ringan untuk dipakai setiap hari.
- Mood utamanya mengambil inspirasi dari atmosfer akademik Jepang modern: tenang, terstruktur, bersih, dan fokus.
- Visual tidak boleh terasa seperti aplikasi enterprise yang kaku, tetapi juga tidak boleh jatuh ke gaya anime-themed atau gamification yang terlalu berisik.

## Core Tone Pillars

### 1. Calm Discipline
- Fondasi visual harus terasa stabil dan terarah.
- Base color, spacing, dan layout perlu memberi rasa fokus seperti planner belajar atau workbook digital yang rapi.
- Halaman penting seperti onboarding, syllabus, dan progress sebaiknya mengutamakan clarity daripada dekorasi.

### 2. Youthful Momentum
- Produk harus tetap terasa relevan untuk digital-native user.
- Accent, motion, dan progress moments boleh terasa energik selama tidak membuat UI menjadi ramai.
- Semangat visualnya adalah “serius untuk dipakai belajar, tetapi tidak melelahkan untuk dipandang setiap hari”.

### 3. Smart Guidance
- KotobaHub bukan teman ngobrol santai penuh gimmick, melainkan study companion yang tahu kapan harus memberi arah.
- Hierarchy, progress indicator, empty state, dan feedback state harus terasa membantu user mengambil langkah berikutnya.
- Visual emphasis harus digunakan untuk guidance: apa yang penting, apa yang next, dan apa yang perlu diperbaiki.

### 4. Modern Japanese Academic Mood
- Referensi “Jepang” hadir lewat rasa disiplin, keteraturan, dan atmosfer belajar modern, bukan lewat ornamen literal.
- Hindari pattern, ilustrasi, atau simbol budaya yang terlalu stereotip.
- Gunakan struktur, proporsi, dan tone warna untuk menyampaikan mood tersebut.

## Brand Keywords

### Primary Keywords
- Focused
- Youthful
- Academic
- Approachable
- Motivating
- Precise

### Supporting Keywords
- Clean
- Guided
- Calm
- Reliable
- Structured
- Contemporary

### Keywords To Avoid
- Childish
- Over-gamified
- Corporate
- Luxury
- Neon
- Anime-literal

## Learning-Product Personality
- Peran produk: mentor belajar yang terorganisir, bukan entertainer.
- Suara visual: jelas, suportif, dan percaya diri.
- Cara tampil: memberi arah dan progress clarity tanpa terasa menggurui.
- Kesan akhir yang diinginkan: “produk ini membantu saya belajar dengan serius, tapi tetap enak dipakai”.

## Visual Reference Cues

### Reference Cue 1: Japanese Study Planner
- Gunakan grid yang rapi, ruang putih yang cukup, dan grouping yang jelas.
- Surface penting harus terasa seperti lembar kerja atau planner digital yang tertata.
- Gunakan emphasis seperlunya agar fokus user tetap ke materi dan progres.

### Reference Cue 2: Clean Productivity App
- Navigation, card, dan controls perlu terasa efisien dan tidak ornamental.
- Prioritaskan hierarchy yang kuat, iconography sederhana, dan feedback state yang ringkas.
- Tampilan harus modern, tetapi tetap hangat dan tidak terasa dingin seperti tool bisnis.

### Reference Cue 3: Exam-Prep Workbook
- Komponen seperti progress tracker, quiz state, dan section header sebaiknya terasa instructional.
- Gunakan section labeling yang jelas dan ritme visual yang konsisten.
- Kesan yang dicari adalah “structured learning path”, bukan “content feed”.

### Reference Cue 4: Campus Bulletin Energy
- Accent dapat dipakai untuk CTA, milestone, reminder, dan progress highlight.
- Highlight harus terasa seperti penanda penting pada materi belajar, bukan seperti banner promosi.
- Visual pop digunakan untuk momentum, bukan untuk mendominasi layar.

## Visual System Implications

### Layout
- Gunakan komposisi yang lebih banyak horizontal grouping dan panel bertingkat ringan daripada dashboard card-grid yang terlalu padat.
- Landing dan onboarding boleh punya sedikit atmosfer visual, tetapi area belajar inti harus lebih fungsional dan fokus.

### Color Usage
- `Seifuku Navy` menjadi anchor utama untuk rasa disiplin dan identitas brand.
- `Slate Blue` memberi napas visual untuk secondary emphasis, data, dan support surface.
- `Coral Energy` dipakai hemat untuk CTA, active progress, streak, dan feedback penting.

### Typography
- Gunakan sans-serif modern yang bersih dan mudah dipakai pada banyak state UI.
- Typography harus terasa tegas dan muda, bukan editorial mewah atau playful berlebihan.
- Perpaduan Latin dan Japanese support font harus terasa konsisten pada interface dan learning content.

### Iconography And Illustration
- Ikon sebaiknya sederhana, rounded secukupnya, dan mudah dipindai.
- Ilustrasi, jika dipakai, harus berbasis shape dan mood, bukan karakter maskot yang dominan.
- Hindari dekorasi visual yang tidak membantu learning flow.

### Motion
- Motion dipakai untuk menunjukkan transisi state belajar, perubahan progress, dan orientasi antarlayar.
- Animasi harus singkat, bersih, dan fungsional.
- Hindari bounce, overshoot, atau gesture yang membuat produk terasa terlalu casual.

## Suggested Moodboard Sections For Figma
- Brand thesis
- Tone pillars
- Keyword clusters
- Reference cues
- Color seed swatches
- Typography direction
- UI implication notes
- Non-goals

## Non-Goals
- Jangan membuat arah visual seperti aplikasi anime fandom atau merchandise culture.
- Jangan memakai dashboard enterprise dengan dominasi abu-abu dingin dan data density tinggi.
- Jangan menggunakan gaya full-neon, glassmorphism berat, atau playful illustration system yang mengalihkan fokus dari belajar.

## Handoff To DS-03
- `DS-03` harus mempertahankan `Seifuku Navy`, `Slate Blue`, dan `Coral Energy` sebagai seed brand resmi.
- Typography perlu mengutamakan keterbacaan, ritme belajar, dan kompatibilitas English + Japanese content.
- Token spacing, radius, shadow, dan motion harus mendukung mood “academic but friendly”, bukan “consumer social app”.
