# RAPORT SEO ON-PAGE — TEDUC TUR

**Data:** 12 noiembrie 2026
**Proiect:** website Teduc Tur (transport persoane, Huedin, jud. Cluj)
**Mediu analizat:** `https://demo.mrwebsites.ro/teduc-tur/` (mediu demo — domeniul final nu este stabilit)
**Limbă:** română
**Verdict:** **SUCCESS** (optimizare implementată efectiv; vezi secțiunea „Probleme rămase” pentru elementele care depind de decizii externe)

---

## 1. Situația inițială (audit)

### 1.1 Tehnologie și sursă de adevăr

| Aspect | Constatare |
|---|---|
| Tip site | Site **static**, generat cu **Astro** (output HTML pre-compilat) |
| CMS / pluginuri SEO | **Nu există** CMS, temă WordPress sau plugin SEO. Nu există risc de implementare duplicată. |
| Fișiere sursă | În directorul de lucru există **doar build-ul** (HTML + `_astro/` cu CSS, JS, imagini, fonturi). Nu există `src/`, `astro.config`, `package.json`. |
| Generare meta | Meta-urile erau **scrise manual** în fiecare fișier HTML, parțial (doar `title` + `description` + `robots` + `theme-color`) |
| CSS/JS | `_astro/Layout.D2_G3YdX.css` (Tailwind compilat) și `_astro/Layout.astro_astro_type_script_index_0_lang.C599Q8BK.js` — **nu au fost modificate** |

> **Consecință importantă:** toate optimizările au fost aplicate direct în HTML-ul publicat, cu păstrarea integrală a claselor CSS existente. Orice clasă Tailwind nou-introdusă a fost verificată că există deja în CSS-ul compilat (detalii la §7 și în `SEO_TECHNICAL_CHECKS.md`).

### 1.2 Pagini publice identificate (11)

| # | URL relativ | Tip |
|---|---|---|
| 1 | `/index.html` | Pagina principală |
| 2 | `/servicii/index.html` | Hub servicii |
| 3 | `/servicii/curse-regulate-speciale/index.html` | Serviciu B2B |
| 4 | `/servicii/curse-ocazionale/index.html` | Serviciu B2C |
| 5 | `/servicii/transport-special/index.html` | Serviciu B2C |
| 6 | `/servicii/transfer-aeroport/index.html` | Serviciu B2C |
| 7 | `/servicii/servicii-aeroport/index.html` | Serviciu B2C (asistență la terminal) |
| 8 | `/servicii/evenimente/index.html` | Serviciu B2C |
| 9 | `/flota/index.html` | Flotă |
| 10 | `/despre-noi/index.html` | Despre companie |
| 11 | `/contact/index.html` | Contact + cerere ofertă |

### 1.3 Probleme constatate înainte de implementare

| Problemă | Detaliu măsurat |
|---|---|
| **Meta description duplicate** | Aceeași descriere (158 caractere) pe **5 pagini**: Acasă, Servicii, Flota, Despre noi, Contact |
| **Meta description prea lungi** | 330 caractere (Curse regulate), 274 (Transfer aeroport), 212 (Transport special), 209 (Curse ocazionale) — trunchiate în SERP |
| **Title-uri scurte / generice** | 35–47 caractere: „Curse ocazionale Huedin \| Teduc Tur”, „Flota: microbuze și autocar \| Teduc Tur” — fără cuvânt-cheie comercial |
| **H1 generice** | „Servicii”, „Curse ocazionale”, „Flota”, „Despre noi”, „Transport evenimente” — fără expresia-țintă |
| **Lipsă canonical** | 0/11 pagini |
| **Lipsă Open Graph / Twitter Cards** | 0/11 pagini |
| **Lipsă date structurate** | 0 blocuri JSON-LD pe tot site-ul |
| **ALT lipsă pe imaginile de conținut** | 6 tile-uri de serviciu pe Acasă + 6 pe pagina Servicii aveau `alt` gol |
| **Lipsă robots.txt / sitemap.xml** | Nu existau în rădăcina proiectului |
| **Domeniu demo hardcodat** | Linkurile „Distribuie pe Facebook/WhatsApp” de pe 6 pagini de serviciu conțineau `https://demo.mrwebsites.ro/teduc-tur/...` |
| **Conținut subțire** | Flota: 74 cuvinte; Servicii (hub): 97 cuvinte; lipsa oricărei secțiuni B2C/B2B pe Acasă |
| **Indexare** | `meta robots = noindex, nofollow` pe toate paginile — **corect pentru demo, păstrat nemodificat** |

