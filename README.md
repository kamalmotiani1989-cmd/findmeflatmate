# FindMeFlatMate website

This repo is the website at **https://findmeflatmate.com**. Its files are copied from the app's
source, `flatmates/` in [kamalmotiani1989-cmd/NavigateMe](https://github.com/kamalmotiani1989-cmd/NavigateMe),
by `.github/workflows/publish.yml` (every 30 minutes, or on demand from the Actions tab), which
commits them to `main` and mirrors `main` to `gh-pages`. Change the app there, not here: copied
files are overwritten on the next run.

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
