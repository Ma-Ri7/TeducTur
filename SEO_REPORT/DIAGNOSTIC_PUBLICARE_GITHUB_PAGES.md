# DIAGNOSTIC PUBLICARE GITHUB PAGES — TEDUC TUR

**Data:** 12 noiembrie 2026
**Domeniu:** `https://teductur.eu`
**Obiectiv:** identificarea cauzei pentru care site-ul funcționează corect local (`http://localhost:8000/`), dar pe domeniul public apare fără CSS, cu imagini lipsă, meniu neformatat și pictograme supradimensionate.

> Stadiu: **diagnostic READ-ONLY**. Nu s-a modificat niciun fișier al site-ului, nu s-a creat `.nojekyll`, nu s-a executat commit/push/deploy.

---

## Verdict

**CONFIRMED** — cauza este identificată cu dovezi directe, reproductibile prin `curl`.

**Cauza:** GitHub Pages rulează **Jekyll** peste conținutul publicat (implicit la deploy din branch). Jekyll exclude din publicare orice director/fișier al cărui nume începe cu `_` (și cu `.`). Directorul de build Astro se numește **`_astro/`** și, deci, **nu este publicat**. În repo lipsește fișierul **`.nojekyll`**, care ar fi dezactivat procesarea Jekyll. Consecința: toate resursele din `_astro/` (CSS, JS, imagini, fonturi) returnează **404** pe domeniul public, în timp ce local (`python3 -m http.server`) sunt servite normal.

---

## 1. Metoda actuală de publicare

| Element | Valoare | Dovadă |
|---|---|---|
| Tip site | Static, build Astro comis direct în rădăcina repo | există `index.html`, `servicii/`, `_astro/` la rădăcină |
| Ramură publicată | `main` | `git branch -a` → doar `main`; `default_branch: main` (API) |
| Metodă | **GitHub Pages — „Deploy from a branch”**, sursa `main` / rădăcină (`/`) | nu există `.github/workflows/` (deci nu GitHub Actions); nu există branch `gh-pages` |
| Domeniu personalizat | `teductur.eu` | fișier `CNAME` în rădăcină = `teductur.eu` |
| DNS | apex → IP-uri GitHub Pages (`185.199.108/109/110/111.153`); `www` → CNAME `ma-ri7.github.io` | `dig` |
| Pages activ | `has_pages: true` | API repo |
| `.nojekyll` | **lipsă** | `ls .nojekyll` → „No such file"; `find . -name .nojekyll` → gol; live `/.nojekyll` → `404` |

> Notă: API-urile `GET /repos/{owner}/{repo}/pages` și `.../pages/builds/latest` returnează `404` pentru cereri **neautentificate** (endpointele de Pages necesită autentificare), deci nu au putut confirma configurația la nivel de API. Metoda de mai sus este stabilită prin dovezile de tip fișier/ramură/DNS, nu prin API.

## 2. Cauza exactă

GitHub Pages, la deploy din branch, rulează **Jekyll** în mod implicit. Comportamentul Jekyll:

- exclude din publish directorii denumiți cu prefix `_` (underscore) — ex. `_astro/`, `_layouts/` etc.;
- exclude fișierele/directoarele denumite cu prefix `.`;
- singurul mecanism oficial de **dezactivare** a Jekyll este un fișier gol `.nojekyll` în rădăcina repo-ului.

Directorul de build Astro este **`_astro/`** și conține 100% din CSS/JS/fonturi/imagini. Fără `.nojekyll`, nicio resursă din `_astro/` nu este publicată.

**De ce local merge:** `python3 -m http.server` servește fișierele de pe disc fără nicio filtrare, deci `_astro/` și toate resursele sale sunt accesibile.

## 3. Dovezi concrete

### 3.1. `.nojekyll` lipsește
- `ls -la .nojekyll` → `No such file or directory`
- `find . -name '.nojekyll'` → niciun rezultat
- `https://teductur.eu/.nojekyll` → `404` (HTML pagină de eroare)

### 3.2. `_astro/` există local și este urmărit în git (deci e în repo-ul publicat)
- `ls _astro | wc -l` → **91 fișiere**
- `git ls-files _astro | wc -l` → **91** (toate urmărite; nu există `.gitignore`)
- Componență: `1` CSS, `1` JS, `7` fonturi `.woff2`, `82` imagini `.webp`

### 3.3. Live: tot ce e în `_astro/` → 404; tot ce e în afara lui → 200

