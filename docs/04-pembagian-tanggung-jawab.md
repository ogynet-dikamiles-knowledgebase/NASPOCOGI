# 04 — Pembagian Tanggung Jawab (Prinsip Pengelolaan Mandiri)

## 1. Prinsip

Tim IT **tidak perlu membuatkan setiap tautan**. IT bertanggung jawab memberikan akun, mengatur grup, hak akses, keamanan, masa berlaku, kapasitas, pencatatan, dan penyelesaian insiden. **Pengguna yang sudah berwenang** mengelola aktivitas file dan berbagi dokumen sehari-hari sendiri.

## 2. Tabel tanggung jawab (dari pembuat POC)

| Kegiatan | Tugas IT | Tugas pengguna |
|---|---|---|
| Akun dan grup | Membuat dan menonaktifkan akun sesuai persetujuan | Menjaga sandi dan metode autentikasi |
| Folder divisi | Menetapkan folder dan izin sesuai pemilik data | Menyimpan file hanya di area yang diizinkan |
| Mengirim dokumen | Menentukan kebijakan pembagian | Membuat sendiri tautan untuk melihat/unduh |
| Menerima berkas | Mengizinkan fungsi *File Request* bagi peran tertentu | Membuat dan menutup permintaan unggah sendiri |
| Kolaborasi | Mengatur akses pengguna atau grup lintas divisi | Mengelola folder kerja sesuai hak |
| Audit dan insiden | Meninjau catatan, menindaklanjuti penyimpangan | Melapor dan mencabut tautan jika tidak dibutuhkan |

> **Catatan kemampuan:** spesifikasi resmi menyatakan admin dapat mengizinkan pengguna non-admin untuk mengatur izin berbagi dan membuat *file request* (dengan password dan masa berlaku) **[RESMI]**. Fungsi *File Request* belum diuji di POC (tidak ada di lampiran) **[UJI]**.

## 3. Pembagian peran yang diusulkan [USULAN]

| Peran | Siapa | Wewenang | Tanggung jawab |
|---|---|---|---|
| **Administrator NAS/Drive** | IT Network / IT Support (dibatasi, 2FA wajib) | Akun, grup, Team Folder, kuota, kebijakan Drive, log | Hardening, patch, backup, penanganan insiden |
| **Pemilik data (data owner)** | Kepala divisi/departemen | Menyetujui siapa saja yang masuk grup dan peran apa | Review akses berkala, klasifikasi data |
| **Manager folder** | Penanggung jawab folder kerja (ditunjuk pemilik data) | Peran *Manager* pada folder miliknya | Mengelola anggota, mencabut link yang tidak dibutuhkan |
| **Anggota** | Karyawan | Peran *Editor* atau *Viewer* sesuai tugas | Menyimpan data di area resmi; tidak membagikan ke luar tanpa alasan |
| **Pengguna link publik** | Anggota tertentu yang disetujui | Membuat link publik (dengan password + masa berlaku) | Mencabut link setelah selesai; tidak menyebar password bersama link |
| **Auditor internal** | Internal audit | Akses baca ke log/laporan link | Review berkala, temuan |

## 4. Aturan operasional yang diusulkan [USULAN — untuk didiskusikan]

1. Data perusahaan hanya disimpan di NAS (Team Folder/My Drive); layanan eksternal lain tidak dipakai untuk data perusahaan.
2. Berbagi ke rekan internal memakai **invitee User/Group**, bukan link publik.
3. Link publik hanya untuk pihak luar, selalu dengan **password** dan **masa berlaku** (batas maksimum ditetapkan, misalnya 7 atau 30 hari — angka final diputuskan pemilik kebijakan).
4. Password link tidak dikirim bersama link yang sama; gunakan kanal berbeda.
5. Peran default *Viewer*; *Editor* untuk kolaborator; *Manager* hanya pemilik data.
6. Link dan akses ditinjau berkala memakai laporan link berbagi yang dapat diekspor **[RESMI]**.
7. Karyawan yang pindah/keluar: akses dicabut dan data bisnis dipastikan berada di Team Folder (bukan hanya My Drive).
8. Insiden (link bocor, akun dicuri): lapor ke IT; IT mencabut akses dan menelusuri log.
