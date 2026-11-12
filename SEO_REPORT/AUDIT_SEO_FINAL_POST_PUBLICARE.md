# AUDIT SEO FINAL POST-PUBLICARE — TEDUC TUR

**Data:** 12 noiembrie 2026
**Domeniu:** `https://teductur.eu`
**Stadiu:** audit **read-only** (fără modificări, fără commit/push/deploy). Bazat pe verificări live (HTTP) + analiza fișierelor locale (byte-identice cu cele publicate, confirmat prin SHA-256).

---

## Verdict

**SUCCESS** — SEO tehnic și on-page sunt în stare bună: cele 11 pagini sunt live (`200`), cu title/description unice, un singur H1, canonical absolut corect, `noindex` eliminat, `robots.txt` + `sitemap.xml` funcționale, JSON-LD valid și onest (fără date inventate), iar resursele CSS/JS/imagini/fonturi se publică corect. Rămân doar câteva probleme minore, neblocante (listate la §5).

> Notă importantă: **indexarea efectivă în Google** nu poate fi confirmată din acest audit (necesită Google Search Console și timp de recrawling) — vezi §8.

---

## 1. Tabel — cele 11 pagini

| Pagină | HTTP | Title (len) | Desc (len) | H1 | H2/H3 | Canonical absolut | noindex | OG/Tw |
|---|---|---|---|---|---|---|---|---|
| `/` | 200 | Transport persoane Huedin – microbuze și autocar (60) | 157 | 1 | 6/6 | `…/` | ✗ lipsă | 7/4 |
| `/servicii/` | 200 | Servicii de transport persoane în Huedin și Cluj (60) | 143 | 1 | 4/0 | `…/servicii/` | ✗ | 7/4 |
| `/servicii/curse-regulate-speciale/` | 200 | Transport angajați Cluj și Huedin – curse regulate (62) | 148 | 1 | 7/4 | corect | ✗ | 7/4 |
| `/servicii/curse-ocazionale/` | 200 | Închiriere microbuz cu șofer – excursii și grupuri (62) | 152 | 1 | 7/4 | corect | ✗ | 7/4 |
| `/servicii/transport-special/` | 200 | Transport persoane la comandă, Huedin – Cluj (56) | 157 | 1 | 7/4 | corect | ✗ | 7/4 |
| `/servicii/transfer-aeroport/` | 200 | Transfer aeroport Cluj din Huedin și Oradea (55) | 146 | 1 | 7/4 | corect | ✗ | 7/4 |
| `/servicii/servicii-aeroport/` | 200 | Asistență la aeroport Cluj: sosiri și bagaje (56) | 150 | 1 | 7/4 | corect | ✗ | 7/4 |
| `/servicii/evenimente/` | 200 | Transport persoane la evenimente: nunți, botezuri (61) | 144 | 1 | 7/4 | corect | ✗ | 7/4 |
| `/flota/` | 200 | Închiriere microbuze cu șofer, Huedin–Cluj (54) | 153 | 1 | 3/4 | `…/flota/` | ✗ | 7/4 |
| `/despre-noi/` | 200 | Despre Teduc Tur – firmă de transport persoane Huedin (53) | 152 | 1 | 6/3 | `…/despre-noi/` | ✗ | 7/4 |
| `/contact/` | 200 | Contact Teduc Tur – ofertă transport persoane Huedin (52) | 146 | 1 | 4/1 | `…/contact/` | ✗ | 7/4 |

- **Title-uri:** 11/11 unice, 52–62 caractere (SERP-safe) ✅
- **Descriptions:** 11/11 unice, 143–157 caractere ✅
- **H1:** exact 1 pe fiecare pagină ✅
- **Ierarhie H2/H3:** corectă, fără salturi ✅
- **`noindex`:** eliminat de pe toate paginile ✅
- **OG/Twitter:** 7 meta OG + 4 meta Twitter per pagină ✅
- **ALT:** 86 imagini de conținut au `alt` descriptiv; 76 decorative au `alt` gol (bare `alt`), ceea ce este corect pentru imagini decorative ✅
- **Linkuri interne:** 1094 referințe interne verificate → **0 defecte** ✅

