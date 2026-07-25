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

Live at **<https://uniwind.net>** since 2026-07-25. `uniwind.net` is registered and delegated to
AWS Route 53 (hosted zone `Z33T3XJ6J8442Z`); these records point it at GitHub Pages:

| Type | Name | Value |
|---|---|---|
| A | `uniwind.net` | `185.199.108.153` `185.199.109.153` `185.199.110.153` `185.199.111.153` |
| CNAME | `www` | `hanlung.github.io` |

The custom domain is set in Settings ▸ Pages, which is what committed the `CNAME` file, with
HTTPS enforced (Let's Encrypt cert covers `uniwind.net` + `www.uniwind.net`).
`hanlung.github.io/*` now 301-redirects here.

**If you ever re-do this, order matters:** set up DNS *first*. The `CNAME` file makes Pages
redirect `hanlung.github.io` to the custom domain, so writing it before DNS resolves takes the
only working URL offline.

## The apex A records are pinned to GitHub's IPs

Those four addresses are GitHub Pages' published apex IPs, hardcoded in DNS. If GitHub ever
changes them the site goes dark with no warning, so re-check them against
<https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site> if the
domain ever stops answering. (`www` uses a CNAME and is immune to this.)
