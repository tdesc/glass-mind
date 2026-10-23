# Public paper link deployment

Published on 2026-10-24 (Europe/Moscow) through the existing `mind-glass-site-proxy` Cloudflare Worker. The dashboard confirmed version `cb9ab7aa` as **Active / Latest**; the previous version was `9793ad15`.

The change rewrites the two exact legacy private-repository paper URLs to this public repository on successful HTML GET responses for Glass Mind paper routes. Conditional request headers and obsolete body validators are removed for those transformed responses. Other routes continue through the existing handlers.

Live verification:

| Check | Observed result |
| --- | --- |
| English paper | All 3 GitHub links point to `papers/glass-mind-v0.1-draft.md` here |
| Russian paper | All 3 GitHub links point to `papers/glass-mind-v0.1-draft-ru.md` here |
| English paper source button | Opened the public GitHub file successfully |
| Homepage | Loaded with its existing main heading |
| Deployed script | Syntax checked and matched the editor contents exactly before publication |

The Pages origin was not redeployed. Before the next source-based site or proxy deployment, apply the retained patches to that maintained source so the public URLs remain in future builds:

- [Pages and paper renderer](mind-glass-public-links.patch)
- [Proxy source](mind-glass-proxy-source-links.patch)

The paper contents were copied without changes; the internal implementation repository remains private.
