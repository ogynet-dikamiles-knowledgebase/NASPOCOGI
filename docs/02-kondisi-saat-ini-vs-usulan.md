# 02 — Kondisi Saat Ini vs Usulan

## 1. Kondisi saat ini (existing)

| Aspek | Kondisi |
|---|---|
| Layanan NAS | DSM dengan cara kerja **SMB ke endpoint user** |
| Pengelompokan | Grup per departemen dengan permission grup pada share folder |
| Kapasitas | Belum ada jatah/kuota yang ditetapkan per departemen atau user |
| Hak akses | Belum ada aturan tegas siapa saja yang boleh memakai NAS |
| Berbagi antar divisi | Mengandalkan permission folder (butuh IT untuk mengubah) |
| Berbagi ke pihak luar | Tidak ada jalur resmi → **hipotesis**: pengguna beralih ke Google Drive |
| Temuan audit | Masih ada kasus berbagi folder memakai Google Drive |

> "Hipotesis" di atas belum diverifikasi dengan wawancara pengguna. Disarankan memvalidasinya (lihat [06](06-rencana-implementasi-dan-kebutuhan-departemen.md), bagian kebutuhan dari departemen).

## 2. Perbandingan pendekatan

| Aspek | Existing: SMB + grup | Synology Drive | Catatan |
|---|---|---|---|
| Pengalaman pengguna | Seperti folder jaringan | Web portal, klien desktop/mobile, mirip Google Drive | [RESMI] |
| Berbagi ke rekan (satu/lintas departemen) | Lewat perubahan permission oleh IT | Pemilik berbagi sendiri ke user/grup dengan peran | [POC] EV-05..EV-09 |
| Berbagi ke pihak luar | Tidak tersedia | Link publik dengan password dan masa berlaku | [POC] EV-10; [RESMI] |
| Kontrol peran | Read/Write/No access | Previewer, Viewer, Editor, Manager | [POC] EV-05..EV-08 |
| Versi file | Tidak ada bawaan | Hingga 32 versi per file, retensi 7/30/60/120 hari | [RESMI] |
| Kuota | Perlu dirancang (DSM) | Perlu dirancang (DSM); mobile app menampilkan kuota Team Folder | [RESMI] [KOMUNITAS] |
| Audit/log | Log DSM/SMB | Log Drive: operasi file, perubahan izin, rotasi versi; laporan link berbagi dapat diekspor | [RESMI] |
| Kebijakan unduh/watermark | Tidak ada | Per shared folder, hanya berlaku untuk non-admin | [RESMI] |
| Kebergantungan jaringan | LAN/VPN | Web/klien; link publik butuh endpoint yang dapat dijangkau pihak luar | [POC] |

## 3. Opsi arah

| Opsi | Uraian | Kelebihan | Kekurangan/Risiko |
|---|---|---|---|
| **A. SMB saja (diperketat)** | Tetap SMB, perketat grup, tambah kuota | Perubahan paling kecil; familiar | Tidak menjawab kebutuhan berbagi cepat dan ke pihak luar → risiko Google Drive tetap ada |
| **B. Drive untuk semua** | Semua data pindah ke Synology Drive | Satu alur, kontrol terpusat | Migrasi besar; kompatibilitas aplikasi/skrip yang bergantung pada SMB; kapasitas versi bertambah |
| **C. Hibrida [USULAN]** | SMB untuk data/aplikasi yang sudah berjalan; Drive (My Drive + Team Folder) untuk kolaborasi dan berbagi | Menjawab kebutuhan berbagi tanpa memutus yang sudah berjalan; migrasi bertahap | Dua jalur akses harus dikelola; perlu aturan jelas data mana di mana; kompatibilitas SMB dan Drive pada folder yang sama **[UJI]** |

**Arah yang diusulkan: Opsi C**, dimulai dari pilot 1–2 departemen. Alasan: menjawab tantangan inti (kendali + kemudahan) dengan risiko transisi paling kecil. Keputusan akhir berada pada pimpinan dan pemilik data.

## 4. Prinsip rancangan yang diusulkan

1. **Data bisnis di Team Folder** (dimiliki organisasi, izin per grup, versi dan recycle bin dapat dikendalikan admin); **My Drive untuk kerja pribadi/sementara**. Alasan: file di My Drive dimiliki pengguna, sehingga rentan "yatim" saat pengguna pindah/keluar **[UJI]**.
2. **Peran paling kecil yang cukup**: default *Viewer*; *Editor* untuk kolaborator; *Manager* hanya pemilik data.
3. **Link publik = pengecualian**, bukan default: wajib password dan masa berlaku (lewat SOP; penegakan teknis perlu dicek **[UJI]**), ditinjau berkala lewat laporan link berbagi.
4. **Identitas kuat**: 2FA diwajibkan minimal untuk admin dan pengguna yang boleh membuat link publik.
5. **Kuota eksplisit** per departemen/Team Folder dan dipantau.
6. **Dapat ditelusuri**: log Drive/DSM dikirim ke penyimpanan log yang tidak bisa diubah pengguna biasa **[UJI]**.
