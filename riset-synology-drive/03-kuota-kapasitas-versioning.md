# 03 — Kuota, Kapasitas, dan Versioning

Topik ini menjawab bagian tantangan: **belum ada jatah kapasitas per departemen**.

## 1. Jenis kuota di DSM

| Jenis | Keterangan | File system | Sumber |
|---|---|---|---|
| **Kuota shared folder** | Membatasi total data dalam satu shared folder (termasuk Team Folder) | **Btrfs saja** | [RESMI] (spesifikasi Shared Folders: fitur Btrfs-dependent) |
| **Kuota pengguna pada shared folder** | Membatasi pemakaian per pengguna di dalam folder tertentu | Btrfs | [KOMUNITAS] (tutorial DSM 6.2) |
| **Kuota pengguna per volume** | Membatasi total pemakaian pengguna di satu volume | Btrfs dan ext4 | [KOMUNITAS] (tutorial DSM 6.2) |
| **Kuota grup** | Dijelaskan pada tutorial sebagai kuota grup pada shared folder; berlaku untuk seluruh anggota dan dapat ditimpa batas individu | Pada shared folder; dukungan file system tidak dinyatakan jelas oleh tutorial (kemungkinan Btrfs, karena kuota shared folder butuh Btrfs) | [KOMUNITAS] |

Aturan yang perlu diketahui:

- Anggota grup `administrators` memiliki kuota volume dan shared folder **tak terbatas** [RESMI] → akun harian jangan dijadikan administrator.
- Bila beberapa batas berlaku, urutan prioritas pada tutorial: shared folder → pengguna → grup [KOMUNITAS].
- Tanpa batas per pengguna, pengguna dalam satu folder berbagi total kuota folder; satu orang bisa menghabiskan ruang [KOMUNITAS].
- Di DSM 6.2, file di Recycle Bin dihitung dalam kuota shared folder [KOMUNITAS] → **verifikasi di DSM 7.x**.
- Menu: pada Btrfs, kuota shared folder ada di pengaturan lanjutan folder [KOMUNITAS]. Letak persis di DSM 7.x **[UJI]**.

> Sumber komunitas ini ditulis untuk DSM 6.2. Perilaku di DSM 7.x harus diverifikasi langsung pada NAS.

Pemantauan: mobile app menampilkan **penggunaan dan kuota per Team Folder**; admin dapat **menghitung penggunaan penyimpanan Drive** dan membersihkan recycle bin secara manual [RESMI].

## 2. Rancangan kuota departemen [USULAN]

1. Pastikan file system volume (Btrfs/ext4). Jika ext4, kuota shared folder tidak tersedia; pilih kuota pengguna per volume.
2. Ukur pemakaian saat ini per departemen (baseline).
3. Tetapkan kuota per Team Folder/shared folder departemen dengan faktor versi/recycle (lihat bawah).
4. Tetapkan batas per pengguna di dalam folder bila perlu (agar satu orang tidak menghabiskan ruang).
5. Sisakan cadangan kapasitas global; jangan menjual-lebih seluruh kapasitas.
6. Tinjau triwulan.

Rumus dan template: [../docs/06-rencana-implementasi-dan-kebutuhan-departemen.md](../docs/06-rencana-implementasi-dan-kebutuhan-departemen.md) bagian 3.

## 3. Versioning

| Parameter | Nilai | Sumber |
|---|---|---|
| Jumlah versi per file | Hingga 32 | [RESMI] |
| Deduplikasi | Antar versi | [RESMI] |
| Jendela retensi (rotasi) | 7, 30, 60, atau 120 hari | [RESMI] |
| Strategi retensi | FIFO, atau **Intelliversioning** (menyimpan versi signifikan) | [RESMI] |
| Pemulihan | File dan folder dapat dipulihkan ke titik waktu tertentu; *Version Explorer* untuk telusur/unduh/pulihkan dengan granularitas menit | [RESMI] |
| Cakupan | Diterapkan pada Team Folder | [RESMI] |

Dampak kapasitas: versi memakan ruang meski dideduplikasi → masukkan faktor versi pada kuota. Manfaat: pemulihan dari salah timpa atau enkripsi ransomware **sepanjang versi lama masih ada dan akun admin tidak diambil alih**.

## 4. Recycle bin

- Penghapusan dari Team Folder masuk Recycle Bin yang **hanya dapat diakses admin sistem** [RESMI].
- Admin dapat membersihkan recycle bin manual untuk membebaskan ruang [RESMI].
- Konsekuensi: pengguna tidak dapat memulihkan sendiri dari Team Folder → siapkan prosedur permintaan pemulihan ke IT **[USULAN]**.

## 5. Kapasitas volume (konteks)

- Hingga 256 volume; ukuran volume tunggal 10 GiB – 200 TiB (Btrfs mendukung hingga 1 PiB dengan opsi Petabyte); jenis RAID bergantung model [RESMI].
- Fitur khusus Btrfs: analisis penggunaan volume, snapshot dan replikasi, self-healing file, kuota shared folder [RESMI].

**Implikasi:** bila NAS perusahaan masih ext4, banyak fitur pengendalian (kuota shared folder, snapshot) tidak tersedia. Periksa lebih dulu — ini bisa menentukan kelayakan rancangan.
