# Atomic Commits

Selesaikan pekerjaan yang diminta dengan satu tujuan logis per commit. Saat skill ini diminta untuk implementasi, buat commit lokal selama pengerjaan, kecuali pengguna meminta rencana saja atau melarang commit. Pemanggilan otomatis tidak memperluas izin tugas. Ikuti instruksi pengguna dan aturan repositori.

## Periksa kondisi awal

- Baca instruksi repositori, status Git, diff staged dan unstaged, serta beberapa pesan commit terbaru. Catat branch, HEAD awal jika ada, dan perubahan yang sudah ada sebelum mulai.
- Bedakan perubahan tugas ini dengan pekerjaan pengguna yang sudah ada. Sertakan perubahan lama hanya jika pengguna meminta perubahan tersebut ikut dikomit.
- Jika direktori belum menjadi repositori Git, lanjutkan pekerjaan yang aman dan jelaskan bahwa commit belum dapat dibuat. Jangan menginisialisasi Git atau mengubah konfigurasi identitas tanpa otorisasi.
- Jika ada konflik merge atau operasi Git yang belum selesai, jangan menyelesaikan atau membatalkannya tanpa kaitan dan otorisasi yang jelas.

## Tentukan batas commit

Sampaikan pembagian singkat: tujuan setiap commit dan urutan dependensinya. Untuk satu perubahan sederhana, cukup satu commit. Jangan meminta persetujuan atas pembagian rutin yang sudah termasuk lingkup tugas.

- Pisahkan tujuan yang bisa direview sendiri, misalnya perbaikan validasi, penambahan fitur, dan refaktor independen.
- Gabungkan implementasi dengan tes, konfigurasi, migrasi, dokumentasi, atau lockfile yang diperlukan untuk perubahan itu. Jangan membuat commit antara yang sengaja merusak build atau kontrak.
- Jangan membagi commit hanya berdasarkan file, direktori, lapisan arsitektur, jumlah baris, atau kuota commit. Satu fitur dapat memerlukan beberapa file dalam satu commit.
- Pisahkan refaktor dari perubahan perilaku jika keduanya tetap menghasilkan keadaan yang valid. Gabungkan jika pemisahan menghasilkan langkah yang rusak.
- Untuk perubahan lintas repositori, buat commit di masing-masing repositori dan jelaskan dependensinya.

Contoh: perubahan penyimpanan pengaturan, penambahan pemetaan gesture, dan perbaikan bug navigasi yang independen dapat menjadi tiga commit. Bila layar pengaturan tidak bisa dibangun tanpa model penyimpanannya, sertakan keduanya dalam satu commit atau buat model yang kompatibel sebagai langkah pertama.

## Kerjakan dan commit satu tujuan sampai selesai

1. Implementasikan satu kelompok perubahan, termasuk penyesuaian yang diperlukan agar tahap tersebut berfungsi.
2. Jalankan pemeriksaan yang relevan dengan kelompok itu, mengikuti perintah dan kebiasaan proyek. Untuk perubahan perilaku, sertakan tes yang bermakna bila diperlukan. Jangan menambah tes yang hanya menyalin implementasi atau memaksakan tes untuk perubahan sepele.
3. Periksa diff, lalu stage hanya path atau hunk yang termasuk tujuan tersebut. Gunakan path eksplisit. Hindari staging menyeluruh yang dapat menyerap pekerjaan lain.
4. Periksa seluruh index dengan `git diff --cached`, ringkasannya, dan `git diff --cached --check`. Pastikan tidak ada perubahan pengguna, rahasia, atau file hasil proses yang tidak relevan.
5. Buat commit lokal setelah pemeriksaan yang diwajibkan lulus. Gunakan gaya pesan repositori; bila belum ada konvensi, gunakan `type(scope): tujuan konkret` seperti `feat(settings): add gesture action mapping` atau `fix(auth): reject inactive accounts`. Tambahkan alasan atau batasan dalam body jika berguna. Jangan mengarang nomor issue atau hasil tes.
6. Verifikasi commit benar-benar berhasil, catat hash dan isinya, lalu periksa status sebelum melanjutkan ke tujuan berikutnya.

Jika perubahan sudah terlanjur tercampur, gunakan staging per hunk atau patch index yang telah ditinjau. Jangan membuang atau menulis ulang working tree untuk memisahkannya.

## Jaga index dan kejujuran verifikasi

- Pertahankan perubahan dan status staging awal pengguna. Jangan memasukkannya lewat `git commit` biasa, men-unstage semuanya, atau memakai stash sebagai langkah otomatis.
- Jika index awal berisi pekerjaan di luar lingkup, gunakan index sementara terisolasi atau worktree yang diizinkan hanya bila perubahan dan staging asli dapat dipertahankan dengan benar setelah commit. Bila tidak dapat menjaminnya, lanjutkan pekerjaan yang aman dan laporkan hambatan commit.
- Untuk commit yang disusun melalui staging sebagian, tes pada working tree dapat mencakup kode yang belum masuk commit. Verifikasi snapshot commit secara terisolasi bila dibutuhkan agar hasil tes benar-benar berlaku untuk commit tersebut. Jelaskan bila snapshot belum diuji.
- Perbaiki kegagalan yang disebabkan tugas sebelum commit. Jika pemeriksaan wajib terhalang lingkungan atau kegagalan yang sudah ada, laporkan penyebabnya dan lanjutkan pekerjaan independen; jangan melewati pemeriksaan wajib atau mengklaim lulus.
- Jangan menjalankan reset destruktif, membuang perubahan, amend, rebase, squash, push, atau mengubah hook dan konfigurasi Git kecuali diminta atau sudah diotorisasi. Bila commit keliru, utamakan commit koreksi yang fokus.
- Jika hook mengubah file, tinjau perubahan dan jalankan kembali pemeriksaan yang terdampak. Jika hook menolak commit, perbaiki penyebabnya tanpa menonaktifkan hook.

## Tutup dengan hasil yang bisa ditelusuri

Tuntaskan semua tujuan yang diotorisasi. Laporkan setiap hash commit beserta tujuan singkatnya, hasil pemeriksaan, dan perubahan yang masih tersisa. Nyatakan secara jelas jika commit belum berhasil atau pengujian hanya mencakup working tree. Jangan mengklaim working tree bersih bila masih ada pekerjaan pengguna.
