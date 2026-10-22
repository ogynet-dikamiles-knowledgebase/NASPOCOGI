# 02 — Peran, Izin, dan Berbagi

## 1. Dua jenis tautan

| | Directory Link (internal) | Public Link |
|---|---|---|
| Pola URL pada POC | `/d/f/<token>` | `/d/s/<token>` |
| Siapa yang dapat membuka | Hanya invitee (butuh login) | Siapa pun yang memegang link (opsional password) |
| Mode privasi | *Private – Only invitees can access* | *Anyone with the link can …* (pada screenshot: *can edit*) |
| Kontrol | Peran per invitee | Password, masa berlaku, tingkat akses |
| Evidence | EV-05..EV-08 | EV-10..EV-12 |

[POC]

## 2. Peran berbagi (invitee)

| Peran | Hak | Evidence |
|---|---|---|
| **Previewer** | Preview | EV-05 |
| **Viewer** | Preview, Download | EV-06 |
| **Editor** | Preview, Comment, Download, Upload, Edit | EV-07 |
| **Manager** | Preview, Comment, Download, Upload, Edit, Delete, Share | EV-08 |

[POC] — diambil dari tooltip UI.

Catatan:

- *Viewer* tidak memiliki *Comment*, sedangkan *Editor* memilikinya.
- Hanya *Manager* yang dapat **Delete** dan **Share**.
- Invitee dapat berupa **User/Group** (kolom input "User/Group" pada dialog) [POC] → grup divisi dapat dipakai langsung.

Rekomendasi pemakaian [USULAN]:

| Kebutuhan | Peran |
|---|---|
| Hanya boleh melihat tanpa menyalin | Previewer |
| Boleh melihat dan mengunduh | Viewer |
| Kolaborasi | Editor |
| Pemilik/penanggung jawab data | Manager |

## 3. Link publik

Yang terlihat pada POC [POC]:

- Opsi *Create a public link to share files with anyone*.
- *Privacy Settings* (dipilih: *Anyone with the link can edit*).
- *Password Protection* (*Require password*).
- *Link Expiration* (*Expire on*, tanggal).
- Tooltip: *izin folder diwariskan ke file di dalam direktorinya saat diakses lewat link publik*.

Yang dinyatakan resmi [RESMI]: link publik dapat diberi password dan masa berlaku (web portal, mobile, dan admin); laporan link berbagi untuk folder terpilih dapat diekspor.

Pengamatan perilaku pengunjung publik [POC]/[KETERANGAN POC]: preview, atau preview + unduh; **tidak dapat** membuat folder/mengganti nama.

Yang belum diketahui/diuji [UJI]:

- Daftar lengkap opsi *Privacy Settings* untuk link publik dan arti masing-masing.
- Apakah file yang ditambahkan ke folder **setelah** link dibuat otomatis terpapar.
- Apakah admin dapat **mewajibkan** password/masa berlaku atau menetapkan batas maksimum masa berlaku secara teknis (bila tidak, aturan harus melalui SOP dan audit laporan link).
- Apakah dapat membatasi **siapa** yang boleh membuat link publik (spesifikasi menyatakan admin dapat mengizinkan non-admin mengatur izin berbagi — cek apakah dapat dibedakan antara berbagi internal dan link publik).

## 4. File Request

Fungsi untuk **menerima berkas dari pihak luar** tanpa memberi akses ke folder. Ketersediaan: web portal "collect files from external users via file requests" [RESMI]; admin dapat mengizinkan non-admin membuat file request dengan opsi password dan masa berlaku [RESMI].

Relevansi: menjawab kebutuhan "terima dokumen dari vendor/klien" tanpa Google Drive. **Belum diuji di POC** [UJI] — sertakan di uji lanjutan.

## 5. Label

Label pribadi dan label bersama; admin mengelola label bersama, dapat memberi hak membuat label kepada non-admin, dan memindahkan kepemilikan label [RESMI]. Berguna untuk klasifikasi sederhana (mis. "Internal", "Rahasia") tetapi **bukan** mekanisme pengendalian akses.

## 6. Kontrol tambahan oleh admin

| Kontrol | Cakupan | Sumber |
|---|---|---|
| Pembatasan unduh | Per shared folder; hanya untuk non-admin | [RESMI] |
| Watermark | Per shared folder; teks hingga 32 karakter (isi, warna, sudut, transparansi dapat diatur); file ≤100 MB; jenis file tertentu | [RESMI] |
| Izin berbagi non-admin | Admin dapat mengizinkan non-admin mengatur izin berbagi dan membuat file request | [RESMI] |
| Laporan link berbagi | Ekspor untuk folder terpilih | [RESMI] |
| File locking | Otomatis/manual; admin dapat membuka paksa | [RESMI] |
| Pemutusan klien & hapus jarak jauh | Dari daftar koneksi klien | [RESMI] |

Catatan: pembatasan unduh **tidak** berlaku untuk admin, dan watermark tidak berlaku pada tugas sinkron [RESMI]. Karena itu, kontrol ini melengkapi — bukan menggantikan — kebijakan peran dan pembatasan akun admin.
