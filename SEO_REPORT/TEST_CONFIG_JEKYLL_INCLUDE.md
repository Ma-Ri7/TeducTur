# TEST TEHNIC `_config.yml` — PUBLICAREA DIRECTORULUI `_astro/`

**Data:** 12 noiembrie 2026
**Obiectiv:** verificare izolată dacă `include: ["_astro"]` în `_config.yml` face GitHub Pages să publice cele 91 de resurse din `_astro/`, fără a redenumi directorul și fără a modifica HTML-ul.

> Stadiu: test de cercetare **izolat** (în `/tmp`), repo-ul principal **nu a fost modificat**. Nu s-a creat `_config.yml` în repo, nu s-a făcut commit/push/deploy.

---

## Verdict

**CONFIRMED** — configurația `include: ["_astro"]` face build-ul GitHub Pages (gem `github-pages` 232 + Jekyll 3.10.0) să publice **toate** resursele din `_astro/` (CSS, JS, imagini WebP și fonturi WOFF2) la **aceleași căi relative**, copiate **byte-cu-byte** identic, iar HTML-ul rămâne nealterat.

---

## 1. Versiunile exacte ale componentelor

| Componentă | Versiune | Sursă |
|---|---|---|
| Acțiunea de build GitHub Pages | `ghcr.io/actions/jekyll-build-pages:v1.0.13` | pasul „Pull ghcr.io/actions/jekyll-build-pages:v1.0.13" din rularea `43173665182` (API public) |
| Gem `github-pages` | **232** | `Gemfile`-ul acțiunii (`github-pages = 232`) + `pages.github.com/versions` |
| Jekyll (inclus în gem) | **3.10.0** | `pages.github.com/versions` |
| Ruby (imagine Docker) | 3.3.4 | `pages.github.com/versions` |
| Ruby folosit în testul local | 3.4.7 | `ruby@3.4` (Homebrew) |

Instalat local: `github-pages 232`, `jekyll 3.10.0` (+ dependențe), în directorul de gemuri de utilizator (`/Users/a/.gem/ruby/3.4.0`), **fără** a atinge repository-ul.

## 2. Configurația testată

```yaml
include:
  - _astro
```

