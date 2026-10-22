# 05 — Risiko dan Mitigasi

Tujuan dokumen ini: **mengidentifikasi dan mengantisipasi risiko sebelum berdampak ke bisnis**. Penilaian kemungkinan/dampak adalah **penilaian awal penyusun** dan perlu dikaji bersama pemilik proses.

Skala: **R** = Rendah, **S** = Sedang, **T** = Tinggi.

| ID | Risiko | Indikasi/Penyebab | Kemungkinan | Dampak | Mitigasi | Status verifikasi |
|---|---|---|---|---|---|---|
| R01 | Data bocor via link publik | Link tanpa password/masa berlaku; link folder induk mewariskan izin ke seluruh isi | S | T | SOP: wajib password + masa berlaku; bagikan file/folder khusus, bukan induk; tinjau berkala laporan link berbagi; batasi siapa yang boleh membuat link publik | Fitur laporan link: [RESMI]. Penegakan wajib password/expiry secara teknis: [UJI] |
| R02 | Pengguna kembali ke Google Drive (shadow IT) | Pengalaman kurang nyaman; akses publik tidak 100% sama; tidak paham jalurnya | T | T | Sosialisasi + demo; sediakan jalur resmi (link publik, file request); kumpulkan umpan balik pilot; kebijakan resmi + sanksi sesuai HR | [UJI] lewat pilot |
| R03 | Akun diambil alih | Password lemah; 2FA tidak aktif (POC: semua Disabled) | S | T | Wajibkan 2FA minimal admin dan pemilik link publik; kebijakan password; Account Protection (mencakup Synology Drive) dan Auto Block | 2FA per user/grup, Account Protection, Auto Block: [RESMI] |
| R04 | NAS terekspos ke internet | Link publik membutuhkan endpoint yang dapat dijangkau pihak luar | S | T | Desain di FortiGate: segmen khusus, VIP+policy dengan profil keamanan, batasi geo/sumber, TLS sah, jangan publikasikan panel admin DSM, log terpusat, patch rutin | Pertimbangan desain: [USULAN]; lihat [riset/05](../riset-synology-drive/05-publikasi-eksternal-fortigate.md) |
| R05 | Kapasitas habis / tidak adil antar departemen | Belum ada kuota; versi file (hingga 32/file) dan recycle bin memakai ruang | T | S | Tetapkan kuota per departemen/Team Folder; pantau pemakaian; atur kebijakan versi; sisakan cadangan kapasitas | Kuota shared folder butuh Btrfs [RESMI]; perilaku kuota [KOMUNITAS, DSM 6.2] |
| R06 | Kehilangan data (hapus tak sengaja, ransomware, NAS rusak) | Satu NAS = titik kegagalan tunggal; klien sync mereplikasi perubahan termasuk yang merusak | S | T | Hyper Backup untuk data+pengaturan Drive; snapshot (Btrfs); versioning; recycle bin; uji restore berkala; prinsip 3-2-1 | Hyper Backup mencakup Drive: [RESMI]; snapshot butuh Btrfs: [RESMI] |
| R07 | Data "yatim" saat karyawan keluar/pindah | Data bisnis hanya di My Drive milik pengguna | S | S | Data bisnis di Team Folder; prosedur offboarding; uji perilaku share saat akun dinonaktifkan | [UJI] |
| R08 | Privilege creep (peran berlebih) | Banyak Manager/Editor yang tidak perlu | S | S | Default Viewer; review akses berkala bersama pemilik data; deskripsi grup berisi pemilik | [USULAN] |
| R09 | Audit trail tidak memadai | Log hanya di NAS; bisa dihapus jika akun admin diambil alih | R | T | Gunakan log Drive (operasi file, perubahan izin, rotasi versi); ekspor/teruskan ke penyimpanan log terpisah (syslog/SIEM) | Isi log: [RESMI]; forwarding: [UJI] |
| R10 | Batas klien/kinerja | Batas 500.000 file per klien; koneksi klien bersamaan tergantung model NAS | R | S | Pilot dengan data nyata; cek spesifikasi model NAS; ukur beban | [RESMI] batas; hasil nyata [UJI] |
| R11 | Konflik SMB dan Drive pada folder yang sama | Dua jalur akses ke data yang sama (hibrida) | S | S | Aturan data mana di jalur mana; uji sebelum rollout | [UJI] |
| R12 | Ketergantungan versi & patch | Drive Server dan klien harus kompatibel (mis. Drive Server 3.0+ dengan klien 3.0+; file locking butuh klien 4.0.0+) | S | S | Jadwal patch DSM/Drive; matriks versi klien; uji sebelum update | [RESMI] |
| R13 | Salah ekspektasi fitur publik | Pengguna mengira sama dengan Google Drive (mis. mengedit/buat folder lewat link) | T | R | Panduan singkat + tabel perbedaan; demo | [POC]/[KETERANGAN POC] |

## Hal yang sudah baik pada POC

- Akun `admin` bawaan **dinonaktifkan** (EV-01).
- Folder dibagikan dengan mode **Private — Only invitees can access** (EV-05..EV-08).
- Link publik memakai **password dan masa berlaku** (EV-10).

## Hal yang tidak boleh terbawa ke produksi

- 2FA **Disabled** pada semua akun (EV-01).
- Password link publik yang sangat lemah (EV-10).
- Pengaturan *"Anyone with the link can edit"* sebagai pilihan default (EV-10) — untuk pihak luar, mulai dari akses paling kecil (preview/unduh) dan naikkan hanya bila dibutuhkan.