| Resursă | HTTP | Content-Type | Corect? |
|---|---|---|---|
| `https://teductur.eu/` | 200 | text/html | ✅ |
| `https://teductur.eu/_astro/Layout.D2_G3YdX.css` | **404** | text/html | ❌ (pagină eroare) |
| `https://teductur.eu/_astro/Layout.astro_astro_type_script_index_0_lang.C599Q8BK.js` | **404** | text/html | ❌ |
| `https://teductur.eu/_astro/hero-sprinter-rosu.BWNIlai4_ZRkWb5.webp` | **404** | text/html | ❌ |
| `https://teductur.eu/_astro/hero-sprinter-rosu-mobil.D_z0tBCN_2euK3n.webp` | **404** | text/html | ❌ |
| `https://teductur.eu/_astro/inter-latin-wght-normal.Dx4kXJAl.woff2` | **404** | text/html | ❌ |
| `https://teductur.eu/favicon.svg` (în afara `_astro/`) | **200** | image/svg+xml | ✅ |
| `https://teductur.eu/index.html` | 200 | text/html | ✅ |
| `https://teductur.eu/servicii/index.html` | 200 | text/html | ✅ |

Primii octeți ai răspunsului pentru CSS sunt `<!DOCTYPE html><html>...` — adică **pagina de eroare 404 GitHub Pages**, nu fișierul CSS. Aceasta confirmă că fișierul nu este publicat, nu că ar exista o problemă de rută relativă.

### 3.4. Referințele din HTML coincid exact cu fișierele locale (exclus mismatch de nume/cale)

- Pagina principală: `<link rel="stylesheet" href="_astro/Layout.D2_G3YdX.css">`, script `_astro/Layout.astro_astro_type_script_index_0_lang.C599Q8BK.js`, imagini `_astro/...webp` (cu `srcset`).
- Paginile interioare folosesc căi relative corecte (`../_astro/...`, `../../_astro/...`), toate rezolvând către `_astro/` din rădăcină.
- Fișierele locale au **exact** denumirile referite (ex. `_astro/Layout.D2_G3YdX.css`). Nu există diferențe de majuscule/minuscule.

## 4. Resursele care nu se încarcă (sumar)

Toate resursele din `_astro/` (91 fișiere). Reprezentativ:

| URL | HTTP |
|---|---|
| `/_astro/Layout.D2_G3YdX.css` | 404 |
| `/_astro/Layout.astro_astro_type_script_index_0_lang.C599Q8BK.js` | 404 |
| `/_astro/hero-sprinter-rosu.BWNIlai4_ZRkWb5.webp` | 404 |
| `/_astro/hero-sprinter-rosu-mobil.D_z0tBCN_2euK3n.webp` | 404 |
| `/_astro/inter-latin-wght-normal.Dx4kXJAl.woff2` | 404 |

Simptomele observate (site fără stilizare, imagini lipsă, meniu neformatat, pictograme supradimensionate) sunt consecința directă a faptului că **CSS-ul nu se încarcă** (pictogramele SVG au dimensiunile date exclusiv de clasele CSS `size-*`, care lipsesc) și **JS-ul nu se încarcă** (caruselul Flotă, meniul mobil, formularul „Cere ofertă" → WhatsApp nu inițializează).

## 5. Soluția minimă recomandată

Adăugarea unui fișier **`.nojekyll`** (gol, 0 bytes) în **rădăcina repo-ului**, apoi commit + push pe `main`:

```
(conținut gol)
```

Acest lucru spune GitHub Pages să **nu** mai ruleze Jekyll, astfel încât directorul `_astro/` să fie publicat ca atare, iar toate resursele statice să redevină accesibile (`200`).

Alternativă (nedorită, invazivă): redenumirea `_astro/` → `assets/` și actualizarea tuturor referințelor din cele 11 fișiere HTML. Soluția `.nojekyll` este minimă, reversibilă și nu modifică HTML/CSS/JS.

## 6. Fișierele care ar trebui modificate ulterior (după aprobare)

| Fișier | Acțiune |
|---|---|
| `.nojekyll` (rădăcină) | **de creat** (fișier gol) — remedierea propriu-zisă |

Nu este necesară nicio altă modificare: HTML-ul, CSS-ul, JS-ul, imaginile, fonturile și configurația SEO/domeniului rămân neschimbate.

---

## Anexă — comenzi reproduse (read-only)

```bash
git branch -a                                    # doar main
find . -name '.nojekyll'                         # gol
ls _astro | wc -l                                # 91
git ls-files _astro | wc -l                      # 91 (toate urmărite)
curl -s -o /dev/null -w '%{http_code} %{content_type}\n' \
  https://teductur.eu/_astro/Layout.D2_G3YdX.css   # 404 text/html
curl -s -o /dev/null -w '%{http_code} %{content_type}\n' \
  https://teductur.eu/favicon.svg                   # 200 image/svg+xml
curl -s -o /dev/null -w '%{http_code}\n' \
  https://teductur.eu/.nojekyll                      # 404
```