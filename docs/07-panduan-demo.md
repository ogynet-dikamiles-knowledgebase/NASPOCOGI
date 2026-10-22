# 07 — Panduan Demo

Tujuan: memvisualisasikan cara kerja dan pemanfaatan NAS agar lebih maksimal. Durasi sekitar 10–15 menit.

## Akses

| | |
|---|---|
| URL | <https://naspoc.ogy.my.id/> |
| Akun | `UserA`, `UserB` |
| Password | Diberikan secara pribadi (japri) oleh pembuat POC |

> Lingkungan pribadi milik Bragy. **Jangan unggah data perusahaan.** Link publik contoh POC berakhir pada 23 Okt 2026.
> Gunakan dua sesi browser terpisah (mis. satu jendela biasa dan satu jendela Incognito) agar UserA dan UserB dapat tampil bersamaan.

## Skenario

1. **Struktur** — Tunjukkan konsep: grup per divisi → pengguna. (EV-01, EV-02)
2. **My Drive** — Login UserA, tunjukkan folder dan file; jelaskan kemiripan dengan Google Drive. (EV-03)
3. **Berbagi antar divisi** — UserA klik *Share* pada folder → tambah `UserB` → tunjukkan 4 peran dan hak masing-masing → Save. (EV-05..EV-08)
4. **Sisi penerima** — Login UserB (Incognito) → *Shared with me* → file milik UserA muncul. (EV-09)
5. **Peran berbeda, hasil berbeda** — Ubah peran UserB (Previewer → Viewer → Editor) dan tunjukkan perbedaan tombol yang aktif.
6. **Berbagi ke luar** — UserA pilih file → *Public Link* → centang password dan masa berlaku → salin link. (EV-10)
7. **Pengunjung tanpa akun** — Buka link di jendela baru: hanya *Preview/Download*; tidak ada pembuatan folder/ganti nama. (EV-11, EV-12)
8. **Cabut akses** — UserA hapus invitee atau matikan link publik; tunjukkan akses hilang.
9. **Penutup** — Sampaikan peran IT vs pengguna ([04](04-pembagian-tanggung-jawab.md)) dan hal yang butuh keputusan ([06](06-rencana-implementasi-dan-kebutuhan-departemen.md)).

## Hal yang perlu disampaikan secara jujur kepada audiens

- Berbagi publik **tidak 100% sama** dengan Google Drive (pengunjung hanya preview/unduh).
- Team Folder, kuota, versioning, log, dan backup **belum diuji** di POC ini.
- Publikasi ke internet untuk produksi perlu **desain keamanan di FortiGate** terlebih dahulu.
