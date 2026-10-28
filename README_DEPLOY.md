# Rekap Perjalanan Dinas — GitHub Pages + Firebase

Situs berjalan di GitHub Pages. Firestore menjadi sumber data bersama. Pengunjung dapat membaca dan mengekspor data; hanya satu akun admin yang boleh mengubahnya.

## Persiapan Firebase

1. Buat proyek Firebase baru pada akun Anda dan gunakan paket Spark. Buat database Cloud Firestore pada mode production. Pilih lokasi Asia yang sesuai; lokasi database tidak dapat diubah setelah dibuat.
2. Di **Authentication → Sign-in method**, aktifkan **Email/Password**. Buat akun admin dari **Authentication → Users → Add user**. Kata sandi tetap dimasukkan langsung di Firebase Console.
3. Tambahkan aplikasi web Firebase, lalu salin konfigurasi web dari **Project settings → Your apps** ke `firebase-config.js`. Konfigurasi web bukan rahasia; aturan Firestore tetap menjadi pengaman akses.
4. UID admin proyek ini sudah dimasukkan ke `firebase-config.js` dan `firestore.rules`.
5. Tempelkan isi `firestore.rules` ke **Firestore Database → Rules**, lalu terbitkan. Aturan ini memberi siapa pun akses baca dan membatasi semua perubahan ke UID admin tersebut.
6. Di **Authentication → Settings → Authorized domains**, tambahkan `ybusax.github.io`.

Koleksi `trips` dan dokumen `app/settings` akan kosong ketika proyek baru. Data yang tersimpan di browser sebelumnya tidak disalin ke database.

## GitHub Pages

1. Buat repository **public** bernama `Rekap_Perjalanan_Dinas` di akun `ybusax`.
2. Unggah `index.html`, `firebase-config.js`, `firestore.rules`, dan `README_DEPLOY.md` ke root repository. Jangan unggah file salinan/backup aplikasi.
3. Buka **Settings → Pages**, pilih **Deploy from a branch**, branch `main`, folder `/ (root)`, lalu simpan.
4. Situs akan tersedia di `https://ybusax.github.io/Rekap_Perjalanan_Dinas/`.

## Akses dan batasan

- Aplikasi tidak menyediakan pendaftaran admin. Buat akun admin langsung melalui Firebase Console.
- Tombol yang mengubah data disembunyikan untuk publik. Pemeriksaan UID di Firestore Rules tetap menolak perubahan langsung dari luar aplikasi.
- Data perjalanan dan master pegawai dapat dibaca publik sesuai kebutuhan aplikasi. Jangan menambahkan data yang tidak boleh dipublikasikan.
- Firebase Spark menyediakan kuota tanpa biaya; jika batas layanan terlampaui, akses dapat tertahan sampai kuota pulih atau paket berubah. Periksa halaman penggunaan Firebase secara berkala.
