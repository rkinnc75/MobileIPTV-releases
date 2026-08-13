# MobileIPTV — releases

Public distribution point for [MobileIPTV](https://github.com/rkinnc75/MobileIPTV).
**Artifacts only. No source.**

This repository is public **by necessity**: the in-app updater fetches
`version.json` and the APK unauthenticated. The source repository stays private.

## Contents

| File | Purpose |
|---|---|
| `version.json` | Update manifest the app polls |
| Release assets | Signed sideload APKs, one per tag |

## `version.json`

```json
{
  "versionCode": 1,
  "versionName": "0.1.0",
  "apkUrl": "https://github.com/rkinnc75/MobileIPTV-releases/releases/download/v0.1.0/MobileIPTV-v0.1.0.apk",
  "apkSha256": "<sha256 of the asset>",
  "changelog": "Short, user-facing summary."
}
```

The app **verifies `apkSha256` before installing, on every path.**

## Publishing order is load-bearing

`version.json` is written **only after** the APK asset is confirmed downloadable.
Publishing the manifest first makes the app see a new version and 404 on the
download — an intermittent-looking failure that cost a sibling project eight
fixes. The release workflow enforces this and refuses to publish otherwise.

Releases are cut by the `release` workflow in the source repo, triggered by
pushing a tag created **locally** on a commit already on `main`.

## Play Store builds

Google Play builds are **not** published here. The Play flavour ships without the
in-app updater entirely — self-updating violates Play policy. See
`spec/54` and `spec/55` in the source repo.
