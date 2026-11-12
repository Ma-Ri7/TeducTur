# MIGRARE PE DOMENIUL OFICIAL — CHECKLIST SEO

Document operațional pentru lansare. **Nimic din acest document nu a fost aplicat automat** (domeniul final nu este cunoscut).

---

## 1. Starea actuală a mediului demo

| Element | Stare |
|---|---|
| URL demo | `https://demo.mrwebsites.ro/teduc-tur/` |
| Indexare | `meta robots = noindex, nofollow` pe toate cele 11 pagini — **păstrat intenționat** |
| Canonical | relativ, auto-referențial (`href="index.html"`) |
| `og:image` | relativ (ex. `_astro/hero-sprinter-rosu...webp`) |
| `og:url` | **absent** (ar necesita domeniul final) |
| `robots.txt` | **nu există** |
| `sitemap.xml` | **nu există** |
| Referințe la domeniul demo | doar în `href`-urile de share (Facebook/WhatsApp) de pe 6 pagini — **rescrise runtime** din `location.href`; valoarea demo rămâne fallback fără JS |

## 2. Pași la lansarea pe domeniul oficial

### Pasul 1 — Elimină `noindex`

În toate cele 11 fișiere HTML, șterge linia:

```html
<!-- Demo de prezentare: nu se indexează până la lansare. TODO(real): scos la lansare. -->
<meta name="robots" content="noindex, nofollow">
```

Verificare: `grep -rl 'noindex' --include='*.html' .` → niciun rezultat.

### Pasul 2 — Absolutizează canonical (recomandat, opțional)

Canonical-ul relativ funcționează corect pe orice domeniu. Pentru maximă claritate (și pentru a elimina orice dublet `.../index.html` vs `.../`), înlocuiește în fiecare pagină:

```html
<link rel="canonical" href="index.html">
```

cu URL-ul absolut al variantei alese, ex.:

```html
<link rel="canonical" href="https://DOMENIU.ro/servicii/curse-regulate-speciale/">
```

**Atenție:** dacă alegi varianta fără `index.html`, asigură-te că serverul servește `/servicii/curse-regulate-speciale/` și că varianta cu `index.html` face 301 către ea (sau invers), ca să nu existe două URL-uri indexabile pentru aceeași pagină.

### Pasul 3 — Adaugă `og:url` și absolutizează `og:image` / `twitter:image`

```html
<meta property="og:url" content="https://DOMENIU.ro/calea/paginii/">
<meta property="og:image" content="https://DOMENIU.ro/_astro/hero-sprinter-rosu.BWNIlai4_ZRkWb5.webp">
<meta name="twitter:image" content="https://DOMENIU.ro/_astro/hero-sprinter-rosu.BWNIlai4_ZRkWb5.webp">
```

(Facebook și alte platforme nu rezolvă `og:image` relativ.)

### Pasul 4 — Creează `robots.txt` în rădăcina domeniului

```
User-agent: *
Allow: /

Sitemap: https://DOMENIU.ro/sitemap.xml
```

> Nu folosi `Disallow: /` „ca să nu se indexeze demo-ul”: blochează crawl-ul și `noindex`-ul nu mai este citit. Pentru demo, `noindex` din meta este suficient și corect.

### Pasul 5 — Generează `sitemap.xml`

Toate cele 11 URL-uri, `lastmod` = data lansării, `changefreq`/`priority` opționale:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url><loc>https://DOMENIU.ro/</loc><lastmod>2026-11-12</lastmod></url>
  <url><loc>https://DOMENIU.ro/servicii/</loc><lastmod>2026-11-12</lastmod></url>
  <url><loc>https://DOMENIU.ro/servicii/curse-regulate-speciale/</loc><lastmod>2026-11-12</lastmod></url>
  <url><loc>https://DOMENIU.ro/servicii/curse-ocazionale/</loc><lastmod>2026-11-12</lastmod></url>
  <url><loc>https://DOMENIU.ro/servicii/transport-special/</loc><lastmod>2026-11-12</lastmod></url>
  <url><loc>https://DOMENIU.ro/servicii/transfer-aeroport/</loc><lastmod>2026-11-12</lastmod></url>
  <url><loc>https://DOMENIU.ro/servicii/servicii-aeroport/</loc><lastmod>2026-11-12</lastmod></url>
  <url><loc>https://DOMENIU.ro/servicii/evenimente/</loc><lastmod>2026-11-12</lastmod></url>
  <url><loc>https://DOMENIU.ro/flota/</loc><lastmod>2026-11-12</lastmod></url>
  <url><loc>https://DOMENIU.ro/despre-noi/</loc><lastmod>2026-11-12</lastmod></url>
  <url><loc>https://DOMENIU.ro/contact/</loc><lastmod>2026-11-12</lastmod></url>
</urlset>
```

### Pasul 6 — Adaugă `url` în JSON-LD (opțional dar recomandat)

În `LocalBusiness` (pagina Acasă) și `WebSite`, adaugă:

```json
"url": "https://DOMENIU.ro/",
"image": "https://DOMENIU.ro/_astro/hero-sprinter-rosu.BWNIlai4_ZRkWb5.webp"
```

Iar în `BreadcrumbList`, absolutizează `item`-urile (Google preferă URL-uri absolute pentru rich results):

```
"item": "https://DOMENIU.ro/servicii/curse-regulate-speciale/"
```

### Pasul 7 — Google Search Console

1. Verifică proprietatea domeniului.
2. Trimite `sitemap.xml`.
3. Inspecție URL pentru cele 11 pagini → „Request indexing”.
4. Monitorizează: Acoperire (pagini indexate), Performanță (query-uri), Core Web Vitals.

### Pasul 8 — Validatoare

| Test | URL |
|---|---|
| Date structurate | `https://validator.schema.org/` |
| Rich Results | `https://search.google.com/test/rich-results` |
| Core Web Vitals | `https://pagespeed.web.dev/` |
| Open Graph | `https://developers.facebook.com/tools/debug/` |

## 3. Verificare post-lansare (checklist rapid)

- [ ] `https://DOMENIU.ro/robots.txt` răspunde 200 și conține `Sitemap:`
- [ ] `https://DOMENIU.ro/sitemap.xml` răspunde 200, conține 11 URL-uri
- [ ] `noindex` eliminat din toate paginile
- [ ] Title/description apar corect în SERP (fără dubluri)
- [ ] `/servicii/` și `/servicii/index.html` nu returnează ambele 200 (301 pe una)
- [ ] Imaginea din `og:image` se încarcă în Facebook Debugger
- [ ] Linkurile `tel:` funcționează pe mobil
- [ ] Linkurile WhatsApp funcționează
- [ ] Formularul „Cere ofertă” deschide WhatsApp cu câmpurile completate
- [ ] Lighthouse mobil: fără erori de accesibilitate introduse, LCP pe imaginea hero
