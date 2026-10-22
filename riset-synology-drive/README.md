# Riset Synology Drive — Fokus Kebutuhan POC

Hasil penggalian informasi tentang Synology Drive, **dibatasi pada hal yang relevan dengan kebutuhan saat ini**: berbagi file/folder yang terkendali, pengelolaan akses dan kuota per departemen, keamanan, audit, dan publikasi eksternal.

Tanggal riset: 22 Oktober 2026. Versi yang dirujuk: halaman spesifikasi resmi **DSM 7.4** (halaman yang sama juga mencantumkan DSM 7.3 dan 7.2 sebagai versi server yang didukung).

## Isi

| Berkas | Topik |
|---|---|
| [01-arsitektur-dan-fitur.md](01-arsitektur-dan-fitur.md) | Komponen Synology Drive, My Drive vs Team Folder, klien, prasyarat |
| [02-peran-izin-dan-berbagi.md](02-peran-izin-dan-berbagi.md) | Peran berbagi, link internal vs link publik, File Request, label, kontrol admin |
| [03-kuota-kapasitas-versioning.md](03-kuota-kapasitas-versioning.md) | Kuota DSM, versi file, recycle bin, perencanaan kapasitas |
| [04-keamanan-audit-dan-backup.md](04-keamanan-audit-dan-backup.md) | 2FA, Account Protection, Auto Block, log, backup, snapshot |
| [05-publikasi-eksternal-fortigate.md](05-publikasi-eksternal-fortigate.md) | Pertimbangan desain bila link publik harus dapat dibuka dari internet |
| [06-uji-lanjutan-dan-pertanyaan-terbuka.md](06-uji-lanjutan-dan-pertanyaan-terbuka.md) | Daftar uji dan pertanyaan yang belum terjawab |
| [sumber.md](sumber.md) | Daftar sumber dan keterbatasan riset |

## Keterbatasan riset (penting)

Halaman bantuan Synology Knowledge Center (`kb.synology.com`) dimuat dengan JavaScript sehingga isi artikelnya **tidak dapat dibaca** oleh alat riset yang dipakai. Karena itu rujukan utama adalah **halaman spesifikasi resmi Synology** (yang dapat dibaca) dan satu tutorial komunitas untuk kuota. Hal yang bergantung pada letak menu atau opsi persis di antarmuka diberi label **[UJI]** dan perlu diverifikasi langsung di Drive Admin Console/DSM pada NAS.

## Label

Sama seperti README utama: **[POC]**, **[RESMI]**, **[KOMUNITAS]**, **[KETERANGAN POC]**, **[UJI]**, **[USULAN]**.