---

## 2. Strategia SEO aplicată

1. **Un cuvânt-cheie principal distinct per URL** (fără canibalizare între pagini).
2. **Separare B2C / B2B**: pagina Acasă primește o secțiune dedicată celor două categorii, cu linkuri descriptive către serviciile potrivite.
3. **SEO local** doar acolo unde serviciile existente justifică menționarea localităților (Huedin, Cluj-Napoca, Ciucea, Poieni, Sâncraiu, Călățele, Izvorul Crișului, Beliș, Oradea). **Nu** s-au creat pagini locale noi (fără doorway pages).
4. **Date structurate doar cu informații reale** (fără rating, prețuri, program, coordonate inventate).
5. **Zero modificări de design**: s-au folosit exclusiv clase și tipare existente în site (`.wrap`, `.eticheta`, `.titlu-sectiune`, `.lista-sageti`, `.text-corp`, `font-display`, etc.).
6. **Zero modificări de URL**, de date de contact, de formulare sau de funcționalități.

---

## 3. Title și Meta Description finale (toate unice)

| Pagina | SEO Title (caractere) | Meta Description (caractere) |
|---|---|---|
| Acasă | `Transport persoane Huedin – microbuze și autocar \| Teduc Tur` (60) | `Transport persoane din Huedin cu microbuz și autocar, cu șofer: curse regulate pentru firme și școli, excursii, transfer aeroport și transport la evenimente.` (157) |
| Servicii | `Servicii de transport persoane în Huedin și Cluj \| Teduc Tur` (60) | `Curse regulate pentru firme și școli, excursii cu microbuzul, transport la comandă, transfer aeroport și transport pentru evenimente, cu șofer.` (143) |
| Curse regulate speciale | `Transport angajați Cluj și Huedin – curse regulate \| Teduc Tur` (62) | `Transport angajați și elevi pe traseu fix, cu microbuz cu șofer, din Huedin și satele din jur spre Cluj-Napoca. Contract, program și factură lunară.` (148) |
| Curse ocazionale | `Închiriere microbuz cu șofer – excursii și grupuri \| Teduc Tur` (62) | `Închiriere microbuz sau autocar cu șofer pentru excursii, pelerinaje, ieșiri cu colegii și excursii școlare, din Huedin și Cluj. Preț stabilit dinainte.` (152) |
| Transport special | `Transport persoane la comandă, Huedin – Cluj \| Teduc Tur` (56) | `Transport persoane la comandă, cu microbuz sau autocar, pe traseul și la ora alese de tine: delegații, echipe sportive, grupuri private. Preluare din Huedin.` (157) |
| Transfer aeroport | `Transfer aeroport Cluj din Huedin și Oradea \| Teduc Tur` (55) | `Transfer aeroport Cluj-Napoca și Oradea din Huedin, cu microbuz și șofer. Preluare de la adresă și așteptare la sosiri, pentru familii și grupuri.` (146) |
| Servicii aeroport | `Asistență la aeroport Cluj: sosiri și bagaje \| Teduc Tur` (56) | `Servicii aeroport pentru grupuri: urmărim zborul, așteptăm la sosiri, ajutăm cu bagajele și preluăm pe rând grupurile care sosesc cu zboruri diferite.` (150) |
| Evenimente | `Transport persoane la evenimente: nunți, botezuri \| Teduc Tur` (61) | `Transport pentru nunți, botezuri și alte evenimente: ducem invitații de acasă la biserică, la restaurant și înapoi, oricât de târziu se termină.` (144) |
| Flota | `Închiriere microbuze cu șofer, Huedin–Cluj \| Teduc Tur` (54) | `Microbuze Mercedes-Benz Sprinter de 8+1 și 20+1 locuri, Iveco Daily de 19+1 locuri și autocar Irizar, cu șofer. Vezi interiorul și capacitatea fiecăruia.` (153) |
| Despre noi | `Despre Teduc Tur – firmă de transport persoane Huedin` (53) | `Firmă de transport persoane din Huedin, județul Cluj, activă din 2019: microbuze, autocar și șoferi cu atestat, pentru firme, școli, parohii și familii.` (152) |
| Contact | `Contact Teduc Tur – ofertă transport persoane Huedin` (52) | `Cere ofertă de transport persoane: spune-ne de unde pleci, unde mergi, când și câți sunteți. Telefon 0770 859 339, WhatsApp și e-mail, din Huedin.` (146) |

