# Digital Humans Sber — Cinematic Redesign

**Date:** 2026-04-28
**Status:** Approved, ready for implementation

---

## Goal

Redesign the Digital Humans Sber site from a standard SaaS template into a cinematic, disruptive landing page. Reference: Runway ML aesthetic — full-bleed presence, one strong statement, no grid clutter.

---

## Design System

### Typography
- **Display / headlines:** Fraunces (Google Fonts) — `ital,opsz,wght@0,9..144,800;1,9..144,800`
  - Size: 56–72px, `line-height: 0.88`, `letter-spacing: -3px`
  - Italic used on the final word for cinematic emphasis
- **Body / UI:** DM Sans — weights 400, 500
- **Eyebrow labels:** 8px, `letter-spacing: 3px`, uppercase, `rgba(255,255,255,0.18)`

### Color
- Background: `#070707` (near-black)
- Text: `#ffffff`
- Acid accent: `#C8FF00` — used **only** in micro-details:
  - Animated live dot in eyebrows (`@keyframes blink`)
  - Short divider line (32px × 1.5px) below headline
  - No highlights, no underlines, no large color blocks
- Borders / dividers: `rgba(255,255,255,0.06–0.10)`

### Motion
- Custom easing: `--ease-out: cubic-bezier(0.23, 1, 0.32, 1)`
- Custom easing: `--ease-in-out: cubic-bezier(0.77, 0, 0.175, 1)`
- Hero entrance: `opacity 0→1 + translateY(24px→0)`, 700ms, ease-out, `animation-fill-mode: both`
- Case cards stagger: `nth-child` delays 0 / 80 / 160ms, `IntersectionObserver` trigger at `threshold: 0.15`
- Buttons: `scale(0.97)` on `:active`, 160ms ease-out
- No animations on keyboard-initiated actions

---

## Page Structure

### 1. Hero — Split Screen

**Layout:** Two-column, 50/50, full viewport height.

**Left column (copy):**
```
[eyebrow]  ● DIGITAL HUMANS · SBER

[headline — Fraunces 64px italic finish]
Интерфейс,
который тебя
понимает.

[divider — 32px × 1.5px #C8FF00]

[subheadline — DM Sans 15px, rgba white 0.5]
Живой аватар говорит с клиентом голосом —
слышит, адаптируется, отвечает.
Без форм, без скрипта, 24/7.

[CTAs]
[Поговорить с аватаром]  Кейсы →
```

**Right column (visual):**
- Full-height avatar video (`object-fit: cover`), muted autoplay loop
- No border, no frame — bleeds to the right edge
- Sound toggle button (bottom-right corner)

---

### 2. Cinematic Case Tape

Full-width sections, one per case. Each case = full-bleed video + minimal text overlay.

**Cases (in order):**
1. **М.Видео** — retail assistant avatar
2. **ГигаПомощник** — AI voice assistant (existing video)
3. **СберПервый** — premium banking avatar (existing videos: MVP + Irina)

**Per-case layout:**
```
[full-width video, autoplay muted, loop]

[bottom overlay — gradient]
  [client logo / name]  [one-line description]
  [sound toggle]
```

- Video height: `min(56vw, 680px)`
- Overlay: `linear-gradient(to top, rgba(0,0,0,0.7), transparent)`
- Text: Fraunces client name large, DM Sans description small

---

### 3. Metrics Strip

Three numbers, full-width, dark background.

```
  [number]        [number]        [number]
  [label]         [label]         [label]
```

Numbers in Fraunces italic, large. Labels in DM Sans small caps.
Stagger entrance animation on scroll.

---

### 4. Demo CTA

Full-width dark section, centered.

```
[Fraunces headline — 2 lines]
Готовы запустить
свой аватар?

[CTA button — #C8FF00 background, black text]
Поговорить с аватаром

[ghost link]
Смотреть все кейсы →
```

---

## What Changes vs Current Site

### Remove
- Manifesto text block ("Мы верим...")
- Pillar cards grid (3 columns)
- Bridge quote section
- Tech stack section (WASM, WebRTC badges)
- Standard navbar with many links

### Keep
- All existing videos (converted, optimized)
- Sound toggle functionality
- Metrics numbers (update copy if needed)
- СберПервый section content

### Add
- Fraunces font
- Split-screen hero
- Full-bleed cinematic case layout
- Animated eyebrow with live dot

---

## Existing Assets

| File | Used in |
|------|---------|
| `videos/cinematic-avatar.mp4` | Hero — right column background |
| `videos/mvideo-case.mp4` | Case: М.Видео (primary) |
| `videos/mvideo-emvi.mp4` | Case: М.Видео (alt / secondary) |
| `videos/gigaassistant-demo.mp4` | Case: ГигаПомощник |
| `videos/sberperv-mvp.mp4` | Case: СберПервый (product demo) |
| `videos/sberperv-irina.mp4` | Case: СберПервый (avatar close-up) |
| `videos/credit.mp4` | Reserve / possible hero alt |

---

## Success Criteria

- Opens in <3s on mobile (videos lazy-load below fold)
- All videos play on iOS Safari (muted autoplay)
- Sound toggle works on all videos
- Fraunces loads before first paint (preconnect + `font-display: swap`)
- No layout shift on video load (`aspect-ratio` placeholders)
