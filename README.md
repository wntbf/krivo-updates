# krivo updates

Official public update channel for **krivo**, the Windows video editor.

- Latest version manifest: [latest.json](https://raw.githubusercontent.com/wntbf/krivo-updates/main/latest.json).
- Windows installers: [GitHub Releases](https://github.com/wntbf/krivo-updates/releases).
- Source code and Windows builds remain in a separate private development repository.

## How publishing works

The [publish-update workflow](.github/workflows/publish-update.yml) checks for new Windows installers released from the private `flekideveloper/personal-hub-android` build repository, publishes the installer here, computes its SHA-256, and updates `latest.json` **only after** the public installer is available.

The workflow runs every six hours and can also be started manually from **Actions → Publish krivo update → Run workflow**.

### One-time secret

The repository owner needs to add **Actions secret** `KRIVO_SOURCE_TOKEN` containing a **read-only fine-grained GitHub PAT** from the `flekideveloper` account. The token must be limited to `flekideveloper/personal-hub-android` with **Contents: Read-only**. Store it only under repository **Settings → Secrets and variables → Actions → New repository secret**. Never commit it.

The built-in `GITHUB_TOKEN` is used for publishing to this public repository, so the source token never requires write access.

## Security

The Windows app checks that manifest and installer URLs use HTTPS and validates the downloaded setup file against its SHA-256 before asking the user to install. SHA-256 guards against download corruption but does **not** replace code signing or protect against compromised repository permissions. Releases should eventually be signed with a trusted Windows code-signing certificate. No GitHub user token is embedded into krivo.


Update channel: publish krivo v0.9.15 after verified Windows build.
