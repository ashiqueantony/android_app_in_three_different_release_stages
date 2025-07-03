# Android App with Multi-Stage CI/CD Pipeline 🚀

This project demonstrates a complete CI/CD setup for an Android application using **GitHub Actions**, with **three separate build stages**:

- 🔧 `dev` – Development builds
- 🧪 `stage` – Pre-production/QA testing
- 🚀 `main` – Production release builds

---

## 📁 Branches & Environments

| Branch   | Flavor  | Purpose                      | Build Command                | Output Artifact                       |
|----------|---------|------------------------------|------------------------------|----------------------------------------|
| `dev`    | `dev`   | Internal development/testing | `./gradlew assembleDevRelease`   | `app-dev-release.apk`                 |
| `stage`  | `stage` | QA, UAT, internal demo       | `./gradlew assembleStageRelease` | `app-stage-release.apk`               |
| `main`   | `prod`  | Production / Play Store      | `./gradlew assembleProdRelease`  | `app-prod-release.apk` + GitHub Release |

---

## 🔄 CI/CD Overview

CI/CD pipelines are configured using **GitHub Actions**. Each branch has its own workflow:

- `.github/workflows/android-dev.yml`
- `.github/workflows/android-stage.yml`
- `.github/workflows/android-prod.yml`

Each workflow performs:

1. ✅ Checkout source code
2. ☕ Setup Java 17
3. 🔨 Build APK using correct flavor
4. 🆔 Extract versionName from `build.gradle`
5. 🏷️ (Prod only) Create a git tag (e.g., `v1.0`)
6. 🚀 (Prod only) Publish a GitHub Release with the APK

---

## 🏁 How to Use

### ▶️ Build & Test

Make changes and push to one of the branches:

```bash
git checkout dev
# make changes
git commit -m "Update feature"
git push origin dev

