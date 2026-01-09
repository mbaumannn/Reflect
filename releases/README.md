# Reflect Releases

All Reflect releases are published on **GitHub Releases**:

👉 **[View All Releases](https://github.com/mbaumannn/Reflect/releases)**

---

## Why aren't DMG files stored in git?

Binary files like DMGs are stored in **GitHub Releases** instead of git because:

- ✅ **Smaller repository**: Git repos stay lightweight and fast to clone
- ✅ **Better download experience**: Direct download links with version tags
- ✅ **Release notes**: Each release has formatted notes and changelog
- ✅ **GitHub CDN**: Fast downloads from GitHub's infrastructure

---

## Local Development

DMG files are built locally and uploaded to GitHub Releases manually or via CI.

Build a new release:
```bash
cd ../roomcorrector
./scripts/package.sh 1.0.0-betaX
```

This creates: `roomcorrector/build_release/Reflect-Beta-v1.0.0-betaX.dmg`

Upload to GitHub:
```bash
gh release create v1.0.0-betaX \
  --repo mbaumannn/Reflect \
  --title "v1.0.0-betaX — Title" \
  --notes "Release notes here" \
  --prerelease \
  path/to/Reflect-Beta-v1.0.0-betaX.dmg
```

---

## Current Releases

- **v1.0.0-beta3** (Latest) — Double-click installer
- **v1.0.0-beta2** — Performance update (vDSP optimization)
- **v1.0.0-beta1** — Initial beta release
