# CHANGELOG — OPTIMIZARE SEO ON-PAGE

**Data:** 12 noiembrie 2026
**Total fișiere modificate:** 11 (toate HTML) + 6 fișiere de raportare noi în `SEO_REPORT/`
**Fișiere CSS / JS / imagini / fonturi modificate:** **0**

---

## 1. Modificări partajate (aceleași pe toate cele 11 pagini)

| Zonă | Modificare | Motiv |
|---|---|---|
| `<title>` | Înlocuit cu title unic, 52–62 caractere, cuvânt-cheie principal + localizare | Titluri vechi de 35–47 caractere, generice, fără expresie comercială |
| `<meta name="description">` | Înlocuită cu descriere unică, 143–157 caractere | 5 descrieri duplicate + 4 descrieri de 209–330 caractere |
| `<head>` | Adăugat `<link rel="canonical" href="index.html">` (relativ, auto-referențial) | Lipsea complet; varianta relativă evită hardcodarea unui domeniu necunoscut |
| `<head>` | 6 meta Open Graph (`og:type`, `og:site_name`, `og:locale`, `og:title`, `og:description`, `og:image`) | Lipseau complet |
| `<head>` | 4 meta Twitter (`card`, `title`, `description`, `image`) | Lipseau complet |
| `<head>` | Comentariu `TODO(lansare)` cu pașii de la migrare | Să nu se piardă pașii de lansare |
| `<head>` | 1 bloc `<script type="application/ld+json">` | 0 date structurate înainte |
| `<meta name="robots">` | **Nemodificat** (`noindex, nofollow`) | Mediu demo — fără aprobare nu se schimbă indexarea |

## 2. Modificări per fișier

### `index.html`

| Modificare | Detaliu | Motiv |
|---|---|---|
| Title + description | Noi, unice | SEO |
| OG / Twitter / canonical | Adăugate (`og:image` = hero) | SEO tehnic |
| JSON-LD | `LocalBusiness` + `WebSite` | SEO local + brand |
| **Secțiune nouă** „[ Cu cine lucrăm ]” | H2 + 2×H3 + paragraf intro + 8 linkuri descriptive + paragraf SEO local | Lipsa conținutului B2C/B2B și a semnalelor locale |
| ALT | +6 (tile-urile din grila de servicii) | Imagini de conținut fără descriere |
| Spațiere | `pb-[100px] pt-[70px] md:pt-[90px]`, grid `gap-12 md:grid-cols-2 md:gap-[40px]` | Integrare în ritmul vizual existent (după corectarea claselor inexistente în CSS) |

### `servicii/index.html`

| Modificare | Detaliu |
|---|---|
| Title + description | Noi, unice (eliminată duplicarea) |
| H1 | „Servicii” → „Servicii de transport persoane” |
| Conținut | Paragraf B2C/B2B + „Vezi și” (Flotă, Contact) |
| ALT | +6 (grila de servicii) |
| JSON-LD | `BreadcrumbList` + `CollectionPage` + `ItemList` |

### `servicii/curse-regulate-speciale/index.html`

| Modificare | Detaliu |
|---|---|
| Title + description | „Transport angajați Cluj și Huedin – curse regulate” / 148 caractere (era 330) |
| H1 | → „Curse regulate speciale pentru angajați” |
| Conținut | Paragraf contract/facturare + „Vezi și” (Flotă, Contact) |
| JSON-LD | `BreadcrumbList` + `Service` |
| Script inline | Share links recalculate din `location.href` |

### `servicii/curse-ocazionale/index.html`

| Modificare | Detaliu |
|---|---|
| Title + description | „Închiriere microbuz cu șofer – excursii și grupuri” |
| H1 | → „Închiriere microbuz cu șofer” |
| Conținut | Paragraf șofer/preț + „Vezi și” (Flotă, Contact) |
| JSON-LD | `BreadcrumbList` + `Service` |
| Script inline | Share links dinamice |

### `servicii/transport-special/index.html`

| Modificare | Detaliu |
|---|---|
| Title + description | „Transport persoane la comandă, Huedin – Cluj” |
| H1 | → „Transport persoane la comandă” |
| Conținut | Paragraf preluare/adresă + „Vezi și” (Flotă, Contact) |
| JSON-LD | `BreadcrumbList` + `Service` |
| Script inline | Share links dinamice |

### `servicii/transfer-aeroport/index.html`

