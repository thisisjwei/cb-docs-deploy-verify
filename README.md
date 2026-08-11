# cb-docs-deploy-verify

Scratch verification repo: used to empirically test the commit-boost-client docs
GitHub Pages deploy workflow (docs.yml + test-docs.yml) before merging. Not a real project.

E3a: this line touches ONLY the root README (outside the path filter).

## Result summary

- PR-1's docs.yml/test-docs.yml are correct **as written** — no YAML change was needed.
- The one real blocker is a **repo setting**: the `github-pages` environment's deployment
  branch policy must include `main`. Without it the build passes, the artifact uploads,
  and the deploy job fails with:
  `Branch "main" is not allowed to deploy to github-pages due to environment protection rules.`
- A read-only default GITHUB_TOKEN does **not** break the deploy (job-level
  `pages: write` + `id-token: write` elevates fine; the deploy uses the Pages artifact +
  OIDC mechanism, not a gh-pages branch push).
