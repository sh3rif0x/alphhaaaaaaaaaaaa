# Services System Documentation

Vanilla JS + HTML + CSS project (حداد الرياض). This document explains how the `/services` section works, how it is structured, and how to run, extend, debug, and deploy it.

---

## 1. The Idea

One HTML page serves **every** service URL. No per-service folders or files.

| URL                     | What is shown                            |
| ----------------------- | ---------------------------------------- |
| `/services/`            | List of all services                     |
| `/services/iron-gates/` | Detail page for the `iron-gates` service |
| `/services/unknown/`    | 404 "service not found" block            |

All service content lives in **one JSON file**. JavaScript reads the slug from the URL, finds the matching service in the JSON, and renders it.

```
Browser: /services/iron-gates/
        │
        ▼
server.js  ──►  returns services/index.html  (for any /services/<slug>)
        │
        ▼
services/script.js
   ├─ loads header + footer components
   ├─ fetch("/data/services.json")
   ├─ getServiceSlug()  →  "iron-gates"
   ├─ findService()     →  matching object (or null)
   └─ calls template.js
        ├─ renderList()      → cards for /services/
        ├─ renderService()   → detail page
        └─ renderNotFound()  → 404 block
```

---

## 2. Project Structure

```
hadad/
├── index.html
├── main.css / main.js
├── server.js                  ← local dev server (URL rewrite)
├── assets/                    ← images
├── components/
│   ├── header/  (index.html, script.js, style.css)
│   └── footer/  (index.html, script.js, style.css)
├── data/
│   ├── services.json          ← SERVICE DATA (single source of truth)
│   ├── projects.json
│   └── blog.json
├── about/ articles/ contact/ projects/
└── services/
    ├── index.html             ← page shell (containers only)
    ├── script.js              ← routing + loading + show/hide
    ├── template.js            ← HTML generation
    └── style.css
```

**Removed:** the old `services/<slug>/index.html` symlink folders and `services/services.json`. They are not needed.

### Responsibility split

| File | Responsibility | Must NOT do |
|---|---|---|
| `services/index.html` | Static shell and empty containers | Contain service content |
| `services/script.js` | Load components and data, read the URL, choose the view | Build big HTML strings |
| `services/template.js` | Turn data into HTML strings | Fetch data or touch the DOM |
| `data/services.json` | Content | Contain HTML |
| `server.js` | Serve files, rewrite `/services/<slug>` | Contain app logic |

---

## 3. Data Format: `data/services.json`

An array of service objects:

```json
[
  {
    "slug": "iron-gates",
    "title": "البوابات الحديد",
    "image": "/assets/hero-1.jpeg",
    "heroAlt": "بوابات حديد",
    "heroDescription": "Short text shown on the card and in the hero.",
    "article": {
      "introTitle": "Optional heading for the intro",
      "intro": "Optional intro paragraph",
      "sections": [
        { "title": "Section title", "content": "Section text" }
      ],
      "faq": [
        { "question": "Question?", "answer": "Answer." }
      ]
    }
  }
]
```

| Field | Required | Notes |
|---|---|---|
| `slug` | Yes | The URL part. Lowercase, hyphens, unique. |
| `title` | Yes | Card title, hero title, page title |
| `image` | Yes | See image path rules below |
| `heroAlt` | No | Falls back to `title` |
| `heroDescription` | No | Card and hero text |
| `article.*` | No | Missing parts are skipped safely |

`script.js` also accepts `{ "services": [ ... ] }` as a wrapper.

### Image path rules (`getImagePath` in `template.js`)

| In JSON | Becomes |
|---|---|
| `/assets/a.jpg` | `/assets/a.jpg` |
| `https://...` | unchanged |
| `../assets/a.jpg` | `/assets/a.jpg` |
| `./a.jpg` | `/a.jpg` |
| `assets/a.jpg` | `/assets/a.jpg` |

Best practice: always write absolute paths starting with `/`.

---

## 4. Key Rules That Make It Work

