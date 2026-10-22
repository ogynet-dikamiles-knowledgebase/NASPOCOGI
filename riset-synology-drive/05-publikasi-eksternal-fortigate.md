# 05 — Publikasi Eksternal dan Pertimbangan FortiGate

> Dokumen ini adalah **pertimbangan desain [USULAN]**. Isi di bawah memadukan fakta POC/dokumentasi Synology dengan praktik umum keamanan jaringan. Fitur FortiGate yang tersedia bergantung versi FortiOS dan lisensi; **validasi di perangkat yang dipakai** sebelum diterapkan.

## 1. Mengapa ini penting

Link publik hanya berguna bagi pihak luar bila layanan Drive **dapat dijangkau dari internet**. POC memakai `naspoc.ogy.my.id` dan link publik dapat dibuka dari luar (EV-11, EV-12) **[POC]**. Artinya, mengaktifkan jalur ini di produksi **menambah permukaan serangan** pada NAS perusahaan. Keputusan ini harus diambil oleh IT Network, bukan hanya diaktifkan di sisi aplikasi.

Jalur akses POC (reverse proxy, tunnel, atau port-forward) **tidak terlihat** pada evidence → mohon didokumentasikan.

## 2. Opsi publikasi

| Opsi | Uraian | Kelebihan | Kekurangan |
|---|---|---|---|
| **P0 — Tidak dipublikasikan** | Drive hanya via LAN/VPN. Link publik hanya berfungsi bagi yang terhubung | Paling aman | Tidak memenuhi kebutuhan berbagi ke pihak luar → risiko Google Drive tetap ada |
| **P1 — Publikasi terbatas lewat FortiGate** | NAS di segmen khusus (VLAN/DMZ); VIP (DNAT) 443 → NAS; firewall policy dengan profil keamanan; hanya hostname Drive dipublikasikan | Terkendali, terlihat di log FortiGate | Perlu desain, sertifikat, patch rutin |
| **P2 — Reverse proxy/WAF di depan NAS** | Reverse proxy (atau WAF) membatasi path dan memeriksa permintaan; FortiGate meneruskan ke proxy | Dapat membatasi jalur yang terbuka (mis. hanya path link publik) **[UJI]** | Komponen tambahan yang harus dikelola |

Diusulkan: mulai dari **P1** pada fase uji, evaluasi P2 bila jalur terbuka perlu dibatasi lebih ketat.

## 3. Pertimbangan desain di FortiGate

| Area | Pertimbangan |
|---|---|
| **Segmentasi** | Tempatkan NAS pada segmen/VLAN tersendiri; batasi akses dari dan ke segmen lain berdasarkan kebutuhan (least privilege) |
| **Publikasi** | Publikasikan hanya port HTTPS yang dibutuhkan; **jangan** mempublikasikan panel admin DSM ke internet; pakai hostname terpisah untuk Drive (POC sudah memakai host berbeda untuk DSM dan Drive) |
| **Kebijakan** | Terapkan profil keamanan sesuai lisensi (IPS, antivirus, filter web/DNS); batasi sumber (geografi/daftar) bila memungkinkan; pertimbangkan *DoS policy*/pembatasan laju |
| **TLS** | Sertifikat sah; nonaktifkan protokol/cipher usang di sisi NAS |
| **Inspeksi SSL** | Dapat membantu inspeksi tetapi menambah beban dan kompleksitas; putuskan setelah uji kinerja **[UJI]** |
| **Log** | Aktifkan log lalu lintas pada policy; teruskan ke FortiAnalyzer/syslog; korelasikan dengan log Drive |
| **Pemantauan** | Alarm untuk lonjakan unduh, banyak percobaan login gagal, akses dari lokasi tak lazim |
| **Patch** | Jadwal patch untuk FortiOS, DSM, dan Drive Server |

## 4. Kontrol di sisi NAS yang melengkapi

Lihat [04-keamanan-audit-dan-backup.md](04-keamanan-audit-dan-backup.md): 2FA yang diwajibkan, Account Protection (mencakup Drive), Auto Block, firewall DSM, masa berlaku/password pada link publik, laporan link berbagi, pembatasan unduh/watermark.

**Pertahanan berlapis:** FortiGate membatasi *siapa dan apa* yang bisa menjangkau NAS; NAS membatasi *siapa yang boleh melakukan apa* setelah sampai.

## 5. Uji yang disarankan sebelum produksi [UJI]

1. Buka link publik dari jaringan eksternal → hanya konten yang dimaksud yang terlihat.
2. Coba akses panel admin DSM dari internet → harus **tidak** dapat dijangkau.
3. Simulasikan percobaan login berulang → pastikan Auto Block/Account Protection bekerja dan tercatat.
4. Verifikasi log di FortiGate dan di Drive saling bersesuaian untuk satu aksi unduh.
5. Uji kinerja unduh besar dan dampaknya ke FortiGate (CPU, sesi) bila inspeksi SSL diaktifkan.
