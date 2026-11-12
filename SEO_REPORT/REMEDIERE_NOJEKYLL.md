# REMEDIERE .NOJEKYLL — REZULTATE ȘI VERDICT

**Data:** 12 noiembrie 2026
**Domeniu:** `https://teductur.eu`
**Acțiune:** crearea fișierului `.nojekyll` în rădăcină, commit + push pe `main`, apoi verificare HTTP.

---

## Verdict final

**REMEDIEREA NU A REZOLVAT PROBLEMA.** Fișierul `.nojekyll` a fost creat, comis și publicat corect, iar build-ul GitHub Pages a rulat cu succes, **dar resursele din `_astro/` continuă să răspundă cu `404`**.

Motivul (descoperit în această etapă): site-ul folosește GitHub Pages „Deploy from a branch", al cărui pipeline intern (`pages-build-deployment`) este acum bazat pe acțiunea **`jekyll-build-pages`**, care apelează **`github-pages build` (Jekyll) necondiționat** — scriptul său `entrypoint.sh` **nu conține nicio verificare `.nojekyll`**. Prin urmare `.nojekyll` nu mai este onorat, iar Jekyll continuă să excludă directorul `_astro/`.

---

## 1. Ce s-a făcut (corect, conform instrucțiunilor)

| Pas | Stare | Dovadă |
|---|---|---|
| Fișier `.nojekyll` creat la rădăcină (același nivel cu `index.html`, `CNAME`) | ✅ | `wc -c .nojekyll` → `0`; blob git `e69de29…` (blob gol) |
| Fără alte modificări în commit (fără HTML/CSS/JS/imagini, fără `.DS_Store`, fără rapoarte) | ✅ | `git diff --cached --stat` → doar `.nojekyll \| 0` |
| Commit cu mesajul cerut | ✅ | `54aa301 Fix GitHub Pages Astro asset publishing` |
| Push pe `main` | ✅ | `1104a76..54aa301 main -> main` |
| `.nojekyll` pe GitHub | ✅ | `raw.githubusercontent.com/.../main/.nojekyll` → `200`, 0 bytes |

## 2. Verificările HTTP (după publicare)

Testate la ora 07:14 → 07:39 GMT (≈26 min după push, inclusiv cereri directe la origin cu `x-cache: MISS`):

| Resursă | HTTP așteptat | HTTP real | Verdict |
|---|---|---|---|
| `https://teductur.eu/.nojekyll` | 404* | **404** | ✅ (normal — fișier de control, nu se servește) |
| `https://teductur.eu/_astro/Layout.D2_G3YdX.css` | 200 | **404** | ❌ |
| `https://teductur.eu/_astro/Layout.astro_astro_type_script_index_0_lang.C599Q8BK.js` | 200 | **404** | ❌ |
| `https://teductur.eu/_astro/hero-sprinter-rosu.BWNIlai4_ZRkWb5.webp` | 200 | **404** | ❌ |
| `https://teductur.eu/_astro/inter-latin-wght-normal.Dx4kXJAl.woff2` | 200 | **404** | ❌ |
| `https://teductur.eu/` | 200 | **200** | ✅ |
| `https://teductur.eu/servicii/` | 200 | **200** | ✅ |
| `https://teductur.eu/flota/` | 200 | **200** | ✅ |

\* `.nojekyll` returnează 404 și după o remediere reușită — este fișier de control (dotfile), nu conținut servit. Indicatorul real de succes este răspunsul `200` al resurselor `_astro/`, care **nu** s-a produs.

## 3. De ce NU a funcționat `.nojekyll` (cauza rafinată, cu dovezi)

**Dovada mecanismului de publicare** (API GitHub, public):

- Workflow intern: `actions/workflows` → `pages-build-deployment` (path `dynamic/pages/pages-build-deployment`).
- Rularea (run `43173665182`) a deploy-ului commit-ului `54aa301` (= commit-ul `.nojekyll`):
  - job `build` → pasul `Pull ghcr.io/actions/jekyll-build-pages:v1.0.13` ✅, pasul **`Build with Jekyll`** ✅ (~6 s);
  - job `deploy` → `Deploy to GitHub Pages` ✅;
  - stare finală: **`success`**, `sha: 54aa301`, `ref: main`.
- Sursa acțiunii (`actions/jekyll-build-pages` `entrypoint.sh`) execută:
  `github-pages build --source … --destination …`
  **fără** nicio ramură „dacă există `.nojekyll` → copiază static".

**Concluzie:** pipeline-ul actual „Deploy from a branch" rulează Jekyll în toate cazurile. Regula Jekyll de excludere a directoarelor cu prefix `_` (`_astro/`) rămâne activă. `.nojekyll` era onorat de vechiul sistem de build GitHub Pages (documentat până ~2022), dar **nu mai este onorat** de noul backend (`jekyll-build-pages` + gem `github-pages`).

## 4. Soluții recomandate (necesită aprobare — implică alte tipuri de modificări)

1. **Redenumirea `_astro/ → assets/` (recomandată, garantată).**
   - `git mv _astro assets`
   - înlocuire în toate cele 11 fișiere HTML a referințelor `_astro/`, `../_astro/`, `../../_astro/` → `assets/`, `../assets/`, `../../assets/`.
   - actualizare `og:image`/`twitter:image` + `image` din JSON-LD (`https://teductur.eu/_astro/…` → `https://teductur.eu/assets/…`).
   - fără prefix `_` → Jekyll nu mai exclude nimic.

2. **Adăugare `_config.yml` cu `include: ["_astro"]`** (fără editarea HTML).
   - spune Jekyll să nu excludă `_astro/`; funcționează ca „opt-in" pentru directoare cu prefix `_`.

3. **Migrare la GitHub Actions (static, fără Jekyll)** — recomandat pe termen lung.
   - workflow cu `actions/configure-pages` → `actions/upload-pages-artifact` → `actions/deploy-pages` (fără pas Jekyll) și comutarea sursei Pages în „GitHub Actions" (setare din UI-ul GitHub, nu din git).

## 5. Pași următori

1. Alege una dintre soluțiile de la §4 (recomand A, sau B pentru intervenție minimă).
2. Aplic + commit + push.
3. Reverific HTTP: CSS/JS/imagine/font din directorul de asset-uri trebuie să răspundă `200` cu content-type corect (`text/css`, `application/javascript`, `image/webp`, `font/woff2`).