# KotobaHub Design Token Foundation

## Status
- Dokumen ini menyelesaikan task `DS-03`.
- Dokumen ini menetapkan token awal untuk warna, tipografi, spacing, radius, shadow, focus state, dan motion principles.
- Dokumen ini menjadi source of truth awal sebelum masuk ke responsive rules, component inventory, dan high-fidelity system design.

## Dependencies
- [brand-identity-brief.md](./brand-identity-brief.md)
- [design-direction-board.md](./design-direction-board.md)
- [mvp-plan.md](../mvp-plan.md)

## Figma Reference
- System design canvas untuk DS-02 dan DS-03 ada di Figma: https://www.figma.com/design/iCvRU1So1SOrAl58xFZurg/KotobaHub?node-id=0-1&p=f&t=ddPurcNfdFspetWW-0
- Representasi visual token di Figma harus mengikuti nilai token pada dokumen ini bila terjadi perbedaan.

## Reconciliation Note
- `mvp-plan.md` sebelumnya menyebut token warna awal `ink`, `paper`, `matcha`, `amber`, dan `coral` dalam bentuk high-level direction.
- Setelah `DS-01` dan `DS-02`, brand seed resmi yang dikunci adalah `Seifuku Navy`, `Slate Blue`, dan `Coral Energy`.
- Mulai dokumen ini, struktur token dipecah menjadi:
  - brand tokens untuk identitas utama
  - neutral surface/text tokens untuk readability
  - semantic/support tokens untuk success, warning, error, dan info
- Dengan begitu, arahan lama di `mvp-plan.md` tetap terwakili secara semantik tanpa menabrak brief brand yang lebih final.

## Token Principles
- Token harus semantic-first agar mudah dipakai lintas landing page, app shell, learning flow, dan dashboard.
- Brand token tidak dipakai langsung untuk semua state; gunakan role token agar contrast dan accessibility lebih mudah dikontrol.
- Semua token awal diasumsikan dipakai di mode terang terlebih dahulu karena fase MVP belum mengunci dark mode.

## Color Foundation

### Brand Seeds
| Token | Value | Purpose |
| --- | --- | --- |
| `brand.primary` | `#1D1D36` | identitas utama, strong surface, primary nav, brand moments |
| `brand.secondary` | `#6F7FA6` | supporting emphasis, data accent, secondary highlight |
| `brand.accent` | `#FF7A59` | CTA, active state, streak, reward, momentum cue |

### Neutral And Surface Tokens
| Token | Value | Purpose |
| --- | --- | --- |
| `bg.canvas` | `#F7F8FC` | background aplikasi utama |
| `bg.subtle` | `#EFF2F8` | section tint, grouped background |
| `surface.default` | `#FFFFFF` | card, sheet, panel dasar |
| `surface.elevated` | `#FBFCFE` | modal ringan, floating card, highlighted surface |
| `surface.strong` | `#232743` | dark emphasis surface, banner, inverse block |
| `border.subtle` | `#E2E6F0` | divider ringan dan outline form default |
| `border.default` | `#CDD4E4` | border komponen standar |
| `border.strong` | `#A7B2C8` | border aktif ringan, selected support |

### Text Tokens
| Token | Value | Purpose |
| --- | --- | --- |
| `text.primary` | `#1F2340` | body text utama |
| `text.secondary` | `#54607C` | body support, label sekunder |
| `text.muted` | `#7A86A3` | hint, metadata, caption |
| `text.inverse` | `#FFFFFF` | text di surface gelap |
| `text.accent` | `#D95F41` | inline emphasis yang terkait momentum |

