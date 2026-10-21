# behrouzghaemi

Personal landing page — a static, single-page site.

- `index.html` — the page (markup, styles and the React runtime bundle)
- `resume.html` — résumé preview page (linked from the contact section)
- `cv.pdf` — the downloadable résumé; `cv.webp` is its preview image
- `assets/` — hero/about/contact videos, poster images and web fonts

## Run locally

```bash
python3 -m http.server 3000
# open http://localhost:3000
```

Or with Node:

```bash
npx serve .
```

### Updating the résumé

`resume.html` shows a generated preview image. If you replace `cv.pdf`,
regenerate `cv.webp` so the preview stays in sync:

```bash
pdftoppm -png -r 144 -singlefile cv.pdf /tmp/cv
python3 -c "from PIL import Image; Image.open('/tmp/cv.png').convert('RGB').save('cv.webp', 'WEBP', quality=90, method=6)"
```

## Deploy to Vercel

The project is a plain static site: no build step, no dependencies.

### Option 1 — Git (recommended)

1. Push this repository to GitHub.
2. In Vercel: **Add New → Project → Import Git Repository** and pick `xoxxel/behrouzghaemi`.
3. Framework preset: **Other**. Build command: leave empty. Output directory: leave empty (root).
4. **Deploy**. Every push to `main` redeploys automatically.

### Option 2 — Vercel CLI

```bash
npm i -g vercel
vercel        # first deploy / link the project
vercel --prod # production deploy
```

`vercel.json` sets `cleanUrls`, a no-cache policy for the HTML and one-day caching
for files in `/assets`, plus basic security headers.

### Custom domain

Vercel → Project → **Settings → Domains** → add the domain and point its DNS
records as instructed. The contact address in the page (`hi@behrouzghaemi.ir`)
is a plain `mailto:` link, so no mail configuration is required for the site itself.

---

## فارسی

این پروژه یک سایت استاتیک تک‌صفحه‌ای است و به هیچ مرحله build نیاز ندارد.

- فایل اصلی: `index.html`
- صفحه‌ی رزومه: `resume.html` (از بخش تماس لینک شده است)
- فایل PDF رزومه: `cv.pdf` — تصویر پیش‌نمایش آن `cv.webp` است
- ویدیوها، پوسترها و فونت‌ها: پوشه‌ی `assets/`

**پیش‌نمایش محلی**

```bash
python3 -m http.server 3000
```

**دپلوی روی Vercel**

۱. مخزن را روی GitHub پوش کنید.
۲. در Vercel گزینه‌ی **Add New → Project** را بزنید و مخزن `xoxxel/behrouzghaemi` را انتخاب کنید.
۳. Framework را روی **Other** بگذارید؛ Build Command و Output Directory را خالی رها کنید.
۴. **Deploy** را بزنید. از این پس هر push روی شاخه‌ی `main` به‌صورت خودکار دپلوی می‌شود.
  
یا با CLI:

```bash
npm i -g vercel
vercel        # اولین دپلوی و اتصال پروژه
vercel --prod # دپلوی نهایی روی دامنه‌ی اصلی
```

> نکته: کل صفحه به‌صورت استاتیک سرو می‌شود و ویدیوها از پوشه‌ی `assets/`
> استریم می‌شوند؛ بنابراین پوشه‌ی `assets` را همراه فایل `index.html` نگه دارید.

> اگر `cv.pdf` را عوض کردید، تصویر پیش‌نمایش `cv.webp` را هم
> با دستور بالا دوباره بسازید تا صفحه‌ی رزومه هم‌زمان با PDF به‌روز بماند.