1. **Always use absolute URLs** (`/data/services.json`, `/services/script.js`). Relative URLs like `../data/services.json` break on `/services/iron-gates/` because `..` resolves to `/services/`, giving `/services/data/services.json` (404).
2. **The server must rewrite** `/services/<slug>` to `services/index.html`. Without that, the browser gets a 404 before JavaScript runs.
3. **VS Code Live Server (port 5500) cannot rewrite URLs.** Use `server.js` (or a real server) instead.
4. **`getServiceSlug()`** takes the segment after `services` in the pathname. `/services/` gives `null` (list view).
5. **Module script**: `<script type="module">` runs after parsing, so `init()` handles both `loading` and already-loaded states.

---

## 5. Files

### 5.1 `server.js` (local dev server, no dependencies)

```js
const http = require("http");
const fs = require("fs");
const path = require("path");

const ROOT = __dirname;
const PORT = 5500;

const TYPES = {
    ".html": "text/html; charset=utf-8",
    ".css": "text/css; charset=utf-8",
    ".js": "text/javascript; charset=utf-8",
    ".json": "application/json; charset=utf-8",
    ".png": "image/png",
    ".jpg": "image/jpeg",
    ".jpeg": "image/jpeg",
    ".webp": "image/webp",
    ".svg": "image/svg+xml",
    ".ico": "image/x-icon"
};

function send(res, file, status = 200) {
    fs.readFile(file, (err, data) => {
        if (err) {
            res.writeHead(404, { "Content-Type": "text/plain; charset=utf-8" });
            return res.end("404 Not Found");
        }
        res.writeHead(status, {
            "Content-Type": TYPES[path.extname(file).toLowerCase()] || "application/octet-stream"
        });
        res.end(data);
    });
}

http.createServer((req, res) => {
    const urlPath = decodeURIComponent(req.url.split("?")[0]);
    let file = path.join(ROOT, urlPath);

    if (!file.startsWith(ROOT)) {
        res.writeHead(403);
        return res.end("Forbidden");
    }

    // /services/<slug>  ->  services/index.html
    if (/^\/services\/[^/.]+\/?$/.test(urlPath)) {
        return send(res, path.join(ROOT, "services", "index.html"));
    }

    if (fs.existsSync(file) && fs.statSync(file).isDirectory()) {
        file = path.join(file, "index.html");
    }

    send(res, file);
}).listen(PORT, () => console.log(`http://localhost:${PORT}`));
```

Run it:

```bash
cd ~/Desktop/hadad && node server.js
```

The server reads files on every request, so edits to HTML/JS/CSS/JSON only need a browser refresh. Restart only if you edit `server.js`.

### 5.2 `services/index.html`

```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الخدمات | حداد الرياض</title>
    <link rel="icon" href="/assets/logo.png">
    <link rel="stylesheet" href="/main.css">
    <link rel="stylesheet" href="/components/header/style.css">
    <link rel="stylesheet" href="/components/footer/style.css">
    <link rel="stylesheet" href="/services/style.css">
</head>
<body>
    <div id="header"></div>
    <main id="servicesPage">
        <section id="servicesList" class="services-list-page">
            <div class="services-list-header">
                <span>خدمات حداد الرياض</span>
                <h1>جميع خدماتنا</h1>
                <p>نقدم مجموعة متكاملة من خدمات الحدادة والأعمال المعدنية والساندوتش بانل والزجاج.</p>
            </div>
            <div id="servicesGrid" class="services-grid"></div>
        </section>
        <section id="serviceDetail" class="service-detail-page" hidden></section>
        <section id="serviceNotFound" class="service-not-found" hidden></section>
    </main>
    <div id="footer"></div>
    <script type="module" src="/services/script.js"></script>
</body>
</html>
```

The four containers (`#servicesList`, `#servicesGrid`, `#serviceDetail`, `#serviceNotFound`) must exist. `script.js` fills them.

### 5.3 `services/script.js`