### Semantic Tokens
| Token | Value | Purpose |
| --- | --- | --- |
| `state.success` | `#4E8B6F` | mastery up, correct answer, completion cue |
| `state.success-bg` | `#E8F4ED` | success surface ringan |
| `state.success-hover` | `#447B61` | hover state untuk success button atau interactive chip |
| `state.success-active` | `#396853` | active atau pressed state untuk success button |
| `state.warning` | `#D89A3D` | caution, pending, review soon |
| `state.warning-bg` | `#FFF5E6` | warning surface ringan |
| `state.warning-hover` | `#C28723` | hover state untuk warning button atau interactive chip |
| `state.warning-active` | `#A96F11` | active atau pressed state untuk warning button |
| `state.error` | `#C95A5A` | incorrect answer, destructive warning |
| `state.error-bg` | `#FBECEC` | error surface ringan |
| `state.error-hover` | `#B54A4A` | hover state untuk error button atau destructive action |
| `state.error-active` | `#963A3A` | active atau pressed state untuk error button |
| `state.info` | `#4D78C9` | informational chip, neutral highlight |
| `state.info-bg` | `#ECF2FF` | info surface ringan |
| `state.info-hover` | `#3E68B8` | hover state untuk info button atau interactive chip |
| `state.info-active` | `#31559D` | active atau pressed state untuk info button |

### Semantic Interaction Rule
- Untuk semantic button atau chip yang bersifat interactive, minimal siapkan empat state: `normal`, `bg`, `hover`, dan `active`.
- `normal` dipakai sebagai warna inti semantic.
- `bg` dipakai untuk tinted background atau subtle container.
- `hover` dan `active` harus diturunkan dari warna semantic utama dengan arah yang lebih gelap agar affordance interaksi tetap jelas di mode terang.
- State turunan ini diprioritaskan untuk button-like controls, status pill interaktif, filter chips, dan quick action feedback.

## Color Usage Rules
- `brand.primary` harus paling dominan pada identity moments, tetapi jangan dipakai sebagai background penuh untuk semua layar.
- `brand.secondary` dipakai untuk supporting emphasis seperti filters, data visualization, dan secondary badges.
- `brand.accent` hanya dipakai pada elemen yang memang butuh urgency atau momentum visual.
- Semantic colors harus tetap lebih rendah prioritasnya daripada hierarchy konten utama.
- Background utama harus tetap terang agar konten belajar panjang tetap nyaman dibaca.

## Typography Foundation

### Font Pair
- Primary UI font: `Plus Jakarta Sans`
- Japanese support font: `Noto Sans JP`

### Typography Principles
- UI harus terasa modern dan muda, tetapi tetap stabil untuk informasi yang padat.
- Font weight medium dan semibold digunakan untuk hierarchy; bold hanya untuk headline atau score utama.
- `Noto Sans JP` dipakai saat konten Jepang perlu tampil alami dan konsisten dengan materi belajar.

### Type Scale
| Token | Size / Line Height | Use |
| --- | --- | --- |
| `type.display` | `40 / 48` | landing hero, page hero, major score |
| `type.h1` | `32 / 40` | page heading utama |
| `type.h2` | `24 / 32` | section heading |
| `type.h3` | `20 / 28` | card title, step title |
| `type.body-lg` | `18 / 28` | onboarding explanation, highlighted paragraph |
| `type.body` | `16 / 24` | body text default |
| `type.body-sm` | `14 / 20` | helper text, secondary copy |
| `type.label` | `13 / 18` | field label, badge label |
| `type.caption` | `12 / 16` | metadata, footnote, tiny status |

### Font Weight Guidance
| Token | Weight | Use |
| --- | --- | --- |
| `weight.regular` | `400` | long-form body |
| `weight.medium` | `500` | labels, compact emphasis |
| `weight.semibold` | `600` | section heading, active control |
| `weight.bold` | `700` | key metrics, strong headline |

## Spacing Foundation
- Gunakan base scale `4px` agar layout tetap fleksibel untuk mobile dan desktop.

| Token | Value |
| --- | --- |
| `space.1` | `4px` |
| `space.2` | `8px` |
| `space.3` | `12px` |
| `space.4` | `16px` |
| `space.5` | `20px` |
| `space.6` | `24px` |
| `space.8` | `32px` |
| `space.10` | `40px` |
| `space.12` | `48px` |
| `space.16` | `64px` |

### Spacing Intent
- `space.2` sampai `space.4` untuk internal control spacing.
- `space.5` sampai `space.8` untuk card padding, section gap kecil, dan stacked content rhythm.
- `space.10` ke atas dipakai untuk page sections dan area yang butuh napas visual.

