# SEO TECHNICAL CHECKS — TEDUC TUR

Toate verificările de mai jos au fost **executate efectiv** pe fișierele finale, cu server local (`python3 -m http.server`) și Chrome headless (CDP), plus scripturi Python de validare.

---

## 1. Verificări SEO automate

| # | Verificare | Metodă | Rezultat |
|---|---|---|---|
| 1 | Title unic pe fiecare pagină | extragere `<title>` + comparație | **PASS** — 11/11 unice, 52–62 caractere |
| 2 | Meta description unică | extragere `meta[name=description]` + comparație | **PASS** — 11/11 unice, 143–157 caractere |
| 3 | Title / description ne-goale | verificare lungime | **PASS** — 0 goale |
| 4 | Exact un H1 per pagină | numărare `<h1>` | **PASS** — 1/1 pe toate paginile |
| 5 | Ierarhie H1→H2→H3 | inspecție structură | **PASS** — H2 3–7, H3 0–6, fără sărituri de nivel în conținutul nou |
| 6 | Canonical prezent și corect | `link[rel=canonical]` + rezolvare URL în browser | **PASS** — 11/11; rezolvat corect la `/servicii/curse-regulate-speciale/index.html` (fără query string) |
| 7 | Open Graph + Twitter | numărare meta | **PASS** — 6 OG + 4 Twitter per pagină |
| 8 | Robots meta nemodificat | comparație cu backup | **PASS** — `noindex, nofollow` pe 11/11 (intenționat, mediu demo) |
| 9 | JSON-LD valid | `json.loads()` pe fiecare bloc | **PASS** — 11 blocuri, 0 erori de parsare |
| 10 | Tipuri schema.org corecte | inspecție `@type` | **PASS** — LocalBusiness, WebSite, BreadcrumbList, Service, CollectionPage, ItemList, AboutPage, ContactPage |
| 11 | ALT-uri imagini | numărare `alt` goale vs completate | **PASS** — 57/152 completate; restul sunt decorative (`alt=""` justificat) |
| 12 | Linkuri interne valide | 777 referințe (`href`, `src`, `srcset`) verificate | **PASS** — 0 lipsă |
| 13 | Tag-uri HTML echilibrate | parser propriu (`html.parser`) | **PASS** — 11/11 fără tag-uri neînchise |
| 14 | Clase CSS existente | fiecare clasă folosită căutată în CSS-ul compilat (415 clase distincte) | **PASS** — 0 clase inexistente |
| 15 | Ancore interne | `#cerere-oferta`, `#continut` | **PASS** — țintele există (`FORM`, `MAIN`) |
| 16 | Duplicare meta între sisteme | inspecție `<head>` | **PASS** — un singur set de meta, scris manual, fără duplicate |

## 2. Verificări tehnice / funcționale (browser real)

| # | Verificare | Metodă | Rezultat |
|---|---|---|---|
| 1 | Erori / warning-uri JavaScript | CDP `Log.entryAdded` + `Runtime.exceptionThrown`, 11 pagini × 2 viewport-uri | **PASS** — 0 erori, 0 warning-uri |
| 2 | Overflow orizontal (mobile) | `scrollWidth` vs `clientWidth`, viewport 390/900/1440 | **PASS** — egale pe toate paginile |
| 3 | H1 încadrat în banda hero | `getBoundingClientRect` H1 vs secțiune | **PASS** — spațiu rămas 86–3005 px pe toate paginile/viewport-urile |
| 4 | Meniu mobil (hamburger) | click programatic pe `[data-meniu-buton]` | **PASS** — `aria-expanded: false → true`, meniu vizibil (647 px) |
| 5 | Galerie foto (săgeți) | click pe `[data-inainte]` | **PASS** — contor `1 / 4 → 2 / 4`, slide activ corect |
| 6 | Formular cerere ofertă | inspecție DOM | **PASS** — 10 câmpuri, buton submit, fără `action` (se trimite în WhatsApp prin JS) — **nemodificat** |
| 7 | Linkuri `tel:` | numărare + valoare | **PASS** — `tel:+40770859339` pe toate paginile (3–4 instanțe) |
| 8 | Linkuri WhatsApp | inspecție href | **PASS** — `https://wa.me/40770859339?text=...` funcțional |
| 9 | Linkuri de distribuire socială | evaluare runtime după scriptul nou | **PASS** — rescrise pe URL-ul curent (`...?u=http%3A%2F%2F127.0.0.1%3A8765%2F...`); domeniul demo nu mai este folosit |
| 10 | Imagine hero încărcată | `img.complete` + `naturalWidth` | **PASS** — varianta mobilă corectă (`hero-sprinter-rosu-mobil..._2fcgqY.webp`) |
| 11 | Factori Core Web Vitals controlabili | `loading`, `fetchpriority`, `width/height`, `sizes` | **PASS** — hero `eager` + `fetchpriority=high`, restul `lazy`; dimensiuni explicite (fără CLS) |