```js
import { initHeader } from "/components/header/script.js";
import { renderList, renderService, renderNotFound } from "/services/template.js";

const DEBUG = new URLSearchParams(location.search).has("debug") || localStorage.getItem("debug") === "1";
const log = (...a) => DEBUG && console.log("%c[services]", "color:#e67e22", ...a);
const $ = s => document.querySelector(s);

const servicesList = $("#servicesList");
const servicesGrid = $("#servicesGrid");
const serviceDetail = $("#serviceDetail");
const serviceNotFound = $("#serviceNotFound");

async function loadComponent(selector, url) {
    const target = $(selector);
    if (!target) return;
    const r = await fetch(url);
    log("component", url, r.status);
    if (!r.ok) throw new Error("Failed to load " + url + " (" + r.status + ")");
    target.innerHTML = await r.text();
}

async function loadServices() {
    const url = "/data/services.json";
    const r = await fetch(url);
    log("fetch", url, r.status);
    if (!r.ok) throw new Error("Failed to load " + url + " (" + r.status + ")");
    const data = await r.json();
    const services = Array.isArray(data) ? data : data.services;
    if (!Array.isArray(services)) throw new Error("services.json must be an array");
    log("services:", services.map(s => s.slug));
    return services;
}

function getServiceSlug() {
    const parts = location.pathname.split("/").filter(Boolean);
    const i = parts.indexOf("services");
    const slug = i === -1 ? null : parts[i + 1] || null;
    log("pathname:", location.pathname, "| slug:", slug);
    return slug ? decodeURIComponent(slug) : null;
}

function findService(services, slug) {
    if (!slug) return null;
    const w = slug.trim().toLowerCase();
    return services.find(s => String(s.slug).trim().toLowerCase() === w) || null;
}

function show(section) {
    if (servicesList) servicesList.hidden = section !== "list";
    if (serviceDetail) serviceDetail.hidden = section !== "detail";
    if (serviceNotFound) serviceNotFound.hidden = section !== "404";
}

function showServicesList(services) {
    show("list");
    if (servicesGrid) servicesGrid.innerHTML = renderList(services);
    document.title = "الخدمات | حداد الرياض";
}

function showServiceDetail(service) {
    show("detail");
    if (serviceDetail) serviceDetail.innerHTML = renderService(service);
    document.title = (service.title || "الخدمة") + " | حداد الرياض";
}

function showNotFound() {
    show("404");
    if (serviceNotFound) serviceNotFound.innerHTML = renderNotFound();
    document.title = "404 | حداد الرياض";
}

async function init() {
    try {
        log("page:", location.href, "| has #servicesList:", !!servicesList);
        await loadComponent("#header", "/components/header/index.html");
        initHeader();
        await loadComponent("#footer", "/components/footer/index.html");

        const services = await loadServices();
        const slug = getServiceSlug();

        if (!slug) return showServicesList(services);

        const service = findService(services, slug);
        log("route: DETAIL", slug, service ? "FOUND" : "NOT FOUND");
        if (!service) return showNotFound();
        showServiceDetail(service);
    } catch (error) {
        console.error("Services initialization failed:", error);
        showNotFound();
    }
}

if (document.readyState === "loading") {
    document.addEventListener("DOMContentLoaded", init);
} else {
    init();
}
```

### 5.4 `services/template.js`

