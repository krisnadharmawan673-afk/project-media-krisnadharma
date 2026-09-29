# Panduan Peningkatan Proyek: Fitur Versus, Desain SVG Interaktif, & Menu Pengembang

Dokumen ini berisi spesifikasi perbaikan dan peningkatan (**improvement**) untuk diterapkan pada proyek **Petualangan Pecahan**. Tujuan utama dari peningkatan ini adalah mengubah mekanisme permainan tunggal menjadi **permainan duel 2-pemain (Versus Mode)** berdampingan pada satu layar, berbasis input nomor absen siswa, menggunakan **SVG Dinamis** untuk pecahan, serta menambahkan informasi identitas pengembang pada bagian menu atas.

Media ini dirancang agar interaktif, di mana **guru bertindak sebagai fasilitator** yang memandu siswa, sementara dua orang siswa maju bersama untuk berkompetisi.

---

## 1. Peningkatan Menu Atas: Menu "Pengembang" (User-Friendly)

Untuk menghargai kontributor akademis dan membuat aplikasi lebih profesional, tambahkan tombol menu baru di bilah navigasi atas (utility-bar) bersanding dengan Musik, Suara, Atur, dan Keluar.

*   **Elemen HTML Baru (di dalam `.utility-bar` pada `index.html` dan halaman lainnya):**
    ```html
    <button class="utility-btn" type="button" data-open-modal="developerModal">
      <span class="utility-icon">👤</span>
      <span class="utility-label">Pengembang</span>
    </button>
    ```
*   **Struktur Modal Pengembang (`developerModal`):**
    *   Menggunakan backdrop gelap transparan (`modal-backdrop`).
    *   Kartu informasi bergaya papan kayu atau kertas kartun dengan bayangan tebal.
    *   **Isi Informasi:**
        *   **Judul:** 👤 Tentang Pengembang
        *   **Pengembang Utama:** `Krisna` (Krisna Media)
        *   **Dosen Pembimbing 1:** `Josep`
        *   **Dosen Pembimbing 2:** `Putri`
    *   Tombol "Tutup" dengan gaya warna merah kartun yang mencolok.

---

## 2. Alur Sistem Versus & Input Absensi

Sebelum memulai game apa pun, sistem harus menyajikan layar inisialisasi absensi siswa:
*   **Layar Input Absen:**
    *   Terdapat dua formulir input di sisi kiri dan kanan:
        *   **Sisi Kiri:** "Siswa 1 (Kiri) - Masukkan Nomor Absen"
        *   **Sisi Kanan:** "Siswa 2 (Kanan) - Masukkan Nomor Absen"
    *   Tombol "MULAI DUEL" hanya akan aktif setelah kedua siswa memasukkan nomor absen mereka (hanya menerima angka 1-50).
*   **Layout Tampilan Layar Utama (Split-Screen):**
    *   Layar terbagi menjadi 2 area utama secara horizontal (50% kiri untuk Siswa Kiri, 50% kanan untuk Siswa Kanan).
    *   Setiap sisi memiliki kartu identitas kecil di bagian atas yang menampilkan: `Absen [No]`.
    *   Skor masing-masing siswa ditampilkan secara real-time di atas areanya masing-masing.

---

## 3. Desain Pecahan Berbasis SVG Dinamis (Pizza / Lingkaran)

Untuk membuat visualisasi pecahan yang realistis, responsif, dan interaktif, pengembang **dilarang menggunakan aset gambar statis (PNG/JPG) untuk potongan pecahan**. Gunakan **inline SVG** yang digenerate dengan JavaScript.

### Rumus Matematika SVG untuk Menggambar Slice (Potongan Pizza):
Untuk membagi lingkaran menjadi $N$ bagian sama besar, kita menggunakan rumus koordinat busur SVG (`d="M x y A r r ..."`):
```javascript
function getSlicePath(cx, cy, r, startAngleDegree, endAngleDegree) {
  const startRad = (startAngleDegree - 90) * Math.PI / 180;
  const endRad = (endAngleDegree - 90) * Math.PI / 180;
  
  const x1 = cx + r * Math.cos(startRad);
  const y1 = cy + r * Math.sin(startRad);
  const x2 = cx + r * Math.cos(endRad);
  const y2 = cy + r * Math.sin(endRad);
  
  const largeArcFlag = (endAngleDegree - startAngleDegree) <= 180 ? 0 : 1;
  
  return `M ${cx} ${cy} L ${x1} ${y1} A ${r} ${r} 0 ${largeArcFlag} 1 ${x2} ${y2} Z`;
}
```

### Keunggulan SVG Interaktif:
1.  **Dapat Diklik (Interactive Toggling):** Setiap elemen `<path>` (potongan) dapat diberi event listener klik untuk mengubah status warnanya (misal: abu-abu menjadi merah pizza).
2.  **Responsif:** Menggunakan atribut `viewBox="0 0 200 200"` agar pas di semua ukuran layar.
3.  **Realistis:** Dapat diberi ornamen pizza (keju kuning, pepperoni merah, bintik oregano) di dalam `<path>` menggunakan tag `<pattern>` atau SVG Grouping (`<g>`).

---

## 4. Spesifikasi 3 Game Versus Interaktif

Kedua siswa akan berhadapan langsung pada layar yang sama (Siswa Kiri menggunakan keyboard sisi kiri / interaksi sentuh kiri, Siswa Kanan menggunakan keyboard sisi kanan / interaksi sentuh kanan).

