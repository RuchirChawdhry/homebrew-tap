# Homebrew Tap 🍺

Personal Homebrew formulae for public command-line projects.

## Installation

Once a formula has been reviewed and merged:

```bash
brew tap RuchirChawdhry/tap
brew install RuchirChawdhry/tap/<formula>
```

No formulas are published yet.

## Automated release proposals

Every day at **09:23 IST**, this tap checks the public GitHub Releases
registered in [packages.json](packages.json). If the latest stable release
has a new standalone macOS archive, the shared ci-workflows engine
downloads it, verifies its SHA-256, generates a Homebrew formula,
and opens a **review-only PR**.

Nothing merges automatically and nothing is submitted to Homebrew's
official repositories. Application repositories do not need write tokens.

The catalog starts empty. To opt a project into monitoring, add an entry:

```json
{
  "name": "example-cli",
  "repository": "OWNER/PUBLIC-REPO",
  "asset": "example-cli-macos-x64.tar.gz",
  "binary": "example-cli",
  "architecture": "x86_64",
  "description": "A command-line application",
  "homepage": "https://github.com/OWNER/PUBLIC-REPO",
  "license": "MIT"
}
```

This is a template, not an existing package. Put it in the catalog's
`packages` array once the actual public release exists. Supported
archives currently contain one executable at their root.

Run manually from **Actions > Propose Homebrew formula updates > Run workflow**.
PR checks use non-publishing dry-run mode.

### Required GitHub permission

Enable **Settings > Actions > General > Workflow permissions >
Allow GitHub Actions to create and approve pull requests**. This authorizes
the bot to create proposals in this tap only; it never approves or merges.

The automation skips when an earlier promotion PR awaits review. Because
`GITHUB_TOKEN`-created PRs do not automatically trigger additional CI,
the updater syntax-checks formulas before proposing them. Native installation
checks belong to the application's release pipeline.

Shared logic: [ci-workflows](https://github.com/RuchirChawdhry/ci-workflows).
