# Cara build jadi .apk (Finstergram)

Proyek ini terdeteksi sebagai project Android Gradle di folder `finstergram/`.

## Opsi A — Build lokal (paling cepat)
1. Install **Android Studio** (atau minimal **JDK 17**, **Android SDK**, **Platform Tools**).
2. Buka terminal di folder `finstergram/` lalu jalankan:
   ```bash
   chmod +x gradlew
   ./gradlew assembleDebug
   ```
3. Hasil APK:
   - `app/build/outputs/apk/debug/app-debug.apk` (siap dipasang ke device).
4. Jika mau rilis (unsigned):
   ```bash
   ./gradlew assembleRelease
   ```
   Hasil: `app/build/outputs/apk/release/app-release-unsigned.apk`.
   Untuk signed release, buat **keystore** lalu set variabel di `gradle.properties`:
   ```properties
   MYAPP_UPLOAD_STORE_FILE=release.keystore
   MYAPP_UPLOAD_KEY_ALIAS=upload
   MYAPP_UPLOAD_STORE_PASSWORD=********
   MYAPP_UPLOAD_KEY_PASSWORD=********
   ```
   Dan di `app/build.gradle` (android > signingConfigs > release) referensikan variabel tersebut.

## Opsi B — Otomatis via GitHub Actions (tanpa install Android Studio)
1. Commit & push folder `finstergram/` ke GitHub.
2. Workflow sudah saya buatkan: `.github/workflows/android.yml`.
3. Setelah push, buka tab **Actions** di GitHub -> workflow **Android CI**.
4. Artifact **app-debug-apk** akan berisi file APK debug yang bisa diunduh.

## Catatan
- Saya tidak bisa menjalankan Gradle/Android SDK di lingkungan ini, jadi file APK tidak bisa dibangun langsung di sini. Instruksi & workflow di atas siap pakai untuk menghasilkan APK di mesin Anda atau di GitHub.
- Jika Anda ingin **signed release APK/AAB**, beri tahu saya, saya bisa menambahkan konfigurasi signing dan AAB ke workflow.