# AGENTS.md

How to work in a repo built from this template.

## Commits

- Use conventional commits: `type(scope): description`, lowercase type.
- Only feat, fix, perf, and revert publish a release.
- A BREAKING CHANGE footer also publishes. `feat!` also publishes.
- Sign every commit. Use SSH signing.
- Never use --no-verify. If a hook fails, fix the issue.

## Hooks

- Install prek hooks: `prek install`
- Install the commit-msg hook type too: `prek install --hook-type commit-msg`
- The commit-msg hook runs commitlint. Bad commit types fail at commit time.
- CI runs the same hooks on pull requests (see pre-commit.yml).

## Workflows

- Use infralicious/actions-checkout in place of actions/checkout.
- When a workflow must use actions/checkout, set
  `with: persistent-credentials: false`.
- Pin every action by SHA. Comment the version next to the pin.
- Declare least-privilege permissions on every job.
- Write workflow code with no script injection. Never put an expression
  directly in a run script. Pass values through env instead.

## Releases

- Releases come from semantic-release on push to main. Do not cut them by hand.
- Release tooling lives in package.json. The release job installs it with npm ci.
- Do not hand-edit CHANGELOG.md. The release generates it.
- Every release carries an SBOM and an attestation.

## Do not touch

- Template placeholders (search for REPLACE_ME) until first use replaces them.
- Generated CHANGELOG.md.
- Badge URLs for another repo.

## First use

- Update badge URLs, the CODEOWNERS team, and placeholders.
- Install the Settings app and the Renovate app.
- Add the repo to safe-settings public.yml in infralicious/.github.
- For public repos, enable branch protection on main.
- To enable CodeQL, set the CODEQL_LANGUAGES repository variable.
