# hREA developer docs

Source for [docs.hrea.io](https://docs.hrea.io), the developer documentation for the hREA GraphQL APIs.

## How this repository publishes

- **`docs/` is the source.** Every page lives there. `mkdocs.yml` at the root holds the theme and the navigation.
- **`main` is the branch that publishes.** A push to `main` runs `.github/workflows/deploy.yml`, which builds the site with MkDocs Material and pushes the result to `gh-pages`.
- **`gh-pages` is machine-written.** GitHub Pages serves it at docs.hrea.io. Never edit it by hand.
- **Pull requests build but do not publish.** The same workflow runs `mkdocs build --strict` on every PR, so a nav entry pointing at a missing file, or a dead internal link, fails the check rather than reaching the site.

If you edit a page and nothing changes on the site, check the Actions tab first. Before September 2026 the MkDocs setup lived on a `github-pages` branch that was never merged, so edits to `main` published nothing at all. That is fixed, and the branch is superseded.

## Working on the docs locally

```bash
pip install -r requirements.txt   # the same toolchain CI installs
mkdocs serve             # live preview on http://127.0.0.1:8000
mkdocs build --strict    # the same check CI runs
```

## What belongs here, and what belongs in the hREA repository

This site is for developers **building an application on hREA**: getting connected, the integration path, and the GraphQL reference.

Documentation for developers working **on hREA itself** lives with the code, in [`docs/` in the hREA repository](https://github.com/h-REA/hREA/tree/sprout/docs): architecture, repository structure, contributing, and how to consume a release. Where this site needs a fact that the hREA repository already states, it links there rather than keeping a second copy that can drift.

## License

Apache 2.0, as with the rest of hREA.