## 2. SEO tehnic

| Verificare | Rezultat |
|---|---|
| `robots.txt` | `200` — `User-agent: * / Allow: /` + `Sitemap: https://teductur.eu/sitemap.xml` ✅ |
| `sitemap.xml` | `200` — **11** `<loc>`, toate `200` ✅ |
| Concordanță sitemap ↔ canonical | 11 URL-uri identice, formă cu `/` final ✅ |
| Variante `/servicii` (fără slash) | `301 → /servicii/` ✅ |
| Variante `/…/index.html` | `200` (fără `301` către forma canonicală) ⚠️ minor |
| `/index.html` | `200` (fără `301` către `/`) ⚠️ minor |
| CSS / JS / WebP / WOFF2 | `200` cu `text/css` / `application/javascript` / `image/webp` / `font/woff2` ✅ |
| HTTPS + www | `https://www.teductur.eu/` → `301 → https://teductur.eu/` ✅ |
| HTTP→HTTPS | `http://teductur.eu/` → `200` direct (fără `301`); header HSTS nu a fost observat ⚠️ minor |

## 3. Date structurate (JSON-LD)

- **Validitate:** 11 blocuri JSON-LD, **0 erori de parsare** ✅
- **Tipuri Schema.org:** `LocalBusiness`, `WebSite`, `BreadcrumbList`, `ListItem`, `Service`, `CollectionPage`, `ItemList`, `AboutPage`, `ContactPage`, `Person`, `PostalAddress`, `City`, `AdministrativeArea` ✅
- **Date firme (LocalBusiness):** `name` S.C. Teduc Tur S.R.L., `alternateName` Teduc Tur, `telephone` +40770859339, `email` teductur@gmail.com, `foundingDate` 2019, `founder` Radu Neag, `address` Huedin/Cluj/RO, `areaServed` (Huedin, Cluj-Napoca, Ciucea, Poieni, Sâncraiu, Călățele, Izvorul Crișului, Beliș, Oradea, județul Cluj), `knowsLanguage` ro, `url` https://teductur.eu/, `image` hero. **Toate reale, preluate din site** ✅
- **Concordanță schema ↔ conținut vizibil:** telefon/e-mail/localitate/servicii coincid cu textele și footer-ul ✅
- **Fără date inventate:** absente `review`, `aggregateRating`, `ratingValue`, `priceRange`, `openingHoursSpecification`, `geo`, `sameAs` — corect, nu au fost inventate recenzii/ratinguri ✅
- **Omitere justificată:** `streetAddress`/`geo` (nu există adresă stradală publică în site) și `sameAs` (linkul Facebook e generic, nu o pagină reală) ✅

## 4. Conținut și SEO local

- **Relevanță transport persoane Huedin:** titlurile/H1/descrierile acoperă „transport persoane", „microbuz/autocar", „Huedin" pe paginile de top ✅
- **Arie acoperită:** Cluj-Napoca, județul Cluj, Valea Crișului și satele din jur (Ciucea, Poieni, Sâncraiu, Călățele, Izvorul Crișului, Beliș), plus Oradea pentru transfer aeroport ✅
- **Servicii B2C și B2B:** ambele acoperite — secțiunea „Cu cine lucrăm" (persoane fizice vs companii/instituții) + pagini dedicate (curse regulate B2B; ocazionale/evenimente/transfer B2C) ✅
- **Distribuția cuvintelor-cheie:** mapare dedicată există (`SEO_REPORT/KEYWORD_MAPPING.md`); fiecare pagină are expresie-țintă proprie, fără duplicare de title/description ✅
- **Suprapunere intenție:** `transfer-aeroport` (drumul către aeroport) vs `servicii-aeroport` (asistență la terminal) — intenții distincte, diferențiate prin titlu/descriere/H1 și legate între ele (suprapunere controlată, nu canibalizare) ✅
- **Oportunități (fără a inventa):** adăugarea `streetAddress`/`geo`/`openingHoursSpecification` și `sameAs` doar dacă devin disponibile date reale; eventual o secțiune FAQ locală doar dacă există întrebări reale frecvente. Nu se recomandă adăugarea de servicii/ratinguri inexistente.

