# 01 — Latar Belakang dan Tujuan

## 1. Latar belakang

Berdasarkan informasi saat ini, **internal audit masih menemukan kasus berbagi folder menggunakan Google Drive**. Kekhawatiran utamanya adalah data perusahaan berada di luar kendali perusahaan: siapa yang punya akses, kapan akses dicabut, dan ke mana data diteruskan sulit ditelusuri.

Di sisi lain, NAS perusahaan sudah ada tetapi **pemanfaatannya belum maksimal**:

- belum ada aturan ketat tentang **kapasitas pemakaian** tiap departemen;
- belum ada aturan tegas tentang **hak akses**: siapa saja yang boleh memakai NAS dan dengan peran apa;
- cara kerja saat ini adalah **SMB ke endpoint user**, dikelompokkan dalam grup per departemen.

## 2. Langkah proaktif IT Support saat ini

Memfungsikan NAS sebagai **share folder SMB pada umumnya** dan mengelola seluruh user lewat **permission grup per departemen**. Langkah ini menertibkan akses, tetapi belum menjawab kebutuhan yang membuat pengguna lari ke Google Drive: berbagi cepat ke rekan lintas divisi dan ke pihak luar lewat tautan.

## 3. Tantangan

> Bagaimana meminimalkan kasus serupa (berbagi data lewat layanan di luar kendali perusahaan) **dan** memanfaatkan NAS perusahaan jauh lebih baik daripada kondisi sekarang?

## 4. Hipotesis yang diuji POC

NAS yang dimiliki mendukung pengalaman "ala Google Drive" secara native lewat paket **Synology Drive**. Hipotesisnya:

| # | Hipotesis | Tingkat keyakinan awal |
|---|---|---|
| H1 | Fitur dasar drive (My Drive, unggah, folder, label, bintang) berjalan 100% native | Diuji — lihat EV-03, EV-04 |
| H2 | Berbagi file/folder dari pemilik ke user lain, dalam satu departemen maupun lintas departemen, berjalan native | Diuji — EV-05 s.d. EV-09 |
| H3 | Berbagi publik (tanpa akun) tersedia tetapi **tidak 100% sama** dengan Google Drive | Diuji — EV-10 s.d. EV-12 |
| H4 | Pengelolaan dapat dilakukan **mandiri oleh pengguna berwenang**; IT fokus pada akun, grup, kebijakan, keamanan, kuota, dan audit | Dirancang — lihat [04](04-pembagian-tanggung-jawab.md) |

## 5. Tujuan

1. Memberi gambaran nyata (visual dan bisa dicoba) cara kerja Synology Drive.
2. Memetakan **perbedaan** dari kondisi existing (SMB) dan dari Google Drive.
3. Mengidentifikasi **risiko** sebelum berdampak ke bisnis, beserta mitigasinya.
4. Menyiapkan **bahan keputusan**: kuota, hak akses, kebijakan berbagi, dan dukungan yang dibutuhkan dari departemen lain.
5. Mendokumentasikan jejak dan knowledge base agar dapat dilanjutkan tim.

## 6. Ruang lingkup

**Termasuk:** akun dan grup DSM, My Drive, berbagi antar user (peran Previewer/Viewer/Editor/Manager), berbagi publik via link (password dan masa berlaku), riset fitur resmi Synology Drive yang relevan.

**Belum termasuk (ditunda):**

- **Team Folder** — sengaja belum diaktifkan di POC sampai ada diskusi lebih lanjut [KETERANGAN POC];
- integrasi Active Directory/LDAP;
- uji performa dan beban, klien desktop/mobile;
- uji ketahanan (backup/restore, failover);
- desain akses dari internet lewat FortiGate pada lingkungan produksi (hanya dibahas sebagai pertimbangan desain — lihat [riset/05](../riset-synology-drive/05-publikasi-eksternal-fortigate.md)).

## 7. Lingkungan dan batasan

- POC dijalankan **100% di lingkungan pribadi** milik Bragy, bukan di NAS produksi perusahaan, karena POC ini berawal dari tantangan langsung untuk membuktikan cara kerja Synology Drive.
- Data uji hanya berupa gambar dummy (desain halaman login). Tidak ada data perusahaan.
- Hasil POC menunjukkan **kemampuan fitur**, bukan jaminan konfigurasi produksi. Konfigurasi produksi harus divalidasi ulang di NAS perusahaan (model, versi DSM, versi Drive Server, file system).
