# uniwind.net

Static site for Uniwind, served by GitHub Pages from `main` at the repository root.

```
index.html                              landing page
seven-seas-kingdom/privacy/index.html   privacy policy  (required by the App Store)
seven-seas-kingdom/support/index.html   support page     (required by the App Store)
```

## Do not hand-edit the privacy policy

`seven-seas-kingdom/privacy/index.html` is **generated**. Its source of truth is
`docs/privacy-policy.md` in the game repository, converted by `scripts/gen_privacy_html.py`
there. Edit the Markdown, regenerate, and copy the result here — otherwise the two drift and
the published policy stops matching the reviewed one.

The game links to these pages directly: `PRIVACY_URL` in `app/app_root.gd` points at
`https://uniwind.net/seven-seas-kingdom/privacy`, so that path must keep working. Changing it
means shipping a new build.

## Custom domain

`uniwind.net` is registered and delegated to AWS Route 53. To serve the site from the apex
domain, add these records in the hosted zone, then set the custom domain in
Settings ▸ Pages (which commits a `CNAME` file):

| Type | Name | Value |
|---|---|---|
| A | `uniwind.net` | `185.199.108.153` |
| A | `uniwind.net` | `185.199.109.153` |
| A | `uniwind.net` | `185.199.110.153` |
| A | `uniwind.net` | `185.199.111.153` |
| CNAME | `www` | `hanlung.github.io` |

Until then the site is live at <https://hanlung.github.io/>. Note the ordering: adding the
`CNAME` file **before** DNS resolves makes Pages redirect `hanlung.github.io` to a domain that
does not answer yet, taking the working URL down. Do the DNS first.