- Nu există `_config.yml` preexistent în repo (verificat: `ls _config.yml` → „No such file"), deci **nu era nimic de păstrat**.
- Nicio directivă suplimentară nu este necesară (confirmat de Test B).

## 3. Comenzile efectiv executate

```bash
# instalare (mediu izolat de utilizator)
/usr/local/opt/ruby@3.4/bin/gem install github-pages -v 232 --user-install --no-document
# + gem-uri „default" retrase din Ruby 3.4: csv base64 logger ostruct rexml bigdecimal mutex_m
#   abbrev observer singleton benchmark date minitest concurrent-ruby i18n tzinfo connection_pool
#   uri erb drb racc securerandom strscan timeout

export GEM_HOME=/Users/a/.gem/ruby/3.4.0
export GEM_PATH=/Users/a/.gem/ruby/3.4.0:/usr/local/lib/ruby/gems/3.4.0
export PATH=/Users/a/.gem/ruby/3.4.0/bin:/usr/local/opt/ruby@3.4/bin:$PATH

# structura de test (în /tmp, separat de repo)
mkdir -p /tmp/teductur_jekyll_test/_astro
#   index.html + _astro/test.css + _astro/test.js + _astro/test.webp + _astro/test.woff2

# TEST A — fără _config.yml
github-pages build --source /tmp/teductur_jekyll_test --destination /tmp/teductur_outA

# TEST B — cu _config.yml (include: ["_astro"])
printf 'include:\n  - _astro\n' > /tmp/teductur_jekyll_test/_config.yml
github-pages build --source /tmp/teductur_jekyll_test --destination /tmp/teductur_outB
```

Aceasta reproduce exact comanda pipeline-ului real (din `entrypoint.sh`): `github-pages build --source … --destination …`.

## 4. Rezultatul Test A (fără `_config.yml`)

Build SUCCESS, dar output-ul conține **doar**:

```
/tmp/teductur_outA/index.html
/tmp/teductur_outA/assets/css/style.css   (temă default)
```

**`_astro/` lipsește complet** → reproduce exact simptomul din producție (HTTP 404 pe `/_astro/*`).

## 5. Rezultatul Test B (cu `include: ["_astro"]`)

Build SUCCESS; output-ul conține:

```
/tmp/teductur_outB/index.html
/tmp/teductur_outB/assets/css/style.css                  (temă default, neutilizat)
/tmp/teductur_outB/_astro/test.css      ← PREZENT
/tmp/teductur_outB/_astro/test.js       ← PREZENT
/tmp/teductur_outB/_astro/test.webp     ← PREZENT
/tmp/teductur_outB/_astro/test.woff2    ← PREZENT
```

Toate cele **4 tipuri de resurse** sunt publicate la **aceleași căi relative** (`_astro/…`).
Verificare integritate (md5 sursă vs output): **toate IDENTICE**, inclusiv binarele `.webp` și `.woff2`; `index.html` este și el **byte-cu-byte identic** (nealterat de Jekyll).

## 6. Lista resurselor găsite în output

| Fișier | Output A (fără config) | Output B (cu include) | byte-cu-byte |
|---|---|---|---|
| `_astro/test.css` | absent | **prezent** | identic |
| `_astro/test.js` | absent | **prezent** | identic |
| `_astro/test.webp` | absent | **prezent** | identic |
| `_astro/test.woff2` | absent | **prezent** | identic |
| `index.html` | prezent | prezent | identic |

## 7. Limitări / diferențe față de pipeline-ul real GitHub Pages

1. **Motorul este identic, mediul diferă minor:** testul a rulat CLI-ul `github-pages` (gem 232 + Jekyll 3.10.0) direct, nu imaginea Docker `jekyll-build-pages:v1.0.13`. Ruby a fost 3.4.7 (local) vs 3.3.4 (Docker). Comportamentul `include` este al nucleului Jekyll 3.10.0 și este independent de aceste diferențe minore de Ruby.
2. **Procesarea altor fișiere (preexistentă):** Jekyll convertește deja `.md`-urile din `SEO_REPORT/` în pagini HTML publice (verificat live: `https://teductur.eu/SEO_REPORT/SEO_TECHNICAL_CHECKS` → `200`, și `.html` → `200`). Aceasta există indiferent de `_config.yml` și este ortogonală fix-ului `_astro`.
3. **Fișier suplimentar inofensiv:** cu `_config.yml` (și fără), build-ul generează `assets/css/style.css` din tema implicită `minima`. Este un fișier neutilizat de site (nu e referit în HTML), deci nu afectează funcționarea.
4. **Finețe de configurare:** `include: ["_astro"]` înlocuiește valoarea implicită Jekyll `include: [".htaccess"]`. Nerelevant aici — GitHub Pages e hosting static (fără Apache/`.htaccess`), iar site-ul nu are astfel de fișier.
5. Referințele **OG/Twitter** din HTML sunt deja absolute (`https://teductur.eu/_astro/…`); referințele CSS/JS/`<img>` sunt relative pe 3 niveluri (`_astro/`, `../_astro/`, `../../_astro/` — 47/96/204 apariții), toate rezolvând către `/_astro/`. Nu conțin secvențe Liquid (`{{` / `{%`), deci HTML-ul este copiat verbatim (confirmat byte-cu-byte). **Nu este necesară nicio modificare în HTML.**

## 8. Recomandarea tehnică finală

Adăugarea la rădăcina repo-ului a unui fișier `_config.yml` cu **doar**:

```yaml
include:
  - _astro
```

- Rezolvă publicarea celor 91 de resurse din `_astro/` (CSS/JS/imagini/fonturi) sub GitHub Pages „Deploy from a branch".
- Nu necesită redenumirea `_astro/`, nu necesită modificarea HTML/CSS/JS/imagini/fonturilor.
- Păstrează `.nojekyll` ca atare (rămâne inofensiv, chiar dacă nu e onorat de pipeline-ul Jekyll actual).

**Atenție:** acțiunea de adăugare a `_config.yml` este **o remediere** — necesită aprobarea ta explicită. Nu am creat fișierul în repo, nu am commit/push/deploy.

Verificare post-aplicare recomandată: `https://teductur.eu/_astro/Layout.D2_G3YdX.css` → `200 text/css`; `…/Layout.astro_astro_type_script_index_0_lang.C599Q8BK.js` → `200`; `…/hero-sprinter-rosu.BWNIlai4_ZRkWb5.webp` → `200 image/webp`; `…/inter-latin-wght-normal.Dx4kXJAl.woff2` → `200`.