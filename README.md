# szkola_funkcje

Statyczna strona (HTML): interaktywne tematy z programowania w C++ dla klasy 8 szkoły podstawowej. Pliki strony leżą w **`public/`**, żeby deploy na Pages publikował tylko gotową stronę.

## Cloudflare Pages

Wdrożenie z katalogu **`public`** (bez kroku build). Repozytorium nie używa GitHub Actions do deployu.

### Opcja A — Cloudflare Pages z Git

W Cloudflare **Workers & Pages → Create → Pages → Connect to Git**:

- Repository: `AdamBrti/szkola_funkcje`
- Framework preset: **None**
- Build command: puste
- Build output directory: `public`

Każdy push na `main` uruchomi deploy po stronie Cloudflare Pages.

### Opcja B — tylko z komputera (Wrangler)

```bash
npx wrangler pages deploy public --project-name=szkola-funkcje
```

Przy pierwszym użyciu Wrangler zaloguje Cię do Cloudflare (OAuth).

## Repozytorium GitHub

Nowe repozytorium:

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/AdamBrti/szkola_funkcje.git
git push -u origin main
```

Istniejące repozytorium — tylko remote i push:

```bash
git remote add origin https://github.com/AdamBrti/szkola_funkcje.git
git branch -M main
git push -u origin main
```

## Struktura

- `public/index.html` — strona główna z kartami tematów
- `public/funkcje.html` — temat: funkcje w C++
- `public/tablice.html` — temat: tablice w C++
- `public/powtorka.html` — temat: powtórzenie (zmienne, funkcje, tablice)
- `public/_headers` — podstawowe nagłówki dla Cloudflare Pages
- `wrangler.jsonc` — lokalna konfiguracja pod deploy przez Wrangler