### Game 1: Duel Memory Card Pecahan (`games/versus-memory.html`)
*   **Mekanisme:**
    *   Layar dibagi dua (Kiri dan Kanan). Masing-masing siswa memiliki **Grid Kartu 4x4 (16 Kartu)** yang identik namun diacak secara terpisah.
    *   Isi kartu adalah pasangan antara:
        *   **Kartu Angka:** Nilai pecahan tertulis (contoh: `1/4`, `2/3`, `3/8`).
        *   **Kartu SVG:** Visualisasi lingkaran pecahan dengan bagian yang diarsir sesuai nilai pecahan tersebut.
    *   Setiap siswa berlomba membuka kartu di areanya masing-masing.
    *   Jika kartu cocok (match), kartu akan tetap terbuka dan siswa mendapat skor +10. Jika salah, kartu tertutup kembali setelah 0.8 detik.
    *   Siswa yang menyelesaikan pencocokan semua kartu di areanya paling cepat adalah pemenangnya.

### Game 2: Duel Balap Kecepatan Pecahan (`games/versus-speed.html`)
*   **Mekanisme:**
    *   Layar tengah menampilkan satu pertanyaan pecahan acak (contoh: sebuah SVG lingkaran diarsir 3/5 bagian).
    *   Di bagian bawah masing-masing sisi siswa (Kiri dan Kanan), disediakan 4 pilihan jawaban yang sama dalam bentuk tombol kartu kayu.
    *   Siswa harus menekan tombol jawaban yang benar di areanya secepat mungkin.
    *   **Sistem Poin:**
        *   Siswa pertama yang menekan jawaban benar mendapat +20 poin.
        *   Siswa kedua yang menekan setelahnya (meski benar) hanya mendapat +5 poin.
        *   Jawaban salah akan mengurangi poin sebanyak -10 poin.
    *   Game terdiri atas 10 ronde soal. Siswa dengan skor tertinggi di akhir ronde memenangkan pertandingan.

### Game 3: Duel Pembuat Pizza (Fraction Assembly) (`games/versus-pizza.html`)
*   **Mekanisme:**
    *   Sistem memunculkan perintah di tengah layar, contoh: **"Buat Pizza bernilai 5/8!"**.
    *   Siswa Kiri dan Siswa Kanan masing-masing memiliki satu SVG Lingkaran Pizza utuh yang terbagi menjadi 8 slice kosong (berwarna putih/abu-abu).
    *   Siswa harus mengetuk slice pizza pada SVG masing-masing untuk mewarnai/mengisi slice tersebut hingga jumlahnya tepat 5 bagian.
    *   Setelah jumlah slice yang dipilih dirasa benar, siswa harus menekan tombol **"SUBMIT"** di areanya.
    *   Siswa pertama yang menekan "SUBMIT" dengan konfigurasi slice yang benar mendapatkan +30 poin dan ronde berakhir.
    *   Jika salah menekan "SUBMIT", area permainan siswa tersebut akan terkunci selama 3 detik sebagai penalti.
    *   Game dimainkan dalam 5 ronde dengan pembagian penyebut pecahan yang berbeda setiap rondenya (per 2, per 3, per 4, per 6, per 8).

---

## 5. Peran Guru sebagai Fasilitator (Teacher-Led Dynamic)

*   **Papan Kontrol Guru:**
    *   Di bagian atas layar game terdapat panel kecil tersembunyi yang hanya bisa diakses guru (dapat dibuka dengan tombol "GURU").
    *   Dari panel ini, guru dapat:
        *   Menjedakan permainan (Pause) untuk menjelaskan materi di tengah jalan.
        *   Mereset skor atau mengulangi ronde jika ada siswa yang salah paham.
        *   Memilih tingkat kesulitan soal pecahan (Pecahan Sederhana vs. Pecahan Campuran).
*   **Pemberitahuan Interaktif:**
    *   Setiap kali game selesai, layar menampilkan modal pemenang yang ramah anak, menampilkan nomor absen pemenang:
        *   *"Selamat Absen 12 Menang! Guru dapat memberikan apresiasi!"*
        *   *"Wah luar biasa! Absen 5 dan Absen 14 bermain dengan sangat adil!"*

---

## 6. Panduan Prompt Pembuatan Kode & Aset SVG bagi Agen Eksekutor

Agen pengembang berikutnya yang mengeksekusi dapat langsung menyalin prompt berikut untuk generate kode halaman game:

### Prompt Eksekusi Game Versus Pizza:
```text
Buat berkas HTML mandiri bernama 'games/versus-pizza.html' menggunakan Tailwind CSS.
Halaman ini harus membagi layar menjadi 2 sisi (Kiri dan Kanan).
1. Tampilkan modal pop-up sebelum game mulai untuk meminta input nomor absen Siswa Kiri dan Siswa Kanan.
2. Gambar Pizza menggunakan rumus kalkulasi Path SVG secara dinamis di dalam tag <svg> (bukan gambar statis).
3. Setiap potongan SVG path pizza dapat diklik untuk toggle warna keju pepperoni (kuning-merah) dan warna abu-abu kosong.
4. Tampilkan instruksi pecahan acak di bagian atas tengah layar, misal 'Buat Pecahan 3/4'.
5. Sediakan tombol 'Kirim Pizza' untuk masing-masing siswa. Periksa apakah jumlah potongan yang dipilih sesuai dengan pembilang dari soal pecahan yang diberikan.
6. Berikan efek suara ceria saat menang ronde dan suara penalti jika salah pilih. Urus progresi skor masing-masing siswa.
```
