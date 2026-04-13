# szkola_funkcje

Statyczna strona (HTML + JS) — panel do nauki funkcji w C++ / JavaScript. Pliki strony leżą w **`public/`**, żeby deploy na Pages nie wysyłał na CDN całego repozytorium (np. `.github`).

## Cloudflare Pages

Wdrożenie z katalogu **`public`** (bez kroku build).

### Opcja A — GitHub Actions (automat po `push` na `main`)

1. W Cloudflare: **My Profile → API Tokens** — utwórz token z uprawnieniami **Cloudflare Pages — Edit** (oraz **Account Settings — Read**, żeby odczytać konto).
2. W GitHub: **Settings → Secrets and variables → Actions** — dodaj:
   - `CLOUDFLARE_API_TOKEN` — wartość tokena
   - `CLOUDFLARE_ACCOUNT_ID` — **Overview** konta w panelu Cloudflare (prawy sidebar)
3. Pierwszy raz w Cloudflare możesz utworzyć pusty projekt **Pages** o nazwie `szkola-funkcje` albo pozwolić, aby pierwszy deploy z Wranglera go zarejestrował (zależnie od konta — jeśli deploy się poskarży, utwórz projekt ręcznie z tą samą nazwą).
4. Wypchnij kod na `main` — workflow `.github/workflows/deploy-cloudflare-pages.yml` wykona `wrangler pages deploy public`.

Jeśli zmienisz nazwę projektu w Cloudflare, zaktualizuj parametr `--project-name=` w workflow.

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

### Pages tylko z panelu (bez Actions)

W Cloudflare **Workers & Pages → Create → Connect to Git** — repozytorium `AdamBrti/szkola_funkcje`, preset **None**, **Build command** puste, **Build output directory** `public`.
