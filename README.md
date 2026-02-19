# ad-archer Scoop Bucket

Custom Scoop bucket for AD-Archer Windows packages.

## Available Apps

- `rustysound`

## Install

```powershell
scoop bucket add ad-archer https://github.com/ad-archer/bucket
scoop install ad-archer/rustysound
```

After adding the bucket, `scoop install rustysound` also works.

## Updating

```powershell
# Update Scoop + all buckets + all installed apps
scoop update

# Update only RustySound
scoop update rustysound
```

## Repository Layout

Scoop expects manifests in a `bucket/` directory:

- `bucket/rustysound.json`

The repository name can be anything (`bucket`, `scoop-bucket`, etc.). The important part is the internal `bucket/` folder.

## Auto Update (CI/CD)

This repo includes `.github/workflows/autoupdate-rustysound.yml`, which:

- no cron schedule (dispatch/manual only)
- supports manual runs (`workflow_dispatch`)
- supports external trigger via `repository_dispatch` (`rustysound-release`)
- updates `bucket/rustysound.json` using Scoop `checkver`
- smoke-tests install/uninstall
- commits and pushes if the manifest changed

## Run Update Manually

From GitHub:

1. Open `Actions`.
2. Select `Auto-update rustysound manifest`.
3. Click `Run workflow`.

From CLI:

```powershell
gh workflow run autoupdate-rustysound.yml --ref main
```

## Local Maintainer Commands

```powershell
# Update manifest from latest upstream release
& "$env:USERPROFILE\scoop\apps\scoop\current\bin\checkver.ps1" -u -Dir "$PWD\bucket" rustysound

# Test install from local manifest
scoop install .\bucket\rustysound.json
```