## 3. Verificări de integritate (design & conținut)

| # | Verificare | Metodă | Rezultat |
|---|---|---|---|
| 1 | Design neschimbat | comparație pixel-cu-pixel înainte/după (ImageMagick `compare -metric AE`), 390 px și 1440 px | **PASS** — pagina Contact: **0 pixeli diferiți** (singurele modificări au fost meta); celelalte pagini diferă **exclusiv** în zona H1 / a secțiunilor noi (bounding-box verificat) |
| 2 | Secțiune nouă integrată vizual | măsurare stiluri calculate | **PASS** — H2 42px/52.5px uppercase `Inter`, H3 22px/29px uppercase, linkuri 16px/30px culoare `#1c1c1c` = exact stilurile existente |
| 3 | Spațiere corectă în secțiunea nouă | măsurare gap-uri | **PASS** — gap coloane 48 px (mobil) / 40 px (desktop), 50 px înainte de paragraful final, padding-bottom 100 px |
| 4 | Fără suprapunere coloane | geometrie stânga/dreapta | **PASS** — coloana 1: 130–700 px, coloana 2: 740–1310 px (40 px între) |
| 5 | CSS / JS / imagini / fonturi neatinse | hash SHA-256 pe tot directorul `_astro/` vs backup | **PASS** — identice 100% |
| 6 | Fișiere modificate | hash pe toate fișierele | **PASS** — doar cele **11 fișiere HTML**; `favicon.svg` neschimbat |
| 7 | Pagini șterse / URL-uri schimbate | inventar fișiere + linkuri | **PASS** — 11/11 pagini prezente, toate URL-urile identice |
| 8 | Date de contact nemodificate | comparație șiruri | **PASS** — telefon, e-mail, localitate, administrator identice |
| 9 | Formulare nemodificate | comparație HTML formular | **PASS** — identice |
| 10 | Fotografii nemodificate | hash fișiere imagine | **PASS** — 0 imagini modificate/șterse |

> **Observație de proces:** în timpul implementării au fost detectate și corectate 5 clase Tailwind inexistente în CSS-ul compilat (`gap-[50px]`, `md:gap-[50px]`, `md:pb-[80px]`, `space-y-2`, `max-w-[700px]`). Au fost înlocuite cu echivalente existente (`gap-12`, `md:gap-[40px]`, `pb-[100px]`, `space-y-2.5`, `max-w-[900px]`). Verificarea finală: **0 clase fără CSS**.

## 4. Comenzi / unelte folosite (reproductibile)

```bash
# server local
python3 -m http.server 8765

# validare meta + JSON-LD + ALT + linkuri + tag balance
python3 verify.py            # 11 pagini, 777 referințe

# existența claselor Tailwind în CSS-ul compilat
python3 classcheck.py        # 415 clase distincte → 0 lipsă

# capturi + erori JS + metrici layout (Chrome headless + CDP)
node shot.mjs                # 11 pagini × 2 viewport-uri, Log + exceptions
node layout.mjs              # 11 pagini × 3 viewport-uri (390/900/1440)
node interactions.mjs        # meniu mobil, galerie, formular, tel/wa

# comparație vizuală înainte/după
compare -metric AE shots/before/x.png shots/after/x.png null:
magick before.png after.png -compose difference -composite -trim info:
```

## 5. Ce NU a putut fi verificat (limitări de mediu)

| Element | Motiv | Recomandare |
|---|---|---|
| Poziții / randare în Google | mediu demo cu `noindex`; fără acces la Search Console | după lansare: GSC + Rich Results Test |
| Rich Results (breadcrumb, LocalBusiness) | necesită URL-uri absolute și indexare | la lansare: `validator.schema.org` + Rich Results Test |
| Core Web Vitals reale (LCP/INP/CLS) | necesită trafic real / CrUX | PageSpeed Insights după lansare |
| `robots.txt` / `sitemap.xml` live | domeniu necunoscut | template în `MIGRARE_DOMENIU_CHECKLIST.md` |
| Redirectări | fără acces la configurația serverului | de stabilit la migrare (canonical + varianta de URL) |
