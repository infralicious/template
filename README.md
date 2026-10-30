# template

[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/infralicious/template/badge)](https://scorecard.dev/viewer/?uri=github.com/infralicious/template)
[![License: MIT](https://img.shields.io/github/license/infralicious/template)](https://github.com/infralicious/template/blob/main/LICENSE)
[![Release](https://img.shields.io/github/v/release/infralicious/template)](https://github.com/infralicious/template/releases)

Language-agnostic. This template ships CI/CD, security, and agent tooling.
It ships no service code. Each generated repo adds its own build, test, and deploy.

## What ships here

- Prek hooks: whitespace, final newline, YAML check, large files, actionlint, commitlint.
- Workflows: OpenSSF Scorecard, CodeQL, dependency review, pre-commit, release.
- Semantic release from conventional commits. Only feat, fix, perf, and revert publish.
- package.json holds release tooling only (semantic-release and plugins). It is not service code.
- SBOM and attestation on every release.
- AGENTS.md and CLAUDE.md for agent tooling.
- CodeRabbit config that inherits the org central config.
- Settings file, Renovate config, Dependabot config, editorconfig, gitignore.
- Docs folder with an ADR folder.

## What does not ship here

- No service code. No build or test workflow. No language runtime.
- No CONTRIBUTING, code of conduct, SUPPORT, issue templates, or PR template.
  The org .github repo provides them as defaults. Do not duplicate them.
- No branch protection in settings.yml. Free private repos get API 403 for it.
  Public repos add it at first use (see below).

## First use

1. Create your repo from this template (Use this template button).
2. Update every badge URL to your new repo name.
3. Update the CODEOWNERS team. The template ships a placeholder team.
4. Replace placeholders (search for REPLACE_ME).
5. Install prek hooks, including the commit-msg hook type:
   - `prek install`
   - `prek install --hook-type commit-msg`
6. Install the Settings app and the Renovate app.
7. Add your repo to safe-settings public.yml in infralicious/.github.
8. For public repos, enable branch protection on main.
   Require pull requests, one approving review, and required status checks.
   Block force-push and deletion.
9. To enable CodeQL, set the CODEQL_LANGUAGES repository variable.
   Example value: `javascript-typescript,python`. Without it, the CodeQL job skips.
10. Push to main. Confirm the Scorecard run publishes. Confirm the first release
    appears after the first feat or fix commit.

## Create a repo from this template (gh CLI)

Create the repo from the template:
`gh repo create infralicious/NEW-NAME --template infralicious/template --public`
Use --private for a private repo. The new repo starts with the template
files and no template history. Clone it after creation:
`gh repo clone infralicious/NEW-NAME`

Set the CodeQL languages variable (change the list to your stack):
`gh variable set CODEQL_LANGUAGES --repo infralicious/NEW-NAME --body "javascript-typescript,python"`
Without this variable, the CodeQL job skips. List variables with:
`gh variable list --repo infralicious/NEW-NAME`

Set a secret only when the new repo needs one. The template needs none:
`gh secret set SECRET_NAME --repo infralicious/NEW-NAME --body "value"`
Prefer --env-file for values from a file. Never paste a secret in chat.
For a value shared by all repos, set an org variable or secret with --org.

Then follow First use: badge URLs, CODEOWNERS, placeholders, apps,
safe-settings entry, and branch protection.

## Notes

- Secret scanning and push protection are on by default for public repos.
  Private repos inherit the org defaults.
- settings.yml is inert without the Settings app. Install the app first.
- Renovate config holds repo-level rules only. Central Renovate owns schedule,
  timezone, dashboard, and discovery. Dependabot covers GitHub Actions only,
  so the two bots never propose the same update.
- The Scorecard badge stays empty until the first Scorecard run publishes.
- The version badge stays empty until the first release.
- CodeRabbit reads AGENTS.md as review criteria. AGENTS.md does double duty.

## Troubleshooting

- Hooks fail: run `prek run --all-files` and fix the reported files.
- No release publishes: check commit types. Only feat, fix, perf, and revert
  publish. Check for a BREAKING CHANGE footer or a `!` marker.
- Scorecard badge empty: check that the first Scorecard run published.
- CodeQL job skips: set the CODEQL_LANGUAGES repository variable.
