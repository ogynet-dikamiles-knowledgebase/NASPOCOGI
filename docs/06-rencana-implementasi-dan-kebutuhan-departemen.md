# 06 — Rencana Implementasi dan Kebutuhan dari Departemen

> Seluruh isi dokumen ini adalah **[USULAN]** untuk didiskusikan. Durasi dan angka final ditetapkan bersama pemilik proses.

## 1. Keputusan yang dibutuhkan

| # | Keputusan | Pemutus yang disarankan | Pilihan/Catatan |
|---|---|---|---|
| K1 | Arah: SMB saja, Drive penuh, atau hibrida | Manajemen + IT | Diusulkan hibrida (lihat [02](02-kondisi-saat-ini-vs-usulan.md)) |
| K2 | Siapa yang boleh memakai NAS/Drive | Manajemen + Kepala divisi | Berbasis grup divisi; daftar anggota disetujui kepala divisi |
| K3 | Kuota per departemen/Team Folder | Manajemen + IT + Kepala divisi | Lihat metode di bagian 3 |
| K4 | Siapa yang boleh membuat link publik | Manajemen + Internal Audit | Diusulkan: pengguna tertentu, 2FA wajib |
| K5 | Batas masa berlaku link publik | Internal Audit + IT | Contoh: 7 atau 30 hari |
| K6 | Klasifikasi data yang boleh/tidak boleh dibagikan keluar | Legal/Compliance + Pemilik data | Data tertentu hanya boleh internal |
| K7 | Desain publikasi eksternal lewat FortiGate | IT Network | Lihat [riset/05](../riset-synology-drive/05-publikasi-eksternal-fortigate.md) |
| K8 | Retensi versi/recycle bin dan strategi backup | IT + Pemilik data | Versi: 7/30/60/120 hari [RESMI] |

## 2. Tahapan

| Fase | Fokus | Keluaran | Kriteria selesai |
|---|---|---|---|
| **0. Stabilkan existing** | Rapikan SMB: audit izin grup, daftar user yang berhak, pemilik tiap folder, ukur pemakaian saat ini; 2FA untuk admin | Daftar folder ↔ pemilik ↔ grup; baseline pemakaian | Semua folder punya pemilik; tidak ada akun/izin tanpa pemilik |
| **1. Lanjutkan POC** | Tuntaskan [uji lanjutan](../riset-synology-drive/06-uji-lanjutan-dan-pertanyaan-terbuka.md): Team Folder, kuota, versioning, file request, log, restore, uji akses dari luar | Laporan POC fase 2 | Seluruh [UJI] kritis terjawab |
| **2. Pilot terbatas** | 1–2 departemen, data nyata non-sensitif, kuota awal, kebijakan sementara | Umpan balik pengguna, metrik | Tidak ada kasus Google Drive baru di departemen pilot; kepuasan memadai |
| **3. Rollout bertahap** | Kebijakan resmi disetujui; pelatihan; migrasi bertahap | SOP resmi, kuota ditetapkan | Departemen terkait berjalan di jalur resmi |
| **4. Operasi dan tinjauan** | Review akses dan link berkala; kapasitas; audit | Laporan triwulan | Link publik tanpa masa berlaku = 0; kuota terpantau |

## 3. Metode menetapkan kuota

Bentuk umum (isi angka dari data nyata, bukan dari asumsi):

```
Kuota_dept = (Data_saat_ini + Pertumbuhan_12_bulan) × (1 + Faktor_versi_dan_recycle)
Total semua kuota ≤ Kapasitas_usable_volume − Cadangan_global
```

Hal yang perlu dipertimbangkan:

- **Versi file**: sampai 32 versi per file (terdeduplikasi lintas versi) dan retensi 7/30/60/120 hari [RESMI] → tambah faktor ruang.
- **Recycle bin** ikut memakai ruang; pada Team Folder hanya admin yang dapat mengaksesnya [RESMI]. Di DSM 6.2, file di recycle bin dihitung dalam kuota shared folder [KOMUNITAS — verifikasi di DSM 7].
- **Kuota shared folder membutuhkan volume Btrfs** [RESMI]; kuota pengguna per volume berlaku juga di ext4 [KOMUNITAS]. Cek file system NAS perusahaan dahulu.
- Anggota grup `administrators` tidak dibatasi kuota [RESMI] → jangan jadikan akun harian sebagai administrator.

Template tabel kuota (diisi bersama pemilik data):

| Departemen | Jumlah user | Data saat ini | Perkiraan tumbuh 12 bln | Faktor versi/recycle | Kuota usulan | Pemilik data |
|---|---|---|---|---|---|---|
| Divisi A | [isi] | [isi] | [isi] | [isi] | [isi] | [isi] |
| Divisi B | [isi] | [isi] | [isi] | [isi] | [isi] | [isi] |
| … | | | | | | |

## 4. Dukungan yang dibutuhkan dari departemen

| Departemen/Peran | Dukungan yang dibutuhkan | Untuk keputusan |
|---|---|---|
| **Manajemen** | Persetujuan arah dan kebijakan; sponsor perubahan | K1, K2, K4 |
| **Internal Audit** | Kriteria kontrol yang dianggap memadai (mis. masa berlaku link, review akses); ikut meninjau hasil pilot | K4, K5 |
| **Legal / Compliance** | Klasifikasi data; aturan data keluar; ketentuan retensi | K6, K8 |
| **HR** | Proses onboarding/offboarding akun; sosialisasi dan konsekuensi kebijakan | Aturan operasional #7 |
| **Kepala divisi (data owner)** | Daftar anggota dan peran; penanggung jawab folder; estimasi kebutuhan kapasitas | K2, K3 |
| **Finance / Pengadaan** | Anggaran ekspansi kapasitas, backup (NAS kedua/cloud), lisensi bila diperlukan | K3, K8 |
| **IT Support** | Operasional harian akun, grup, dukungan pengguna | Fase 0–4 |
| **Pengguna pilot** | Menjalankan skenario nyata dan memberi umpan balik | Fase 2 |

## 5. Indikator keberhasilan (usulan)

- Jumlah kasus berbagi data via layanan di luar kendali perusahaan pada temuan audit berikutnya menurun menuju nol.
- Link publik aktif tanpa masa berlaku = 0.
- Seluruh Team Folder punya pemilik, kuota, dan jadwal review akses.
- Uji restore berhasil sesuai jadwal.
- Waktu IT untuk membuat tautan manual = 0 (pengguna berwenang mengelola sendiri).
