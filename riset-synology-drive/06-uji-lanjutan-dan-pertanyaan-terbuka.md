# 06 — Uji Lanjutan dan Pertanyaan Terbuka

Daftar hal yang **belum terverifikasi** dan perlu diuji agar keputusan tidak bertumpu pada asumsi. Prioritas: **P1** = menentukan kelayakan/keamanan, **P2** = penting, **P3** = pelengkap.

## A. Uji di lingkungan POC

| ID | Uji | Hasil yang diharapkan/dicatat | Prioritas | Status |
|---|---|---|---|---|
| U01 | Aktifkan **Team Folder** untuk satu shared folder; beri izin ke `Grup_DIVISI_A`; cek apa yang terlihat oleh anggota dan non-anggota | Pemetaan izin grup → Team Folder; perbedaan dengan My Drive | P1 | ☐ |
| U02 | Akses **SMB dan Drive** ke folder yang sama; ubah file lewat salah satu jalur | Apakah perubahan terdeteksi di kedua jalur; versi tercatat | P1 | ☐ |
| U03 | **Kuota**: tetapkan kuota shared folder dan kuota pengguna; isi sampai penuh | Perilaku saat penuh; pesan error; apakah recycle bin dihitung | P1 | ☐ |
| U04 | **File Request**: buat sebagai pengguna non-admin; unggah dari luar | Fungsi, opsi password/masa berlaku, lokasi file | P1 | ☐ |
| U05 | **Link publik**: daftar lengkap opsi *Privacy Settings*; mode preview-saja; layar password pengunjung | Screenshot tiap mode; konfirmasi perilaku | P1 | ☐ |
| U06 | **Link publik pada folder**: tambah file setelah link dibuat; coba rename/buat folder sebagai pengunjung | Apakah file baru terpapar; konfirmasi batasan | P1 | ☐ |
| U07 | **Peran**: untuk tiap peran, catat tombol yang aktif/nonaktif di sisi penerima | Matriks aksi per peran dengan screenshot | P2 | ☐ |
| U08 | **Berbagi UserB → UserA** (arah sebaliknya) | Screenshot *Shared with me* milik UserA | P2 | ☐ |
| U09 | **Siapa boleh membuat link publik**: cari pengaturan admin; uji akun non-admin | Apakah dapat dibatasi per pengguna/grup | P1 | ☐ |
| U10 | **Wajib password/masa berlaku**: cari apakah ada pengaturan admin; coba buat link tanpa keduanya | Penegakan teknis vs. hanya SOP | P1 | ☐ |
| U11 | **Akun dinonaktifkan/dihapus**: apa yang terjadi pada file di My Drive dan link yang sudah dibuat | Perilaku data "yatim"; link masih berfungsi? | P1 | ☐ |
| U12 | **Log**: lakukan serangkaian aksi (berbagi, unduh, ubah peran, cabut); cek di log portal/Admin Console | Apakah semua aksi tercatat; siapa/kapan/IP | P1 | ☐ |
| U13 | **Versioning & restore**: timpa file beberapa kali; pulihkan; hapus lalu pulihkan dari recycle bin | Alur pemulihan dan kebutuhan admin | P2 | ☐ |
| U14 | **Hyper Backup** ke target lain; uji restore satu folder | Waktu dan keberhasilan pemulihan | P1 | ☐ |
| U15 | **2FA wajib** untuk satu grup; login ulang | Alur 2FA pengguna; dampak pada klien/mobile | P2 | ☐ |
| U16 | **Klien Drive desktop & mobile**: sinkron, file locking | Kompatibilitas, kinerja | P3 | ☐ |
| U17 | **Pembatasan unduh dan watermark** pada satu folder | Perilaku untuk non-admin vs. admin | P3 | ☐ |

## B. Pertanyaan yang perlu dijawab sebelum produksi

| # | Pertanyaan | Pemilik |
|---|---|---|
| Q1 | Model NAS perusahaan, versi DSM, versi Drive Server, **file system volume (Btrfs/ext4)**? | IT |
| Q2 | Apakah NAS perusahaan memiliki kapasitas dan RAM yang cukup (mis. watermark butuh ≥2 GB RAM; jumlah koneksi klien tergantung model)? | IT |
| Q3 | Strategi backup NAS saat ini: apa, ke mana, kapan terakhir diuji restore? | IT |
| Q4 | Apakah ada identitas terpusat (AD/LDAP) yang akan dipakai? Drive untuk pengguna domain membutuhkan grup keamanan [RESMI] | IT |
| Q5 | Siapa pemilik data tiap folder saat ini? Berapa pemakaian saat ini? | Kepala divisi |
| Q6 | Data apa yang boleh dibagikan ke pihak luar? | Legal/Compliance |
| Q7 | Apa alasan nyata pengguna memakai Google Drive (wawancara singkat)? | IT + HR |
| Q8 | Bagaimana jalur publikasi POC (reverse proxy/tunnel/port-forward) dibuat? | Bragy |
| Q9 | Perbedaan tampilan *Team Folder* antara UserA (ada panah perluasan) dan UserB (tidak ada) pada EV-03 dan EV-04 — mengapa? | Bragy |
| Q10 | Apakah DSM `nas.ogy.my.id` dan Drive `naspoc.ogy.my.id` pada evidence adalah NAS yang sama? | Bragy |

## C. Cara mencatat hasil uji

Setiap uji dicatat dengan format: ID uji · tanggal · hasil · screenshot (simpan di `evidence/` dengan nomor EV berikutnya) · tindak lanjut. Perbarui juga [../docs/03-hasil-poc.md](../docs/03-hasil-poc.md) dan label **[UJI]** pada dokumen terkait menjadi **[POC]** setelah terverifikasi.