## 5. Probleme confirmate (minore, neblocante)

1. **Duplicate de URL:** `/index.html`, `/servicii/index.html` (și celelalte `…/index.html`) returnează `200` fără `301` către forma canonicală cu `/` final. Canonicalele indică forma cu `/`, deci riscul e atenuat, dar ideal ar fi un redirect 301 (necesită decizie/cfg care nu se poate face direct din repo pentru „Deploy from a branch").
2. **HTTP fără redirect către HTTPS:** `http://teductur.eu/` răspunde `200` (nu `301`), iar în răspunsul testat nu apare header `Strict-Transport-Security`. Atribuit infrastructurii GitHub Pages (apex prin A-record). Canonical + sitemap indică `https://`, deci impact SEO redus.
3. **`SEO_REPORT/*.md` publicat ca HTML:** Jekyll convertește rapoartele `.md` în pagini HTML accesibile public (ex. `/SEO_REPORT/SEO_TECHNICAL_CHECKS` → `200`). Preexistent (nu din fix-ul `_config.yml`); se poate opțional exclude via `exclude:` în `_config.yml`.

## 6. Recomandări prioritizate

| # | Recomandare | Prioritate | Tip |
|---|---|---|---|
| 1 | Submit `sitemap.xml` + „Request indexing" pentru cele 11 URL în Google Search Console | **Ridicată** | indexare |
| 2 | Decideți o singură formă de URL (recomandat `/`, cu slash final) și configurați 301 pentru variantele `…/index.html` | Medie | tehnic |
| 3 | (Opțional) `exclude` pentru `SEO_REPORT/` în `_config.yml`, dacă nu doriți rapoartele publice | Joasă | confidențialitate |
| 4 | Rulați validatoarele externe (Rich Results, Facebook Sharing Debugger) pentru confirmarea datelor structurate/OG | Medie | validare |
| 5 | Când există date reale: adăugați `streetAddress`, `geo`, `openingHoursSpecification`, `sameAs` la LocalBusiness | Joasă | schema |

## 7. Verificări care NU au putut fi efectuate

- **Indexarea efectivă în Google** (Acoperire/query-uri) — necesită Google Search Console + recrawling.
- **Core Web Vitals reale (LCP/INP/CLS)** — necesită PageSpeed Insights / date CrUX; nu am declarat scoruri fără măsurători.
- **Rich Results / validare schema.org pe URL live** — necesită rulearea instrumentelor externe (am validat doar sintaxa JSON și corectitudinea datelor).

## 8. Diferența: SEO tehnic / on-page / indexare efectivă

- **SEO on-page** = conținut, title, description, H1, alt, JSON-LD → ✅ optimizat și verificat (acest audit).
- **SEO tehnic** = robots, sitemap, canonical, redirectări, HTTPS, resurse statice → ✅ în mare parte corect; 2–3 iteme minore rămase (§5).
- **Indexare efectivă** = prezența reală în Google → ❓ **neconfirmabilă de aici**. `noindex` a fost eliminat recent, iar indexarea depinde de recrawling și de trimiterea sitemap-ului în GSC. Aceasta este limita reală a auditului, nu o defecțiune a site-ului.

## 9. Performanță (observații, fără scoruri CWV)

- **Imagini:** 82 fișiere WebP, total 5.78 MB; max 279 KB, hero 257 KB — rezonabil; variante responsive via `srcset` (240–900w) ✅
- **Încărcare:** hero `loading="eager"` + `fetchpriority="high"`, restul `loading="lazy"`; `width`/`height` prezente (fără schimb de layout/CLS) ✅
- **Fonturi:** 7 subseturi `woff2` Inter (latin/latin-ext/cyrillic/greek/vietnamese), încărcate după `unicode-range` (doar subseturile necesare) ✅
- **Randare:** un singur CSS (`39 KB`, blocant la primul paint — normal); JS `type="module"` (deferit, neblocant) ✅
- Nu am identificat probleme evidente de performanță.