## Radius Foundation
| Token | Value | Use |
| --- | --- | --- |
| `radius.sm` | `8px` | input, chip, small button |
| `radius.md` | `12px` | default card dan button |
| `radius.lg` | `16px` | prominent panel, dialog content |
| `radius.xl` | `24px` | hero panel, special feature block |
| `radius.full` | `999px` | pill, progress badge, avatar ring |

### Radius Guidance
- Sudut membulat harus terasa modern dan ramah, tetapi jangan terlalu bubble-like.
- `radius.md` menjadi default utama untuk kebanyakan komponen.

## Shadow And Elevation
| Token | Value | Use |
| --- | --- | --- |
| `shadow.sm` | `0 1px 2px rgba(20, 27, 45, 0.08)` | hairline lift untuk input atau chip |
| `shadow.md` | `0 8px 24px rgba(29, 35, 64, 0.08)` | default card lift, dropdown |
| `shadow.lg` | `0 16px 40px rgba(29, 35, 64, 0.12)` | modal, featured surface |

### Elevation Guidance
- Jangan menumpuk shadow berat di banyak card sekaligus.
- Gunakan contrast surface dan border lebih dulu; shadow hanya menegaskan layer.

## Focus State
| Token | Value | Use |
| --- | --- | --- |
| `focus.ring.color` | `#FF7A59` | focus outline utama |
| `focus.ring.outer` | `rgba(255, 122, 89, 0.22)` | outer halo |
| `focus.ring.width` | `2px` | stroke utama |
| `focus.ring.offset` | `2px` | jarak dari komponen |

### Focus Guidance
- Focus state harus sangat jelas pada keyboard navigation.
- `brand.accent` dipakai untuk focus karena mudah terlihat di atas surface terang maupun gelap.
- Jangan hanya mengandalkan perubahan shadow atau border tipis untuk focus-visible.

## Motion Principles

### Motion Intent
- Motion harus membantu orientasi user saat berpindah state belajar.
- Animasi kecil boleh menambah rasa momentum pada progress, tetapi tidak boleh mengganggu konsentrasi.

### Motion Tokens
| Token | Value | Use |
| --- | --- | --- |
| `motion.fast` | `120ms` | hover, pressed, tiny icon shift |
| `motion.base` | `180ms` | panel change, input feedback |
| `motion.slow` | `240ms` | modal, section reveal, route transition ringan |
| `motion.emphasis` | `320ms` | celebratory progress reveal secukupnya |

### Easing Tokens
| Token | Value | Use |
| --- | --- | --- |
| `ease.standard` | `cubic-bezier(0.2, 0, 0, 1)` | default UI transition |
| `ease.enter` | `cubic-bezier(0.16, 1, 0.3, 1)` | entering panels |
| `ease.exit` | `cubic-bezier(0.4, 0, 1, 1)` | exiting panels |

### Motion Rules
- Hindari animasi looping yang tidak punya fungsi.
- Progress celebration cukup ringan: fade, translate kecil, atau number tick.
- Flow belajar inti harus terasa cepat dan responsif, terutama untuk flashcard dan question answering.

## Early Component Implications
- Button primary memakai `brand.primary`; button high-energy CTA atau milestone action boleh memakai `brand.accent`.
- Card default memakai `surface.default`, `border.subtle`, dan `radius.md`.
- Progress indicators boleh memadukan `brand.secondary`, `brand.accent`, dan `state.success` sesuai konteks.
- Form controls harus mengutamakan focus clarity dan spacing yang tenang.
- Button semantic sebaiknya memakai pasangan `normal -> hover -> active` yang konsisten dengan `*-bg` sebagai subtle variant atau low-emphasis state.

## Implementation Note
- Saat implementasi dimulai, token ini sebaiknya diturunkan ke CSS custom properties dan `tailwind.config` atau layer token setara.
- Nama token runtime boleh memakai format teknis seperti `--color-brand-primary`, selama semantic meaning dari dokumen ini tetap dipertahankan.

## Follow-Up Dependencies
- `DS-04` harus memakai token spacing, typography, dan radius ini untuk layout rules mobile dan desktop.
- `DS-07` harus memakai token foundation ini saat menentukan komponen `shadcn` mana yang cukup di-theme dan mana yang perlu custom styling lebih jauh.
- `DS-08` harus memvalidasi kembali contrast, hierarchy, dan consistency ketika high-fidelity screen final disusun.
