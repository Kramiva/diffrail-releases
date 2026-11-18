# Diffrail releases

Download files for [Diffrail](https://diffrail.com). There is no source code here: each
[release](https://github.com/Kramiva/diffrail-releases/releases) holds the installers for one version.

## Publishing a version

1. **Releases** → **Draft a new release**.
2. Choose a tag such as `v0.3.0` (create it on publish). The title can be `Diffrail 0.3.0`.
3. Drag in the installers, for example `diffrail-0.3.0-mac-arm64.dmg` and `diffrail-0.3.0-win-x64.exe`.
   File names decide the buttons on diffrail.com:
   - `.dmg` is macOS, `.exe` or `.msi` is Windows, `.AppImage`, `.deb` or `.rpm` is Linux.
   - `arm64` in the name means Apple silicon (or Arm), `x64` means Intel / 64-bit, `universal` means both Mac chips.
   - Anything else (`.blockmap`, `.yml`, `.zip`) is kept for the app's updater and isn't shown on the site.
4. Leave **Set as a pre-release** off, and **Publish release**.

Within a couple of minutes the [Update the website](.github/workflows/update-website.yml) workflow writes the release
into the website repo, and Hostinger redeploys diffrail.com with download buttons, sizes and SHA-256 checksums.

Added a file to a release that was already published? Run the workflow by hand: **Actions** → **Update the website** →
**Run workflow**.

## Taking a version down

Delete the release (or mark it as a pre-release). The workflow then points the site at the previous release, or back
to the waitlist if there is none.

## Setup (once)

The workflow needs a secret named `WEBSITE_TOKEN`: a fine-grained personal access token with **Contents: Read and
write** on `Kramiva/diffrail-website` only. Settings → Secrets and variables → Actions → New repository secret.
