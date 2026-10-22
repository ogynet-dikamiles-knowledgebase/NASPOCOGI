# 01 — Arsitektur dan Fitur Synology Drive

## 1. Komponen

| Komponen | Fungsi | Sumber |
|---|---|---|
| **Synology Drive Server** | Paket di NAS: sinkronisasi file, kolaborasi, portal web, berbagi aman, cadangan komputer, akses mobile | [RESMI] |
| **Synology Drive Admin Console** | Admin mengelola layanan sinkron, Team Folder, kebijakan versi dan berbagi, klien terhubung, pemantauan aktivitas, penggunaan penyimpanan | [RESMI] |
| **Drive Web Portal** | Akses via browser: My Drive, Team Folder, berbagi, pencarian, label, file request | [RESMI] [POC] |
| **Synology Drive Client** | Klien Windows/macOS/Linux: sinkron, backup komputer, file locking, On-demand Sync | [RESMI] |
| **Synology Drive Mobile** | iOS/Android: akses, berbagi, sinkron, backup foto/video | [RESMI] |
| **Synology Drive ShareSync** | Sinkron antar NAS (multi-site), termasuk izin | [RESMI] |
| **Synology Office** | Edit dokumen/spreadsheet/slide di browser (opsional) | [RESMI] |

## 2. Prasyarat

- DSM yang didukung Drive Server: **7.4, 7.3, 7.2** (halaman spesifikasi) [RESMI].
- Paket pendukung yang harus dipasang lebih dulu dari Package Center: **Synology Universal Search**, **Synology Application Service**, **Universal Viewer** [RESMI].
- Drive Server 3.0+ membutuhkan klien (Drive Client, ShareSync) 3.0+ [RESMI].
- Fitur tertentu punya prasyarat versi: pembatasan unduh dan watermark (Drive Server 3.4+, klien 3.4+, mobile 3.3+); file locking (klien 4.0.0+) [RESMI].
- Watermark membutuhkan RAM minimal 2 GB [RESMI].

## 3. My Drive vs Team Folder

| Aspek | My Drive | Team Folder |
|---|---|---|
| Kepemilikan | Per pengguna [POC] (kolom *Owner* = pengguna) | Berbasis **shared folder** DSM yang diaktifkan sebagai Team Folder [RESMI] |
| Izin | Diatur oleh pemilik lewat *Share* [POC] | Mengikuti izin shared folder DSM (grup/pengguna) **[UJI]**: pastikan pemetaan dengan grup divisi |
| Kebijakan versi | — | Dapat diterapkan per Team Folder (versi, retensi) [RESMI] |
| Pembatasan unduh & watermark | — | Per shared folder, hanya berlaku untuk non-admin [RESMI] |
| Recycle bin | Per pengguna (UI menyediakan *Recycle Bin*) [POC] | File yang dihapus dari Team Folder masuk Recycle Bin yang **hanya dapat diakses admin sistem** [RESMI] |
| Cocok untuk | Kerja pribadi/sementara | Data bisnis departemen |
| Status di POC | Diuji | **Belum diaktifkan** [KETERANGAN POC] |

Batasan: shared folder yang **di-mount** tidak dapat menjadi Team Folder maupun folder sinkron [RESMI].

Implikasi [USULAN]: data bisnis ditempatkan di **Team Folder** agar tidak bergantung pada akun pengguna perseorangan; My Drive untuk file pribadi/sementara.

## 4. Fitur yang relevan dengan kebutuhan

| Fitur | Ringkasan | Sumber |
|---|---|---|
| Berbagi ke pengguna/grup DSM | Langsung ke user atau grup | [RESMI] [POC] |
| Link publik | Dapat diberi password dan masa berlaku | [RESMI] [POC] |
| File Request | Mengumpulkan file dari pihak luar; password dan masa berlaku | [RESMI] |
| Label (pribadi/bersama) | Pengelompokan; label bersama dikelola admin dan dapat dialihkan pemiliknya | [RESMI] |
| File locking | Satu pengguna mengedit pada satu waktu; admin dapat membuka paksa | [RESMI] |
| Aturan sinkron | Admin dapat memblokir kategori/nama/ekstensi/ukuran file tertentu bagi pengguna terpilih | [RESMI] |
| Kontrol perangkat | Daftar koneksi klien (nama perangkat, pengguna, tipe, status, IP, lokasi); putuskan koneksi; hapus jarak jauh file tersinkron | [RESMI] |
| Pencarian | Universal Search; AI Search di model ber-GPU | [RESMI] |
| Backup paket | Hyper Backup dapat mencadangkan pengaturan dan data Drive | [RESMI] |

## 5. Batas dan angka yang perlu diingat

| Batas | Nilai | Sumber |
|---|---|---|
| Versi per file | Hingga 32 (dideduplikasi lintas versi) | [RESMI] |
| Retensi versi | 7, 30, 60, atau 120 hari | [RESMI] |
| File per klien | Hingga 500.000 (lebih dari itu dapat menurunkan kinerja) | [RESMI] |
| Tugas sinkron (klien Windows) | Hingga 64 | [RESMI] |
| Panjang path sinkron | Hingga 2.048 karakter; nama file hingga 255 | [RESMI] |
| Teks watermark | Hingga 32 karakter; file hingga 100 MB | [RESMI] |
| Koneksi klien komputer bersamaan | Bergantung model NAS | [RESMI] |
| Tugas backup komputer | Satu per akun | [RESMI] |