**Verificat automat:** 0 title-uri duplicate, 0 descrieri duplicate, 0 title/description goale.

## 4. Modificări de heading-uri (H1)

| Pagina | H1 înainte | H1 după |
|---|---|---|
| Acasă | Teduc Tur - transport de persoane cu microbuz și autocar, din Huedin în toată țara | *(nemodificat — conține deja expresia-țintă)* |
| Servicii | Servicii | **Servicii de transport persoane** |
| Curse regulate speciale | Curse regulate speciale | **Curse regulate speciale pentru angajați** |
| Curse ocazionale | Curse ocazionale | **Închiriere microbuz cu șofer** |
| Transport special | Transport special | **Transport persoane la comandă** |
| Transfer aeroport | Transfer aeroport | **Transfer aeroport Cluj din Huedin** |
| Servicii aeroport | Servicii aeroport | **Servicii aeroport Cluj** |
| Evenimente | Transport evenimente | **Transport persoane la evenimente** |
| Flota | Flota | **Închiriere microbuze cu șofer** |
| Despre noi | Despre noi | **Firmă de transport persoane în Huedin** |
| Contact | Contact | *(nemodificat — intenție navigațională)* |

- Fiecare pagină are **exact un H1** (verificat).
- Ierarhia H2/H3 a fost păstrată și completată logic: pe Acasă s-au adăugat un H2 nou („Transport persoane pentru persoane fizice și pentru firme”) și două H3 („Pentru persoane fizice”, „Pentru companii și instituții”).
- H2-urile descriptive existente (ex. „Curse regulate speciale din Huedin – transport zilnic pentru angajați și elevi”) au fost **păstrate** — acoperă deja expresiile secundare.
- Verificat: H1 nu depășește banda hero pe niciun viewport (mobil 390px / tabletă 900px / desktop 1440px).

## 5. Modificări de conținut

### 5.1 Conținut nou pe pagina Acasă (secțiune nouă, integrată în design)

Secțiune nouă „**[ Cu cine lucrăm ] — Transport persoane pentru persoane fizice și pentru firme**”, plasată între grila de servicii și secțiunea „De ce să mergi cu Teduc Tur”:

- paragraf introductiv B2C + B2B (firme, școli, instituții) și acoperire geografică reală;
- două coloane cu linkuri descriptive: **4 linkuri B2C** (curse ocazionale, transfer aeroport, evenimente, transport special) și **4 linkuri B2B** (curse regulate/angajați, contract cu factură lunară → Contact, flotă, asistență la aeroport);
- paragraf de **SEO local**: „Deservim Huedinul și satele din jur — Ciucea, Poieni, Sâncraiu, Călățele, Izvorul Crișului, Beliș —, orașul Cluj-Napoca și județul Cluj, iar pentru transferuri ajungem și la Aeroportul Oradea.”

Textul folosește **doar informații existente deja pe site** (anul 2019, capacitățile 8+1/19+1/20+1, localitățile, facturarea lunară, atestatele).

### 5.2 Conținut adăugat pe paginile de serviciu

Fiecare pagină de serviciu a primit **un paragraf de context** (informație existentă, reformulată) + un bloc **„Vezi și”** cu 2 linkuri interne descriptive:

| Pagina | Paragraf adăugat (rezumat) | Linkuri „Vezi și” |
|---|---|---|
| Curse regulate speciale | contracte pe perioade lungi, factură lunară, traseu ajustabil când se schimbă programul | Flotă (8+1, 19+1, 20+1 + autocar) · Contact |
| Curse ocazionale | șoferul rămâne cu grupul la cursele de mai multe zile; preț pentru tot drumul | Flotă · Contact |
| Transport special | preluare de la adresă sau aeroport, lăsare la adresa cerută | Flotă · Contact |
| Transfer aeroport | preluare din Huedin și satele din jur (Ciucea, Poieni, Sâncraiu, Călățele, Izvorul Crișului, Beliș) + curse de noapte | Flotă · Contact |
| Servicii aeroport | asistența se combină cu transferul pentru grupuri mari | **Transfer aeroport** (diferențiere de intenție) · Contact |
| Evenimente | numărul de curse după localitățile invitaților; curse de noapte programate dinainte | **Curse ocazionale** · Contact |

