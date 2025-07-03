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

GitHub Actions will:

Build the dev flavor

Generate dev APK

Upload it as an artifact

🚀 Promote to Stage / Main
Once tested:

bash
Copy
Edit
# Promote to stage
git checkout stage
git merge dev
git push origin stage

# Promote to main (prod release)
git checkout main
git merge stage
git push origin main
main will trigger a tagged GitHub Release

APK will be attached in the "Releases" tab

📦 APK Location
After each build:

Go to your repository → Actions

Select the latest workflow run

Scroll to Artifacts or Releases (for main)

Download the .apk file

🧱 Folder Structure
lua
Copy
Edit
.github/
└── workflows/
    ├── android-dev.yml
    ├── android-stage.yml
    └── android-prod.yml

app/
└── build.gradle       <-- contains flavor configs
🧪 Android Product Flavors Used
Your app/build.gradle includes:

groovy
Copy
Edit
flavorDimensions "version"
productFlavors {
    dev {
        applicationIdSuffix ".dev"
        versionNameSuffix "-dev"
    }
    stage {
        applicationIdSuffix ".stage"
        versionNameSuffix "-stage"
    }
    prod {
        // Production flavor
    }
}
📌 Requirements
Gradle 7.3+

Java 17

GitHub Actions (free for public repos)

🙌 Credits
This setup was built and maintained by Ashique Antony.


