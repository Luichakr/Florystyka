# Vittoria Fiore Gallery — План запуска в продакшен

Текущий статус: **прототип на GitHub Pages**
[luichakr.github.io/Florystyka](https://luichakr.github.io/Florystyka/) · public

---

## Этап 1 — Backend для форм (1–2 дня) ⚡ КРИТИЧЕСКИЙ

Без этого формы только пишут в console — заявки не доходят.

### Варианты (по сложности)

| Решение | Плюсы | Минусы | Стоимость |
|---|---|---|---|
| **Formspree** | 0 кода, готов за 10 мин | 50 submit/мес бесплатно | $10/мес дальше |
| **Telegram-бот** | Виктория получает заявки в чат мгновенно | Нужен серверлесс (Cloudflare Workers/Vercel) | Бесплатно |
| **Resend + Vercel API** | Письма на email Виктории, кастомные шаблоны | Нужна настройка | Бесплатно до 3 000 писем/мес |
| **Свой backend** | Полный контроль, CRM | Нужно писать и хостить | Время + сервер |

**Рекомендация:** Telegram-бот + Formspree fallback на email.

### Что подключить
- В JS `handleSubmit` отправлять `fetch('/api/lead', {body: data})` или прямо в Formspree
- На каждый source-label — отдельный шаблон письма / Telegram-сообщения
- Защита: honeypot field + Cloudflare Turnstile / hCaptcha

---

## Этап 2 — Реальный контент (1 неделя)

- [ ] **Реальный телефон** Виктории — везде заменить `+48 XXX XXX XXX`
- [ ] **Реальный email** — заменить `hello@vittoriagallery.com` (или подтвердить)
- [ ] **Адрес** студии / точки самовывоза
- [ ] **Google рейтинг** — обновить `4.9 · 182 opinie` на реальные цифры
- [ ] **Часы работы** в контактной info
- [ ] **Портфолио** — реальные названия проектов (сейчас демо: Bristol, Atelier Amaro, Ferrari Showroom…)
- [ ] **Имена клиентов B2B** — можно ли публиковать
- [ ] **Описание Виктории** — личная история, био
- [ ] **Прайсинг букетов** — точные суммы и наличие сезонных букетов

---

## Этап 3 — Фото-контент (когда будет готов)

В текущем прототипе картинок нет — везде типографика-driven композиции. Когда будут фото:

- [ ] **Hero** — портретное фото Виктории справа (заменить editorial-блок «98%»)
- [ ] **Service-карточки** — фото в правом нижнем углу каждой карточки
- [ ] **Portfolio** — фото-фон для каждого case (поверх gold-номеров)
- [ ] **Bouquets** — реальные фото букетов
- [ ] **About** — портрет / фото с работы в студии

Размеры: hero 1200×900, services 600×400, portfolio 800×600, bouquets 600×800.
Формат: WebP (с JPG fallback), lazy-load.

---

## Этап 4 — Домен + хостинг продакшена

Сейчас: GitHub Pages (бесплатно, медленнее, без SSR).

**Рекомендация:** перевести на **Vercel** или **Cloudflare Pages**:
- Edge-CDN, быстрее загрузка
- Serverless-функции для форм
- Можно сразу подцепить домен **vittoriagallery.com**
- Бесплатно для трафика этого размера

### Шаги:
1. Создать аккаунт Vercel, подключить GitHub-репо
2. Привязать домен (изменить NS / A-записи)
3. Включить Web Analytics (free)
4. Настроить redirects (www → apex, http → https)

---

## Этап 5 — SEO

### Базовое (день)
- [ ] **Meta tags**: description, og:image (брендовая картинка), twitter:card
- [ ] **Open Graph** — preview-картинка для шеринга в WhatsApp/Telegram/FB
- [ ] **`<title>`** — оптимизировать под ключевики («Luksusowa florystyka Warszawa», «Aranżacje kwiatowe dla hoteli»)
- [ ] **`robots.txt`** + **`sitemap.xml`**
- [ ] **JSON-LD LocalBusiness schema** — для богатых сниппетов в Google
- [ ] **alt-тексты** ко всем фото (когда добавятся)

### Контент-SEO (неделя)
- [ ] Блог-секция (на старте 5–10 статей): «Jak wybrać kwiaty do hotelu», «Florystyka dla restauracji premium» — длинные тексты под запросы
- [ ] Локальное SEO: Google My Business, OpenStreetMap, mapy.cz
- [ ] Каталоги: pf.pl, panoramafirm.pl

---

## Этап 6 — Локализация (RU/EN)

Сейчас весь текст PL. Toggle PL/RU/EN в навигации существует визуально, но не работает.

**План:**
- Вынести все тексты в JSON (`pl.json`, `ru.json`, `en.json`)
- Простой data-i18n атрибут на каждом текстовом элементе
- При клике на PL/RU/EN — подгружать перевод и обновлять DOM
- URL: `?lang=ru` для шеринга

Объём перевода: ~800 слов на язык.

---

## Этап 7 — Performance + Lighthouse

Цель: **90+ на всех 4 метриках** (Performance, A11y, Best Practices, SEO).

- [ ] Минифицировать HTML/CSS/JS (build-step через Vite или просто prettier-minify)
- [ ] Preload critical fonts
- [ ] Заменить `display: swap` → `display: optional` для menos CLS
- [ ] Изображения через `<picture>` с AVIF/WebP
- [ ] Inline critical CSS (above-the-fold)
- [ ] Defer non-critical JS

---

## Этап 8 — Legal

Обязательно для Польши (GDPR/RODO):
- [ ] **Polityka prywatności** — страница `/polityka`
- [ ] **Regulamin** — для продажи букетов (b2c)
- [ ] **Cookie banner** — согласие на аналитику (Cookiebot или своё)
- [ ] Контакт IODO / Inspektor Danych Osobowych (если нужно)
- [ ] Информация о владельце (NIP/REGON) в footer

---

## Этап 9 — Marketing / Launch

### Pre-launch
- [ ] Google My Business — заявить бизнес, получить пин на карте
- [ ] Instagram-аккаунт — единый стиль ленты под сайт
- [ ] Pinterest — pin-board с портфолио (важный канал для свадеб)
- [ ] LinkedIn — для B2B-сегмента

### Launch
- [ ] Press release — польская пресса (Vogue PL, Elle Decor)
- [ ] Подарок-промо первым клиентам (использовать `-10%` оффер)
- [ ] Email blast по существующим контактам Виктории

### Post-launch (continuous)
- [ ] Google Ads — search для «kwiaciarnia premium Warszawa»
- [ ] Meta Ads — таргет для B2C / свадебных клиентов
- [ ] Контент-маркетинг — посты в Instagram 3×/неделю

---

## Этап 10 — Аналитика и оптимизация

- [ ] **Google Analytics 4** + Google Tag Manager
- [ ] **Plausible** (privacy-friendly альтернатива)
- [ ] **Hotjar / Microsoft Clarity** — записи сессий, heatmaps
- [ ] **A/B тесты** — основной CTA (текст кнопки, цвет, расположение)
- [ ] Cели в GA: submit каждой формы — отдельная конверсия по `source`-метке

---

## Приоритеты на ближайшие 7 дней

1. **Day 1–2:** подключить backend для форм (Telegram-бот или Formspree)
2. **Day 3:** заменить все placeholder-данные на реальные
3. **Day 4:** перевести с GitHub Pages на Vercel, привязать vittoriagallery.com
4. **Day 5:** SEO meta tags + sitemap + Google My Business
5. **Day 6:** Cookie-banner + Polityka prywatności
6. **Day 7:** запустить Google Ads со $50–$100 на тест

После этого — итерации по аналитике и контенту.

---

## Контакты по ходу работы

- **GitHub repo:** [Luichakr/Florystyka](https://github.com/Luichakr/Florystyka)
- **Live preview:** [luichakr.github.io/Florystyka](https://luichakr.github.io/Florystyka/)
- **Целевой домен:** [vittoriagallery.com](https://www.vittoriagallery.com/)