```js
// Note: written without the ?? operator on purpose (see Troubleshooting #1)
const esc = value => {
    if (value === null || value === undefined) value = "";
    return String(value)
        .replace(/&/g, "&amp;")
        .replace(/</g, "&lt;")
        .replace(/>/g, "&gt;")
        .replace(/"/g, "&quot;")
        .replace(/'/g, "&#039;");
};

const num = i => String(i + 1).padStart(2, "0");

function getImagePath(image) {
    if (!image) return "";
    if (image.startsWith("/")) return image;
    if (/^https?:\/\//.test(image)) return image;
    if (image.startsWith("../")) return "/" + image.replace(/^(\.\.\/)+/, "");
    if (image.startsWith("./")) return "/" + image.substring(2);
    return "/" + image;
}

export function renderList(services) {
    return services.map((service, index) => {
        const slug = encodeURIComponent(service.slug || "");
        const title = esc(service.title);
        const description = esc(service.heroDescription);
        const image = esc(getImagePath(service.image));
        const alt = esc(service.heroAlt || service.title);

        return `
            <a class="service-card" href="/services/${slug}/">
                <div class="service-card-image">
                    <img src="${image}" alt="${alt}" loading="${index < 3 ? "eager" : "lazy"}">
                </div>
                <div class="service-card-content">
                    <span class="service-card-number">${num(index)}</span>
                    <h2>${title}</h2>
                    <p>${description}</p>
                    <span class="service-card-link">عرض الخدمة ←</span>
                </div>
            </a>
        `;
    }).join("");
}

export function renderService(service) {
    const article = service.article || {};
    const sections = Array.isArray(article.sections) ? article.sections : [];
    const faq = Array.isArray(article.faq) ? article.faq : [];

    const title = service.title || "";
    const description = service.heroDescription || "";
    const image = getImagePath(service.image);
    const alt = service.heroAlt || title;

    const sectionsHtml = sections.map((section, index) => `
        <section class="article-section">
            <div class="article-number">${num(index)}</div>
            <div class="article-section-content">
                <h3>${esc(section.title)}</h3>
                <p>${esc(section.content)}</p>
            </div>
        </section>
    `).join("");

    const faqHtml = faq.length ? `
        <section class="service-faq">
            <div class="faq-heading">
                <span>الأسئلة الشائعة</span>
                <h2>أسئلة عن ${esc(title)}</h2>
            </div>
            <div class="faq-list">
                ${faq.map((item, index) => `
                    <details class="faq-item">
                        <summary>
                            <span>${num(index)}</span>
                            <strong>${esc(item.question)}</strong>
                        </summary>
                        <p>${esc(item.answer)}</p>
                    </details>
                `).join("")}
            </div>
        </section>
    ` : "";

    return `
        <section class="service-hero">
            <div class="service-hero-image">
                <img src="${esc(image)}" alt="${esc(alt)}">
            </div>
            <div class="service-hero-overlay"></div>
            <div class="service-hero-content">
                <span class="service-eyebrow">خدمات حداد الرياض</span>
                <h1>${esc(title)}</h1>
                <p>${esc(description)}</p>
                <div class="service-buttons">
                    <a href="tel:0534107471" class="service-btn service-btn-primary">اتصل بنا</a>
                    <a href="https://wa.me/966534107471" target="_blank" rel="noopener"
                       class="service-btn service-btn-secondary">مراسلتنا</a>
                </div>
            </div>
        </section>

        <section class="service-content">
            <div class="service-layout">
                <aside class="service-sticky">
                    <div class="service-sticky-image">
                        <img src="${esc(image)}" alt="${esc(alt)}">
                    </div>
                    <div class="service-sticky-caption">
                        <span>خدماتنا</span>
                        <strong>${esc(title)}</strong>
                    </div>
                </aside>

                <article class="service-article">
                    <header class="article-header">
                        <span class="article-label">${esc(title)}</span>
                        <h2>${esc(article.introTitle || title)}</h2>
                        <p>${esc(article.intro || description)}</p>
                    </header>

                    ${sectionsHtml}
                    ${faqHtml}

                    <section class="article-cta">
                        <div>
                            <span>تحتاج هذه الخدمة؟</span>
                            <h2>خلنا نعرف تفاصيل مشروعك.</h2>
                            <p>تواصل معنا وأرسل المقاسات أو صور المكان والتفاصيل التي تحتاجها.</p>
                        </div>
                        <div class="article-cta-buttons">
                            <a href="tel:0534107471" class="service-btn service-btn-primary">اتصل بنا</a>
                            <a href="https://wa.me/966534107471" target="_blank" rel="noopener"
                               class="service-btn service-btn-secondary">مراسلتنا</a>
                        </div>
                    </section>
                </article>
            </div>
        </section>
    `;
}

export function renderNotFound() {
    return `
        <span>404</span>
        <h1>الخدمة غير موجودة</h1>
        <p>الخدمة المطلوبة غير موجودة.</p>
        <a href="/services/">العودة إلى الخدمات</a>
    `;
}
```

