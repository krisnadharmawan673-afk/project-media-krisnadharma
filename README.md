# Petualangan Pecahan — Krisna Media

Media pembelajaran pecahan interaktif untuk siswa sekolah dasar. Proyek dibuat dengan HTML5, Tailwind CSS (CDN sebagai enhancement), custom CSS, dan Vanilla JavaScript tanpa framework atau build step.

## Cara menjalankan

1. Ekstrak ZIP.
2. Buka folder `KRISNA MEDIA`.
3. Klik dua kali `index.html` menggunakan Chrome, Edge, Firefox, atau Safari versi modern.
4. Klik salah satu tombol untuk mengaktifkan musik (browser biasanya memblokir audio sebelum interaksi pertama).

Semua fungsi inti, visual, game, dan audio lokal tetap dapat digunakan tanpa proses instalasi. Koneksi internet hanya digunakan bila browser ingin memuat font Fredoka/Quicksand dan Tailwind CDN; tampilan utama memiliki fallback lokal.

## Isi media

- Beranda dengan empat menu utama.
- Petunjuk visual cara bermain.
- Materi pecahan dengan slider pembilang dan penyebut real-time.
- Level 1: memilih bagian pizza.
- Level 2: membandingkan dan drag-and-drop urutan pecahan.
- Level 3: simulasi menjumlahkan cairan pecahan.
- Level 4: simulasi pengurangan untuk membuka peti harta karun.
- Arena Versus untuk dua siswa dalam satu layar:
  - Duel Memory 4×4: kartu angka melawan visual SVG.
  - Balap Kecepatan: 10 ronde, skor +20/+5/−10.
  - Pembuat Pizza: 5 ronde SVG, skor +30 dan penalti 3 detik.
- Input nomor absen 1–50, kartu identitas, dan skor real-time pada kedua sisi.
- Kontrol guru untuk jeda, reset skor, ulang ronde, dan tingkat kesulitan.
- Menu Pengembang berisi identitas Krisna, Josep, dan Putri.
- Evaluasi acak 10 soal dengan papan nilai dan 1–3 bintang.
- Musik, efek suara, mute/unmute, dan progres level melalui `localStorage`.

## Mengulang progres

Pada halaman utama atau peta level, tekan tombol **ATUR**, lalu pilih **Ulangi Progres**.

## Kontrol keyboard Mode Versus

- Memory: kiri memakai `W A S D` + `F`; kanan memakai tombol panah + `Enter`.
- Balap Kecepatan: kiri memakai `Q W E R`; kanan memakai `U I O P`.
- Pembuat Pizza: kiri memakai `A S D F G H J K` + `Spasi`; kanan memakai angka `1–8` + `Enter`.

Semua kontrol keyboard bersifat opsional. Pemain tetap dapat memakai sentuhan atau klik mouse pada area masing-masing.
