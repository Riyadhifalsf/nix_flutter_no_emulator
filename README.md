<h1>Flutter + Android SDK Dev Shell (Tanpa Emulator)</h1>

<p align="center">
  <b>🔥 Environment siap pakai untuk Flutter Android development langsung ke HP tanpa emulator 🔥</b>
</p>

---

## <u>Deskripsi</u>
<p>
Flake ini menyediakan lingkungan pengembangan Flutter untuk Android <b>tanpa emulator</b>. Semua tools yang dibutuhkan sudah termasuk:
Flutter SDK, Android SDK, NDK, Gradle, JDK, CMake, dan Ninja.  
Lingkungan ini reproducible, portabel, dan mudah digunakan di NixOS.  
</p>

<p>
Tujuan utama flake ini adalah memungkinkan <b>build APK langsung ke HP Android</b>, tanpa perlu emulator. Cocok untuk workflow ringan dan fokus ke perangkat nyata.
</p>

---

## <u>Fitur Utama</u>

<ul>
  <li>Flutter SDK siap pakai (stable channel)</li>
  <li>Android SDK dengan build-tools, platform-tools, dan NDK</li>
  <li>Gradle & JDK17 otomatis dikonfigurasi</li>
  <li>CMake dan Ninja untuk integrasi native</li>
  <li>Environment FHS (Filesystem Hierarchy Standard)</li>
  <li>Path, license, dan konfigurasi SDK otomatis</li>
  <li>Fokus deploy ke HP nyata, <b>tanpa emulator</b></li>
</ul>

---

## <u>Prasyarat Sistem</u>

<ul>
  <li>Sistem operasi: <b>NixOS 24.x</b> (direkomendasikan)</li>
  <li>CPU: minimal Intel i3 gen 10 atau setara</li>
  <li>RAM: minimal 8 GB</li>
  <li>Storage: minimal 10 GB kosong untuk SDK</li>
  <li>HP Android dengan <b>USB Debugging aktif</b></li>
  <li>Kabel USB untuk koneksi HP</li>
  <li><b>Tidak memerlukan GPU khusus</b> karena emulator tidak digunakan</li>
</ul>

---

## <u>Instalasi</u>

<ol>
  <li><b>Clone repository dan masuk ke folder:</b>
  <pre><code>git clone https://github.com/Riyadhifalsf/nix_flutter_no_emulator.git 
cd nix_flutter_no_emulator</code></pre>
  </li>

  <li><b>Masuk ke dev shell:</b>
  <pre><code>nix develop</code></pre>
  <p>Nix akan menyiapkan environment FHS otomatis.</p>
  </li>

  <li><b>Cek instalasi Flutter & Android:</b>
  <pre><code>flutter doctor</code></pre>
  <p>Pastikan semua tanda centang hijau, terutama Android toolchain. Tidak akan muncul error emulator.</p>
  </li>
</ol>

---

## <u>Membuat Proyek Flutter Baru</u>

<p>Jika folder kosong, shell secara otomatis akan membuat proyek baru. Untuk manual:</p>

<pre><code>flutter create my_app
cd my_app</code></pre>

<ul>
  <li>Struktur proyek Flutter standar akan dibuat</li>
  <li>Direktori <code>.android/sdk</code> sudah terhubung ke proyek</li>
</ul>

---

## <u>Menyambungkan HP Android</u>

<ol>
  <li>Aktifkan <b>USB Debugging</b> di HP:
    <ul>
      <li>Settings → Developer options → USB debugging</li>
    </ul>
  </li>
  <li>Sambungkan HP ke PC via USB</li>
  <li>Cek apakah HP terdeteksi:
  <pre><code>adb devices</code></pre>
  Harus muncul serial number HP dengan status <code>device</code>.</li>
</ol>

---

## <u>Build APK untuk HP</u>

<ol>
  <li>Build APK release:
  <pre><code>flutter build apk --release</code></pre>
  APK akan tersedia di: <code>build/app/outputs/flutter-apk/app-release.apk</code>
  </li>
  
  <li>Install APK ke HP:
  <pre><code>adb install -r build/app/outputs/flutter-apk/app-release.apk</code></pre>
  <p><b>-r</b> = replace, mengganti versi sebelumnya jika ada</p>
  </li>
</ol>

---

## <u>Menjalankan Aplikasi Langsung di HP</u>

<pre><code>flutter run</code></pre>

<p>
Flutter akan otomatis membangun & menginstal APK di HP, dan log real-time akan muncul di terminal.
</p>

---

## <u>Update Tools & Dependencies</u>

<pre><code>nix flake update
flutter upgrade</code></pre>

<p>
- Nix Flake menjaga environment reproducible  
- Flutter SDK tetap di versi stable
</p>

---

## <u>Tips & Troubleshooting</u>

<ul>
  <li><b>ADB tidak mengenali HP:</b>
    <pre><code>adb kill-server
adb start-server</code></pre>
  </li>
  
  <li><b>Flutter Doctor error Android SDK:</b> Pastikan shell aktif (<code>nix develop</code>) dan <code>ANDROID_HOME</code> sudah benar.</li>
  
  <li><b>Build gagal karena NDK/Gradle:</b> Flake sudah patch & pin versi. Cek <code>android/app/build.gradle.kts</code> atau <code>gradle.properties</code> jika ingin sesuaikan manual.</li>
  
  <li><b>Masalah permission:</b> Pastikan direktori <code>.android/sdk</code> writable:
  <pre><code>chmod -R u+w .android/sdk</code></pre></li>
  
  <li>Restart shell setelah update flake atau install dependencies baru</li>
</ul>

---

# License 

This flake is licensed under the MIT License . 