| Modificare | Detaliu |
|---|---|
| Title + description | „Transfer aeroport Cluj din Huedin și Oradea” / 146 caractere (era 274) |
| H1 | → „Transfer aeroport Cluj din Huedin” |
| Conținut | Paragraf localități de preluare + curse de noapte + „Vezi și” (Flotă, Contact) |
| JSON-LD | `BreadcrumbList` + `Service` |
| Script inline | Share links dinamice |

### `servicii/servicii-aeroport/index.html`

| Modificare | Detaliu |
|---|---|
| Title + description | „Asistență la aeroport Cluj: sosiri și bagaje” — diferențiere clară de Transfer aeroport |
| H1 | → „Servicii aeroport Cluj” |
| Conținut | Paragraf combinare asistență + transfer + „Vezi și” (**Transfer aeroport**, Contact) |
| JSON-LD | `BreadcrumbList` + `Service` |
| Script inline | Share links dinamice |

### `servicii/evenimente/index.html`

| Modificare | Detaliu |
|---|---|
| Title + description | „Transport persoane la evenimente: nunți, botezuri” / 144 (era 127) |
| H1 | → „Transport persoane la evenimente” |
| Conținut | Paragraf planificare curse + „Vezi și” (**Curse ocazionale**, Contact) |
| JSON-LD | `BreadcrumbList` + `Service` |
| Script inline | Share links dinamice |

### `flota/index.html`

| Modificare | Detaliu |
|---|---|
| Title + description | „Închiriere microbuze cu șofer, Huedin–Cluj” / descriere cu capacitățile reale |
| H1 | „Flota” → „Închiriere microbuze cu șofer” |
| Conținut | Paragraf alegere vehicul + dotări + „Vezi și” (3 servicii + Contact) — pagina avea 74 cuvinte |
| JSON-LD | `BreadcrumbList` + `CollectionPage` |

### `despre-noi/index.html`

| Modificare | Detaliu |
|---|---|
| Title + description | „Despre Teduc Tur – firmă de transport persoane Huedin” |
| H1 | „Despre noi” → „Firmă de transport persoane în Huedin” |
| JSON-LD | `BreadcrumbList` + `AboutPage` |
| Conținut comercial | **Neatins** (valori, echipă, parc auto, imagini) |

### `contact/index.html`

| Modificare | Detaliu |
|---|---|
| Title + description | „Contact Teduc Tur – ofertă transport persoane Huedin” |
| H1 | **Nemodificat** („Contact”) |
| JSON-LD | `BreadcrumbList` + `ContactPage` |
| Formular / date de contact | **Neatinse** |

## 3. Note pentru rebuild (important)

Build-ul Astro a fost modificat **direct în HTML**. La o regenerare din sursă, modificările se pierd dacă nu sunt replicate în componente. Mapare orientativă:

| Modificare | Unde trebuie replicată în sursa Astro |
|---|---|
| Title/description per pagină | frontmatter/props ale fiecărei pagini + `Layout.astro` |
| Canonical / OG / Twitter | `Layout.astro` (head), canonical derivat din `Astro.url.pathname` |
| JSON-LD | componentă dedicată (ex. `SchemaOrg.astro`) inclusă în `Layout` |
| H1 / texte / „Vezi și” | componentele de hero și de conținut ale fiecărei pagini |
| Secțiunea „[ Cu cine lucrăm ]” | `src/pages/index.astro` |
| ALT tile-uri | componenta grilei de servicii |
| Script share links | componenta de distribuire socială sau `Layout.astro` |

## 4. Fișiere de raportare create

| Fișier | Conținut |
|---|---|
| `SEO_REPORT/RAPORT_SEO_ONPAGE.md` | Raport complet (audit → implementare → probleme rămase) |
| `SEO_REPORT/KEYWORD_MAPPING.md` | Maparea cuvintelor-cheie pe URL-uri |
| `SEO_REPORT/SEO_BEFORE_AFTER.md` | Comparație înainte/după per pagină |
| `SEO_REPORT/SEO_TECHNICAL_CHECKS.md` | Rezultatele verificărilor tehnice și funcționale |
| `SEO_REPORT/CHANGELOG.md` | Acest document |
| `SEO_REPORT/MIGRARE_DOMENIU_CHECKLIST.md` | Pași + template-uri `robots.txt` / `sitemap.xml` pentru lansare |
