# NASPOCOGI — POC Synology Drive sebagai Pengganti Pola Berbagi File via Google Drive

> Jurnal, jejak pengujian, dan knowledge base untuk Proof of Concept (POC) pemanfaatan NAS Synology perusahaan melalui paket **Synology Drive**.
> Status dokumen: **Draft untuk diskusi** · Tanggal: 22 Oktober 2026 · Penyusun POC: Bragy (SPV IT Network)
> Dokumen ini disusun dengan bantuan Claude (AI). Semua klaim diberi label tingkat keyakinan (lihat bagian *Cara membaca label*).

## Ringkasan singkat

| | |
|---|---|
| **Masalah** | Internal audit masih menemukan kasus berbagi folder lewat Google Drive sehingga data dikhawatirkan keluar dari kendali perusahaan. NAS perusahaan belum punya aturan kuota per departemen maupun aturan siapa yang boleh memakainya. |
| **Langkah proaktif IT Support** | Memfungsikan NAS sebagai share folder SMB biasa, seluruh user dikelola lewat grup izin per departemen. |
| **Pertanyaan POC** | Apakah Synology Drive (paket native di NAS yang sama) dapat menggantikan kebutuhan "ala Google Drive" — berbagi antar user, antar divisi, dan ke pihak luar — dengan kendali penuh di sisi perusahaan? |
| **Hasil utama** | Fitur dasar Drive, berbagi folder/file antar user (termasuk lintas divisi), dan berbagi publik via link (dengan password dan masa berlaku) **berjalan** di POC. Berbagi publik **tidak 100% sama** dengan Google Drive: pengunjung publik hanya dapat preview/unduh, tidak dapat membuat folder atau mengganti nama. |
| **Rekomendasi awal (usulan)** | Model **hibrida**: SMB tetap untuk kebutuhan yang sudah berjalan, Synology Drive (khususnya Team Folder) untuk kolaborasi dan berbagi, dengan kuota, peran, 2FA, dan masa berlaku link ditetapkan sebagai kebijakan. |
| **Butuh keputusan/dukungan** | Kuota per departemen, siapa yang boleh membuat link publik, klasifikasi data, dan desain publikasi eksternal lewat FortiGate. Lihat [docs/06](docs/06-rencana-implementasi-dan-kebutuhan-departemen.md). |

## Struktur repo

```
NASPOCOGI/
├── README.md                          ← Anda di sini
├── reports/
│   └── Laporan-POC-Synology-Drive.pdf ← Laporan lengkap (PDF) dengan evidence
├── docs/                              ← Dokumen POC dan rencana
│   ├── 01-latar-belakang-dan-tujuan.md
│   ├── 02-kondisi-saat-ini-vs-usulan.md
│   ├── 03-hasil-poc.md
│   ├── 04-pembagian-tanggung-jawab.md
│   ├── 05-risiko-dan-mitigasi.md
│   ├── 06-rencana-implementasi-dan-kebutuhan-departemen.md
│   └── 07-panduan-demo.md
├── riset-synology-drive/              ← Hasil penggalian informasi Synology Drive (terpisah per topik)
│   ├── README.md
│   ├── 01-arsitektur-dan-fitur.md
│   ├── 02-peran-izin-dan-berbagi.md
│   ├── 03-kuota-kapasitas-versioning.md
│   ├── 04-keamanan-audit-dan-backup.md
│   ├── 05-publikasi-eksternal-fortigate.md
│   ├── 06-uji-lanjutan-dan-pertanyaan-terbuka.md
│   └── sumber.md
└── evidence/                          ← 12 screenshot POC + indeks
    └── README.md
```

## Cara membaca label tingkat keyakinan

| Label | Arti |
|---|---|
| **[POC]** | Terlihat langsung pada screenshot evidence POC |
| **[RESMI]** | Tercantum pada halaman spesifikasi resmi Synology (diakses 22 Okt 2026) |
| **[KOMUNITAS]** | Dari sumber komunitas/forum; perlu diverifikasi di DSM versi yang dipakai |
| **[KETERANGAN POC]** | Disampaikan pembuat POC, belum ada screenshot di lampiran |
| **[UJI]** | Belum terverifikasi; perlu diuji di lingkungan POC sebelum diandalkan |
| **[USULAN]** | Rekomendasi penyusun; membutuhkan keputusan |

## Demo langsung

Lingkungan demo: <https://naspoc.ogy.my.id/> — akun `UserA` dan `UserB`. Password diberikan secara pribadi (japri) oleh pembuat POC. Panduan skenario demo: [docs/07-panduan-demo.md](docs/07-panduan-demo.md).

> Lingkungan POC adalah **lingkungan pribadi** milik Bragy. Jangan mengunggah data perusahaan ke lingkungan demo.

## Pembaruan

| Tanggal | Perubahan |
|---|---|
| 2026-10-22 | Versi awal: laporan POC, evidence, dan riset Synology Drive |
