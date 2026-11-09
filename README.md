# FindMeFlatMate website

This repo is the website at **https://findmeflatmate.com**. Its files are copied from the app's
source, `flatmates/` in [kamalmotiani1989-cmd/NavigateMe](https://github.com/kamalmotiani1989-cmd/NavigateMe),
by `.github/workflows/publish.yml`, which commits them to `main` and mirrors `main` to `gh-pages`. Change the app
there, not here: copied files are overwritten on the next run.

## When it publishes

- **On demand:** Actions → Publish FindMeFlatMate → Run workflow.
- **When NavigateMe asks:** a `repository_dispatch` event of type `publish`. To have NavigateMe send it after every
  change to `flatmates/`, create a fine-grained token (GitHub → Settings → Developer settings → Fine-grained tokens:
  Only select repositories → findmeflatmate; Repository permissions → Contents: Read and write), and save it in
  NavigateMe → Settings → Secrets and variables → Actions as `SITE_DISPATCH_TOKEN`. A step in NavigateMe's website
  workflow then calls `POST /repos/kamalmotiani1989-cmd/findmeflatmate/dispatches` with `{"event_type":"publish"}`.
  Never put the token in a file.
- **Schedule (fallback):** at :17 and :47 past each hour. GitHub runs scheduled jobs on a best-effort basis; the
  old every-30-minutes schedule (:00 and :30, the busiest minutes) fired only every 4 to 8 hours.

GitHub Pages: Settings → Pages → Deploy from a branch → `gh-pages`, `/ (root)`, custom domain
`findmeflatmate.com`, Enforce HTTPS.

DNS for `findmeflatmate.com`:

| Type  | Name  | Value                          |
|-------|-------|--------------------------------|
| A     | `@`   | `185.199.108.153`              |
| A     | `@`   | `185.199.109.153`              |
| A     | `@`   | `185.199.110.153`              |
| A     | `@`   | `185.199.111.153`              |
| CNAME | `www` | `kamalmotiani1989-cmd.github.io` |

## What gets published

- The pages are **compacted** on the way (no source comments or spacing, short names inside functions),
  with [html-minifier-terser](https://github.com/terser/html-minifier-terser). The readable source
  stays in NavigateMe.
- The **Android app** is copied from NavigateMe's `flatmates-apk` release to this repo's own
  `flatmates-apk` release whenever there's a new build, so the download link
  `https://github.com/kamalmotiani1989-cmd/findmeflatmate/releases/download/flatmates-apk/flatmates.apk`
  keeps working when NavigateMe is private.

## NavigateMe private

This repo has to stay public (GitHub Pages), but NavigateMe can be private. The publish job then needs a
token to read it:

1. GitHub → your photo → **Settings** → **Developer settings** → **Personal access tokens** →
   **Fine-grained tokens** → **Generate new token**. Name it `findmeflatmate publish`, pick an
   expiry, **Repository access: Only select repositories → NavigateMe**, and under **Repository
   permissions** set **Contents: Read-only** (Metadata: Read-only is added by itself). Generate and copy it.
2. This repo → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**:
   name `SOURCE_TOKEN`, paste the token.
3. NavigateMe → **Settings** → **General** → at the bottom, **Change repository visibility** → **Private**.

When the token expires, publishing stops (the Actions tab shows the clone failing): make a new one the
same way and replace the secret.