### 5.3 Pagina Servicii (hub) și Flota

- **Servicii:** paragraf nou care separă clar B2C/B2B + „Vezi și” către Flotă și Contact.
- **Flota:** paragraf nou de alegere a vehiculului după număr de persoane (8+1 pentru familii, 19+1/20+1 pentru angajați și excursii, autocar pentru grupuri mari; dotări reale: aer condiționat, încălzire, centuri, loc de bagaje) + listă „Vezi și” către 3 servicii relevante și Contact.

### 5.4 Ce NU s-a modificat în conținut

- Textele comerciale existente (testimoniale, valori, echipă, dotări) au rămas **neatinse**.
- Nu s-au adăugat prețuri, tarife, program de lucru, disponibilitate 24/7, rute noi sau promisiuni neverificate.
- Datele de contact (telefon `0770 859 339`, e-mail `teductur@gmail.com`, „Huedin, jud. Cluj”, administrator „Radu Neag”) sunt **identice**.

**Volum de text:** 2.861 → **3.323 cuvinte** în `<main>` (+462), distribuite țintit, fără „umplutură”.

## 6. Optimizarea imaginilor (ALT)

| Pagina | Imagini | ALT completate | Observații |
|---|---|---|---|
| Acasă | 22 | **+6** | Cele 6 tile-uri din grila de servicii au primit ALT descriptiv, unic |
| Servicii | 13 | **+6** | Aceleași 6 tile-uri, ALT-uri descriptive |
| Celelalte 9 pagini | 7–16 | 0 | Imaginile erau deja acoperite |

ALT-uri introduse (exemple): „Curse regulate speciale pentru angajați, cu microbuzul Teduc Tur”, „Excursie cu microbuzul, pentru un grup organizat de Teduc Tur”, „Transport special la comandă, cu microbuzul Teduc Tur”, „Transfer aeroport cu microbuzul, din Huedin – Teduc Tur”, „Asistență la aeroport, pentru pasagerii grupurilor – Teduc Tur”, „Transport invitați la nuntă și botez, cu microbuzul Teduc Tur”.

**Decizie documentată:** cele 6 miniaturi din mega-meniu (dropdown desktop) **rămân cu `alt=""`**. Sunt imagini decorative în linkuri care au deja text vizibil (eticheta serviciului), deci `alt=""` este varianta corectă și evită dublarea descrierii pe aceeași pagină. La fel, imaginile de fundal ale benzilor hero (`bg-*.webp`) au `alt=""` — sunt decorative, sensul este dat de H1.

Imaginile, fișierele, dimensiunile și calitatea **nu au fost modificate** (verificat prin hash).

## 7. Linking intern

| Cerință | Stare |
|---|---|
| Pagina principală → toate serviciile importante | ✅ grilă de 6 tile-uri + noua secțiune cu 8 linkuri descriptive |
| Curse regulate → Contact | ✅ meniu + „Cere ofertă pe WhatsApp”/„Sună acum” + „Vezi și: Cere ofertă pentru transport angajați” |
| Curse ocazionale → Flotă + Contact | ✅ „Vezi și” cu ambele |
| Transfer aeroport → Contact + Flotă | ✅ „Vezi și” cu ambele |
| Evenimente → Contact + Curse ocazionale | ✅ „Vezi și” cu ambele |
| Flota → serviciile relevante | ✅ listă nouă: angajați, excursii, transfer aeroport + Contact |
| Despre noi → Servicii + Contact | ✅ listă de 4 servicii + „Mai mult” + linkuri Contact în header/footer |
| Anchor text descriptiv | ✅ toate linkurile noi au text descriptiv (nu „click aici”) |
| Linkuri interne defecte | ✅ 0 (777 referințe verificate) |

## 8. Date structurate (Schema.org / JSON-LD)

Implementate **11 blocuri JSON-LD**, toate valide sintactic (parse JSON reușit) și fără date inventate:

| Pagina | Tipuri |
|---|---|
| Acasă | `LocalBusiness` (`@id: #teduc-tur`) + `WebSite` |
| Servicii | `BreadcrumbList` + `CollectionPage` + `ItemList` (6 servicii) |
| Curse regulate / Curse ocazionale / Transport special / Transfer aeroport / Servicii aeroport / Evenimente | `BreadcrumbList` + `Service` (cu `provider`, `areaServed`) |
| Flota | `BreadcrumbList` + `CollectionPage` |
| Despre noi | `BreadcrumbList` + `AboutPage` (+ `about: LocalBusiness`) |
| Contact | `BreadcrumbList` + `ContactPage` (+ `about: LocalBusiness`) |

