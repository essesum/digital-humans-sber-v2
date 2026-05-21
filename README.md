# Digital Humans · Sber — лендинг

Кинематографичный одностраничный сайт продукта **Digital Humans · Sber** — цифровые аватары для бизнеса, которые говорят с клиентом голосом, понимают контекст и работают прямо в браузере через SDK.

**Репозиторий приватный.**

## Зачем это

Лендинг для презентации продукта потенциальным клиентам и партнёрам:
- показывает, что аватар уже работает в реальных кейсах (банк, премиальный сегмент, ретейл);
- даёт техническую базу — Browser Avatar SDK;
- ставит продукт в один ряд с мировыми примерами категории.

## Live

- **Прод:** https://digital-humans-sber.netlify.app
- Netlify project: `digital-humans-sber` (siteId `d5ff387c-b939-4b99-9c5a-22c1a6ae3356`)

## Структура страницы

1. **Hero** — split-screen с фоновым видео-сиквенсом, заголовок «Интерфейс, который тебя *понимает.*», CTA.
2. **Российские кейсы** (full-bleed cinematic, эстетика Runway ML):
   - **ГигаПомощник** — аватар в офисе банка
   - **СберПервый** — split layout (16:9 landscape + 9:16 portrait), премиальный банкинг
   - **М.Видео** — аватар-продавец
3. **Мировые кейсы** (5 карточек):
   - ABBA Voyage · $175M бюджет
   - Leonardo da Vinci hologram на VivaTech · 1 200+ live exchanges
   - Synthesia · $4B оценка
   - AI-аватары в китайском live-commerce · $7.6M за 7 часов
   - DeepBrain AI Studios · 150+ языков
4. **Browser Avatar SDK** — 4 ключевых фичи: WebGPU/WASM в браузере, npm-пакет, любой голос → живая мимика, контроль поведения.
5. **Метрики** — 3× конверсия, 24/7, −60% нагрузки на колл-центр.
6. **CTA + кот** — «Готовы запустить своего аватара?» в одном блоке с анимацией кота (id `#demo`, на него ведут якоря из навигации и hero).

## Дизайн-система

Полная спека: [`docs/superpowers/specs/2026-04-28-cinematic-redesign-design.md`](docs/superpowers/specs/2026-04-28-cinematic-redesign-design.md).

Кратко:
- **Шрифты:** Fraunces (display, 800, italic для эмфазиса) + DM Sans (UI).
- **Цвет:** фон `#070707`, текст `#fff`, кислотный акцент `#C8FF00` только в микро-деталях (live-dot, короткий divider).
- **Анимации:** кастомный easing `cubic-bezier(0.23, 1, 0.32, 1)`, hero entrance fade+slide, stagger по `IntersectionObserver`, cinematic case overlay reveal на скролл.
- **Шум** в SVG-overlay поверх всего контента для киношного зерна.

## Структура репозитория

```
.
├── index.html                    # вся страница: HTML + inline CSS + inline JS
├── images/                       # локальные превью для «Мировых кейсов»
│   ├── abba.jpg
│   ├── china.jpg
│   ├── davinci-hologram.jpg
│   ├── deepbrain.jpg
│   └── synthesia.jpg
├── videos/                       # видео-ассеты (см. ниже)
├── docs/superpowers/             # план и дизайн-спека редизайна
│   ├── plans/2026-04-28-cinematic-redesign.md
│   └── specs/2026-04-28-cinematic-redesign-design.md
└── .netlify/                     # привязка к Netlify-проекту
```

Размеры: `videos/` ~115 МБ, `images/` ~384 КБ, `index.html` ~40 КБ.

## Видео-ассеты

### Используются в `index.html` (7 файлов)

| Файл | Где применяется |
|------|------|
| `hero-voice-ai.mp4` | hero — фоновое видео, фаза «in» |
| `hero-voice-ai-out.mp4` | hero — фоновое видео, фаза «out» (sequence loop) |
| `giga-assistant-3.mp4` | кейс ГигаПомощник |
| `sberperv-irina.mp4` | кейс СберПервый, landscape (16:9) |
| `sberperv-mvp-sb1.mp4` | кейс СберПервый, portrait (9:16) |
| `mvideo-case.mp4` | кейс М.Видео |
| `cat.mp4` | финальный CTA-блок с котом |

### Резервные и альтернативные дубли (в репо, на странице не используются)

`avatar-example.mp4`, `cinematic-avatar.mp4`, `credit.mp4`, `doctor-bg.mp4`, `giga-assistant.mp4`, `gigaassistant-demo.mp4`, `mvideo-emvi.mp4`, `mvideo-original.mp4`, `sberperv-mvp.mp4`, `seedance-2.mp4`.

Сохранены сознательно как запасные варианты монтажей/кейсов на случай правок.

## Деплой

Netlify-сайт **не привязан к этому репозиторию для CI-сборки**. В `.netlify/netlify.toml` поле `publish` указывает на постороннюю локальную папку и при ручном деплое игнорируется (если передать `--dir .`).

Полный цикл выкатки:

```bash
git push origin main
netlify deploy --prod --dir . --site d5ff387c-b939-4b99-9c5a-22c1a6ae3356
```

⚠️ `--dir .` обязателен — иначе подхватится неправильный путь публикации из `netlify.toml`.

## История правок (краткая хронология)

1. **Cinematic redesign** (2026-04-28, спека в `docs/superpowers/specs/`) — переход со стандартного SaaS-шаблона на эстетику Runway ML.
2. **Hero video sequence:** in → 5 секунд паузы на последнем кадре → out → повтор. Robust preload + `play().catch(...)` для надёжного автоплея.
3. **СберПервый split layout:** landscape слева + portrait-вертикалка справа на десктопе, IntersectionObserver-driven play для портретного видео.
4. **SDK-секция, метрики, финальный CTA-блок** добавлены.
5. **Мировые кейсы:** изначально 6, потом убран HeyGen Avatar V → осталось 5. У карточек: локальное фото (`images/davinci-hologram.jpg` скачан с CDN ravatar), для остальных — кадр-обложка из YouTube, **тоже захостена локально**. YouTube-чипы со ссылкой на видео сделаны `referrerpolicy="no-referrer"`.
6. **YouTube-капча на VPN — пофикшено:** изначально превью карточек грузились с `img.youtube.com`, и на VPN с ротацией IP это создавало mismatch (`IP_A ≠ IP_B`) → бот-стенка при клике. Все превью переведены на локальные файлы → страница не делает ни одного запроса к youtube-доменам → mismatch невозможен.
7. **Кот + CTA:** объединены в один финальный блок. Дублирующая DEMO-секция удалена. Фраза «Аватаром может стать кто угодно» убрана.

## Замечания на будущее

- Текст карточек/кейсов и любые формулировки на лендинге — авторские, без правок без явной просьбы.
- При добавлении новых кейсов: превью всегда хостить локально в `images/` (см. fix-капчи выше).
- Видео — локально в `videos/`. Не подключать внешние CDN-видео.
