# 04 — Keamanan, Audit, dan Backup

## 1. Identitas dan perlindungan login (DSM)

| Kontrol | Kemampuan | Sumber |
|---|---|---|
| **2FA** | Dapat **diwajibkan untuk pengguna/grup tertentu**; hanya administrator yang dapat menonaktifkan 2FA pengguna biasa; ada kode verifikasi darurat via email dan opsi *trust browser* | [RESMI] |
| **Adaptive MFA** | Dapat diaktifkan untuk semua pengguna atau hanya grup administrators | [RESMI] |
| **Account Protection** | Batas percobaan login, frekuensi, aturan pembatalan proteksi; gagal login dan gagal verifikasi identitas dihitung; mencakup DSM, File Station, **Synology Drive**, dan aplikasi mobile | [RESMI] |
| **Auto Block** | Memblokir IP setelah sejumlah gagal login dalam periode tertentu; mendukung daftar blokir/izin; mencakup antara lain DSM web, SSH, SMB, FTP, WebDAV, rsync, VPN | [RESMI] |
| **Firewall DSM** | Filter lalu lintas berdasar IP, rentang IP, port, atau lokasi; aksi default dan beberapa set aturan | [RESMI] |
| **Logout otomatis** | Default 15 menit tidak aktif; dapat diubah | [RESMI] |
| **Kebijakan password** | Panjang maks 127 karakter; masa berlaku 1–999 hari; pengingat ganti 1–99 hari | [RESMI] |
| **Prioritas izin aplikasi** | *Deny* mengalahkan *Allow* | [RESMI] |
| **Prioritas izin shared folder** | *No access* > *Read/Write* > *Read-only* | [RESMI] |

Terlihat pada POC [POC]: akun `admin` dinonaktifkan (baik), 2FA Disabled pada semua akun (tidak untuk produksi).

Rekomendasi [USULAN]:

1. Wajibkan 2FA untuk administrator dan pengguna yang boleh membuat link publik; targetkan seluruh pengguna.
2. Aktifkan Account Protection dan Auto Block; daftar IP kantor/VPN pada allow list.
3. Kebijakan password dan masa berlaku sesuai standar perusahaan.
4. Batasi anggota `administrators`; gunakan akun admin terpisah untuk operasi.

## 2. Pembatasan siapa yang boleh memakai Drive

Spesifikasi DSM menyatakan izin aplikasi memakai prioritas *Deny* mengalahkan *Allow* dan, untuk pengguna domain, Synology Drive, Synology Office, dan SMB membutuhkan **grup keamanan** [RESMI]. Ini mengindikasikan akses aplikasi dapat dibatasi per pengguna/grup. Apakah Synology Drive termasuk aplikasi yang dapat diatur lewat *Application Privileges* DSM dan/atau pengaturan Drive Admin Console, serta letak menu persisnya, **perlu diverifikasi [UJI]**.

## 3. Audit dan log

| Sumber log | Isi | Sumber |
|---|---|---|
| Web portal (aktivitas) | Operasi file, perubahan izin, rotasi versi | [RESMI] |
| Admin Console (sistem) | Gangguan layanan, kesehatan, kejadian, perubahan file, perubahan konfigurasi shared folder; dapat diekspor | [RESMI] |
| Klien | Unduh, hapus, ganti nama dipantau dan dicatat | [RESMI] |
| ShareSync | Peristiwa sinkron dapat difilter | [RESMI] |
| Laporan link berbagi | Ekspor untuk folder terpilih | [RESMI] |
| Laporan izin shared folder | Ekspor CSV (hingga 500.000 catatan per berkas) | [RESMI] |

Rekomendasi [USULAN]:

- Jadwalkan ekspor **laporan link berbagi** dan **laporan izin** (mis. bulanan) untuk review internal audit.
- Teruskan log ke penyimpanan terpisah (syslog/SIEM/FortiAnalyzer bila ada) agar tidak hilang bila akun admin NAS dibobol **[UJI]**.

## 4. Backup, snapshot, dan ketahanan

| Mekanisme | Fungsi | Sumber |
|---|---|---|
| **Hyper Backup** | Mencadangkan pengaturan dan data Synology Drive (lokal/jarak jauh) dan memulihkan ke titik sebelumnya | [RESMI] |
| **Snapshot** (Btrfs) | Snapshot dan replikasi untuk shared folder dan LUN | [RESMI] |
| **Versioning Drive** | Pemulihan titik waktu per file/folder | [RESMI] |
| **Recycle Bin** | Pemulihan penghapusan (admin untuk Team Folder) | [RESMI] |
| **WriteOnce** (Btrfs; model tertentu) | Data tak dapat diubah/dihapus selama retensi (Enterprise/Compliance); **tidak dapat dinonaktifkan setelah aktif**; tidak mendukung Recycle Bin | [RESMI] |
| **Enkripsi shared folder** | AES-256; kunci via passphrase atau Key Manager | [RESMI] |

Catatan:

- Sinkronisasi **bukan** backup: klien sinkron mereplikasi perubahan, termasuk yang merusak. Backup terpisah dan uji restore tetap wajib **[USULAN]**.
- WriteOnce bersifat permanen; pertimbangkan dengan sangat hati-hati sebelum diaktifkan.
- Enkripsi shared folder dapat memengaruhi fitur lain; uji kompatibilitas dengan Drive sebelum dipakai **[UJI]**.

## 5. Antivirus

Spesifikasi DSM mencantumkan paket **AntiVirus Essential (ClamAV)** dan **AntiVirus by McAfee** untuk pemindaian malware [RESMI]. Relevan bila pengguna dapat mengunggah file dari pihak luar lewat File Request. Cakupan dan kinerja dengan Drive **[UJI]**.
