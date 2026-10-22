# Sumber dan Keterbatasan

Seluruh sumber diakses pada **22 Oktober 2026**.

## Sumber resmi Synology

| Sumber | Dipakai untuk |
|---|---|
| [Synology Drive — Technical Specifications (DSM 7.4)](https://www.synology.com/en-global/dsm/7.4/software_spec/synology_drive) | Fitur Admin Console, versioning, pembatasan unduh/watermark, berbagi, file request, label, file locking, klien, batas dan prasyarat |
| [DSM 7.4 — Shared Folders](https://www.synology.com/en-us/dsm/7.4/software_spec/shared_folders) | Kuota shared folder (Btrfs), izin Read/Write/No access, ACL, WriteOnce, enkripsi, laporan izin |
| [DSM 7.4 — Account, Identity & Privileges](https://www.synology.com/en-us/dsm/7.4/software_spec/account_identity_privileges) | Batas pengguna/grup, kuota admin, prioritas izin, kebijakan password, Drive untuk pengguna domain |
| [DSM 7.4 — Security & Sign-in Protection](https://www.synology.com/en-us/dsm/7.4/software_spec/signin_protection) | 2FA, Adaptive MFA, Auto Block, Account Protection, firewall |
| [DSM 7.4 — Storage Management](https://www.synology.com/en-us/dsm/7.4/software_spec/storage_management) | Volume, Btrfs vs ext4, snapshot, fitur khusus Btrfs |

## Sumber komunitas

| Sumber | Dipakai untuk | Catatan |
|---|---|---|
| [NAS-Forum — Tutorial kuota DSM](https://www.nas-forum.com/forum/topic/60596-tuto-comprendre-et-utiliser-le-quota-dans-dsm) | Jenis kuota, dukungan Btrfs vs ext4, prioritas kuota, recycle bin dihitung | Ditulis untuk **DSM 6.2** (2018); verifikasi di DSM 7.x |

## Tidak dapat dibaca (perlu dibuka manual)

Halaman bantuan Synology Knowledge Center dimuat dengan JavaScript sehingga isinya tidak terbaca oleh alat riset. Disarankan membuka langsung:

- <https://kb.synology.com/en-global/DSM/help/SynologyDrive/drive_admin_console>
- <https://kb.synology.com/en-global/DSM/help/SynologyDrive/drive_desc?version=7>
- <https://kb.synology.com/en-af/DSM/help/DSM/AdminCenter/application_appprivilege>
- <https://kb.synology.com/en-af/DSM/help/DSM/AdminCenter/file_user_create?version=7>

## Catatan penggunaan

- Halaman spesifikasi merangkum fitur, bukan langkah konfigurasi. Letak menu dan opsi rinci perlu dikonfirmasi pada NAS (**[UJI]**).
- Perbandingan dengan Google Drive pada dokumen ini sengaja dibatasi pada hasil POC dan pernyataan pembuat POC; tidak ada klaim rinci tentang fitur Google Drive yang diverifikasi dalam riset ini.