---

## 6. Everyday Tasks

### Add a new service
1. Put the image in `assets/`.
2. Add an object to `data/services.json` with a unique `slug`.
3. Refresh. It appears on `/services/` and works at `/services/<slug>/`. No new files or folders.

### Edit a service
Edit its object in `data/services.json`. Nothing else changes.

### Change the layout of cards or detail pages
Edit `services/template.js` (HTML) and `services/style.css` (styling).

---

## 7. Debug Mode

Add `?debug=1` to any services URL:

```
http://localhost:5500/services/iron-gates/?debug=1
```

Or enable it permanently from the browser console:

```js
localStorage.setItem("debug", "1")   // on
localStorage.removeItem("debug")     // off
```

Console output (orange `[services]` prefix) shows:

- the page URL and whether `#servicesList` exists
- each component fetch and its HTTP status
- the `services.json` fetch status and the list of slugs
- the pathname and detected slug
- whether the route resolved to LIST, DETAIL FOUND, or DETAIL NOT FOUND

---

## 8. Troubleshooting (issues we actually hit)

| # | Symptom | Cause | Fix |
|---|---|---|---|
| 1 | `SyntaxError: expected expression, got '?'` in `template.js` | A formatter split `??` into `? ?` | `sed -i 's/? ?/??/g' services/template.js`, or avoid `??` (as in the current `esc`). Also disable format-on-save or use Prettier. |
| 2 | Every service page 404s | `fetch("../data/services.json")` resolves to `/services/data/...` | Use absolute `/data/services.json` |
| 3 | `/services/iron-gates/` 404s on port 5500 | Live Server cannot rewrite URLs | Run `node server.js` instead |
| 4 | `servicesList is null` | `services/index.html` lacked the four containers | Restore `index.html` from section 5.2 |
| 5 | `NetworkError when attempting to fetch` | Server restarted or wrong origin/port | Check the port, hard refresh, use `?debug=1` to see which URL failed |
| 6 | Shell `parse error near '\n'` when pasting | A stray `</parameter>` tag and zsh multi-line paste handling | Type `bash` first, or write files from your editor |
| 7 | `favicon.ico` 404 | No icon declared | `<link rel="icon" href="/assets/logo.png">` in each page head (harmless otherwise) |
| 8 | Page shows the shell but empty | Script crashed | Open DevTools console, add `?debug=1` |

Tip: after changing JS, hard refresh with `Ctrl+Shift+R` so the browser doesn't use a cached module.

---

## 9. Deployment (the rewrite must exist in production too)

`server.js` is for local development. On a real host, add the same rule: **`/services/<slug>` returns `/services/index.html`**.

**Nginx**
```nginx
location ~ ^/services/[^/.]+/?$ {
    try_files /services/index.html =404;
}
```

**Apache (`.htaccess`)**
```apache
RewriteEngine On
RewriteRule ^services/[^/.]+/?$ /services/index.html [L]
```

**Netlify (`_redirects`)**
```
/services/*  /services/index.html  200
```

**Vercel (`vercel.json`)**
```json
{ "rewrites": [{ "source": "/services/:slug", "destination": "/services/index.html" }] }
```

**GitHub Pages** has no rewrites. Use a `404.html` fallback or switch to the query-string form (`/services/?s=iron-gates`), which needs a small change in `getServiceSlug()` and the card links.

---

## 10. Notes and Possible Improvements

- **SEO:** the title is set from JavaScript, and the content is rendered client-side. Search engines generally handle this, but for best results consider pre-rendering each service into static HTML at build time, and adding `<meta name="description">` and canonical tags per service.
- **Unknown slugs** show the in-page 404 block but the HTTP status is still 200, since the server serves the same shell. A real server could check the slug and return 404.
- **Other sections** (`about`, `contact`, `projects`, `articles`) follow the same pattern: folder + `index.html` + `script.js` + `style.css`, with data in `/data/*.json`.
- **Security:** all JSON text goes through `esc()` before entering HTML, so content in the JSON can't inject markup.
