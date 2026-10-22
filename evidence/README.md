# Evidence POC

12 screenshot dari lingkungan POC, diambil 22 Oktober 2026 (zona waktu WIB). Waktu pada kolom *Diambil* berasal dari nama berkas screenshot asli.

## Pengolahan

- Tab, bookmark, dan bilah browser **dipotong** agar hanya area aplikasi yang tampil.
- Pada **EV-10**, nilai kolom password **disamarkan** ("disamarkan"); kotak centang *Require password* tetap terlihat.
- Tidak ada pengubahan lain. Berkas asli (resolusi penuh) tetap berada pada pembuat POC.

## Indeks

| ID | Berkas | Diambil | Pengguna/Konteks | Isi |
|---|---|---|---|---|
| EV-01 | [EV-01_dsm-daftar-user.png](EV-01_dsm-daftar-user.png) | 21:37:53 | DSM Control Panel → User (host `nas.ogy.my.id`) | Akun `admin` (Deactivated), `UserA`, `UserB`; 2FA Disabled |
| EV-02 | [EV-02_dsm-daftar-grup.png](EV-02_dsm-daftar-grup.png) | 21:38:04 | DSM Control Panel → Group | `Grup_DIVISI_A`, `Grup_DIVISI_B` |
| EV-03 | [EV-03_drive-userA-my-drive.png](EV-03_drive-userA-my-drive.png) | 21:35:59 | Synology Drive, UserA (host `naspoc.ogy.my.id`) | My Drive → `MyDrive_dari userA`, 4 file PNG |
| EV-04 | [EV-04_drive-userB-my-drive.png](EV-04_drive-userB-my-drive.png) | 21:35:41 | Synology Drive, UserB (Incognito) | My Drive → `MyDrive_dari userB`, 4 file PNG |
| EV-05 | [EV-05_share-peran-previewer.png](EV-05_share-peran-previewer.png) | 21:49:15 | UserA, dialog Share | Peran Previewer = Preview |
| EV-06 | [EV-06_share-peran-viewer.png](EV-06_share-peran-viewer.png) | 21:49:59 | UserA, dialog Share | Peran Viewer = Preview, Download |
| EV-07 | [EV-07_share-peran-editor.png](EV-07_share-peran-editor.png) | 21:50:08 | UserA, dialog Share | Peran Editor = Preview, Comment, Download, Upload, Edit |
| EV-08 | [EV-08_share-peran-manager.png](EV-08_share-peran-manager.png) | 21:50:15 | UserA, dialog Share | Peran Manager = Preview, Comment, Download, Upload, Edit, Delete, Share |
| EV-09 | [EV-09_drive-userB-shared-with-me.png](EV-09_drive-userB-shared-with-me.png) | 21:50:53 | UserB (Incognito) | *Shared with me* → file milik UserA muncul |
| EV-10 | [EV-10_public-link-pengaturan.png](EV-10_public-link-pengaturan.png) | 21:56:55 | UserA, dialog Share → Public Link | Privacy *can edit*, password, kedaluwarsa 23/10/2026 |
| EV-11 | [EV-11_public-link-tampilan-preview-download.png](EV-11_public-link-tampilan-preview-download.png) | 21:59:39 | Pengunjung publik (tanpa login) | Tombol *Preview* dan *Download* |
| EV-12 | [EV-12_public-link-tampilan-preview-saja.png](EV-12_public-link-tampilan-preview-saja.png) | 22:00:29 | Pengunjung publik (tanpa login) | Hanya tombol *Preview* |

## Evidence yang belum ada (mohon dilengkapi)

| Kebutuhan | Untuk test case |
|---|---|
| *Shared with me* milik UserA (berbagi UserB → UserA) | TC-05 |
| Pengunjung publik pada **folder**: tidak dapat rename/buat folder | TC-08 |
| Dialog Public Link untuk mode **preview saja** | TC-07 |
| Layar password yang dilihat pengunjung publik | TC-06/TC-07 |
| Screenshot Team Folder (setelah diaktifkan) | TC-09 |