Date folosite (toate reale, preluate din site): denumire legală `S.C. Teduc Tur S.R.L.`, nume comercial `Teduc Tur`, telefon `+40770859339`, e-mail `teductur@gmail.com`, localitate `Huedin`, județ `Cluj`, țară `RO`, an înființare `2019`, administrator `Radu Neag`, `areaServed`: Huedin, Cluj-Napoca, Ciucea, Poieni, Sâncraiu, Călățele, Izvorul Crișului, Beliș, Oradea, județul Cluj.

**Deliberat NU s-au adăugat:** `aggregateRating`, `review`, `priceRange`, `openingHoursSpecification`, `geo`, `sameAs` (linkul Facebook este generic, nu o pagină reală), adresă stradală (nu există în site).

## 9. Optimizări tehnice

| Element | Implementare |
|---|---|
| **Canonical** | `<link rel="canonical" href="index.html">` — **relativ, auto-referențial**, valabil pe orice domeniu și pe orice subcale (ex. `/teduc-tur/`). Fără domeniu hardcodat. |
| **Open Graph** | `og:type`, `og:site_name`, `og:locale=ro_RO`, `og:title`, `og:description`, `og:image` (relativ, imagine reprezentativă per pagină) |
| **Twitter Cards** | `summary_large_image` + title/description/image |
| **Robots meta** | `noindex, nofollow` **păstrat pe toate paginile** (mediu demo — nemodificat fără aprobare) |
| **`og:url`** | **Omis intenționat** — ar necesita domeniul final |
| **robots.txt / sitemap.xml** | **Necreate** în site — ar necesita URL-uri absolute. Template-uri gata de folosit în `SEO_REPORT/MIGRARE_DOMENIU_CHECKLIST.md` |
| **Linkuri de distribuire socială** | Domeniul demo `demo.mrwebsites.ro` **eliminat din comportament**: 6 pagini de serviciu au un script inline care reconstruiește URL-urile din `location.href` (funcționează pe orice domeniu). URL-ul demo rămâne doar ca fallback fără JavaScript. |
| **Imagini** | Neschimbate; `loading="eager"` + `fetchpriority="high"` pe imaginea hero, `lazy` pe restul; `width`/`height` prezente (fără CLS) |
| **Structură semantică** | `header`, `nav`, `main#continut`, `section[aria-labelledby]`, `footer`, skip-link — nemodificate |
| **HTML** | Tag-uri echilibrate pe toate cele 11 pagini (verificat cu parser) |

## 10. Probleme rămase (necesită decizie / intervenție la lansare)

1. **Indexarea demo-ului** — `noindex, nofollow` este activ pe toate paginile. **Nu a fost modificat** (cerință explicită). La lansare trebuie eliminat.
2. **Domeniul final** — canonical, `og:url`, `og:image`, `sitemap.xml`, `robots.txt` trebuie absolutizate la migrare. Pași concreți: `SEO_REPORT/MIGRARE_DOMENIU_CHECKLIST.md`.
3. **Variante de URL duplicate** — serverul poate servi atât `/servicii/` cât și `/servicii/index.html`. Canonical-ul actual indică varianta `.../index.html` (cea folosită de linkurile interne). Recomandare: alegeți o singură variantă și 301 către ea (decizie de infrastructură).
4. **Suprapunere controlată: Transfer aeroport vs Servicii aeroport** — intenții distincte (drum vs. asistență la terminal). Diferențiate prin title/description/H1 și legate între ele. Dacă în viitor conținutul devine identic, se recomandă consolidare (nu s-a făcut automat).
5. **Testimoniale fără schema `Review`** — există 4 testimoniale reale, dar fără rating numeric verificabil; conform regulilor, nu s-au marcat ca date structurate.
6. **Fișiere sursă Astro** — build-ul a fost modificat direct. La următoarea regenerare din sursă, modificările trebuie replicate în componentele `.astro`. Vezi `CHANGELOG.md` §„Note pentru rebuild”.
7. **Consistență socială** — linkul Facebook din footer este `https://www.facebook.com/` (generic). După ce se cunoaște pagina reală, se poate adăuga `sameAs` în JSON-LD.

