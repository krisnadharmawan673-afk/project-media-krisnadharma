# Panduan Pengembangan Proyek: Petualangan Pecahan (Fraction Adventure)

Dokumen ini adalah spesifikasi lengkap dan terstruktur untuk pembuatan media pembelajaran interaktif bertema **"Petualangan Pecahan"**. Panduan ini ditujukan bagi agen AI pengembang untuk dieksekusi menggunakan teknologi **Pure HTML, Tailwind CSS, Vanilla JavaScript, dan Custom CSS**.

---

## 1. Konsep Utama & Tema Visual

*   **Nama Proyek:** Petualangan Pecahan (Fraction Adventure)
*   **Tema Desain:** Taman Fantasi & Alam Terbuka (Lush Garden & Fantasy Landscape).
*   **Estetika:** Ceria, ramah anak, penuh warna, menggunakan elemen kayu kartun (wooden board) sebagai papan judul dan tombol, dikelilingi balon udara, kastil, pelangi, rumput hijau, bunga-bunga, dan karakter anak sekolah yang interaktif.
*   **Representasi Pecahan:** Menggunakan visualisasi makanan konkret seperti pizza, semangka, kue pai, donat, apel, dan cairan lab berwarna-warni yang dibagi menjadi beberapa bagian.

---

## 2. Arsitektur & Teknologi Stack

Untuk memastikan performa yang cepat, kemudahan pemeliharaan, dan portabilitas tinggi, proyek ini dikembangkan dengan ketentuan:
1.  **Pure HTML5:** Setiap modul halaman dipisah ke dalam file HTML tersendiri agar kode tidak menumpuk.
2.  **Tailwind CSS:** Digunakan untuk mempercepat pembuatan tata letak (layout) dan desain responsif (melalui CDN atau file lokal).
3.  **Vanilla JavaScript:** Digunakan untuk semua logika game, animasi interaktif, manajemen audio, dan penyimpanan status level.
4.  **LocalStorage:** Untuk melacak level mana saja yang sudah diselesaikan (Unlocked/Locked levels) agar ada progresi permainan.
5.  **Audio System:** Background music (BGM) bernuansa ceria yang bisa di-mute, serta Sound Effects (SFX) untuk tombol klik, jawaban benar, jawaban salah, dan kemenangan.

---

## 3. Struktur Direktori Proyek

Agen pengeksekusi wajib menyusun file dengan struktur yang teratur seperti berikut:

```text
KRISNA MEDIA/
├── index.html                  # Halaman Utama (Beranda)
├── game-menu.html              # Halaman Peta/Menu Level Game
├── petunjuk.html               # Halaman Panduan Bermain
├── materi.html                 # Halaman Belajar Materi Pecahan
├── soal.html                   # Halaman Quiz / Evaluasi Mandiri
├── games/
│   ├── dasar-pecahan.html      # Level 1: Dasar Pecahan
│   ├── membandingkan.html      # Level 2: Membandingkan & Mengurutkan
│   ├── penjumlahan.html        # Level 3: Penjumlahan Pecahan
│   └── pengurangan.html        # Level 4: Pengurangan Pecahan
├── assets/
│   ├── css/
│   │   └── custom.css          # Gaya khusus (animasi goyang, font, dll.)
│   ├── js/
│   │   ├── main.js             # Logika global & manajemen level
│   │   └── audio.js            # Sistem musik dan efek suara
│   ├── audio/                  # File BGM dan SFX (click, correct, wrong, win)
│   └── images/                 # Aset gambar hasil generate
│       ├── backgrounds/        # Latar belakang taman, laboratorium, hutan
│       ├── characters/         # Ilustrasi karakter anak sekolah & guru
│       └── ui/                 # Tombol kayu, papan pengumuman, ikon-ikon
└── project.md                  # File spesifikasi ini
```

---

## 4. Spesifikasi Halaman & UI

### 4.1. Halaman Utama (`index.html`)
*   **Latar Belakang:** Pemandangan taman fantasi dengan bukit hijau, kastil di kejauhan, pelangi, awan bergerak lambat, dan balon udara.
*   **Header:** Papan kayu bertuliskan **"PETUALANGAN PECAHAN"** dengan sub-header **"Belajar Sambil Bermain, Pecahan Jadi Mudah!"** menggunakan font anak-anak yang tebal (seperti *Fredoka One* atau *Lilita One*).
*   **Utility Bar (Kanan Atas):** Tombol bulat untuk Musik (On/Off), Suara SFX (On/Off), Pengaturan, dan Keluar.
*   **Menu Cards (4 Panel Utama):**
    1.  **Card Petunjuk (Hijau):** Ilustrasi arah jalan/kompas + tombol "MULAI".
    2.  **Card Materi (Biru):** Ilustrasi buku pecahan & guru wanita + tombol "MULAI".
    3.  **Card Game (Ungu):** Ilustrasi piala, peti harta karun, gamepad + tombol "MULAI".
    4.  **Card Soal (Jingga):** Ilustrasi papan ujian & anak perempuan belajar + tombol "MULAI".
*   **Dekorasi Bawah:** Karakter anak laki-laki dan perempuan berseragam sekolah SD di sisi kiri dan kanan, serta potongan buah semangka/donat pecahan di tanah sebagai hiasan.

### 4.2. Halaman Menu Game (`game-menu.html`)
*   **Visual Utama:** Jalur setapak taman yang meliuk-liuk (winding road) yang menghubungkan titik level 1, 2, 3, dan 4.
*   **Level Cards (4 Level Permainan):**
    1.  **Level 1: Dasar Pecahan (Biru):** Ilustrasi anak-anak membagi pizza.
    2.  **Level 2: Membandingkan & Mengurutkan (Hijau):** Trek balapan kelinci & rubah dengan tanda `>`, `<`, `=`.
    3.  **Level 3: Penjumlahan Pecahan (Ungu):** Anak-anak memakai jas lab mencampurkan cairan pecahan kimia.
    4.  **Level 4: Pengurangan Pecahan (Oranye):** Anak petualang membuka peti harta karun dengan pecahan kue.
*   **Sistem Progresi:** Level 2, 3, dan 4 awalnya dikunci (locked dengan ikon gembok) dan hanya terbuka jika pemain menyelesaikan level sebelumnya.
*   **Dekorasi:** Buku terbuka, tas sekolah, simbol matematika (`+`, `-`, `×`, `÷`), dan papan tanda kayu bertuliskan *"Ayo Jadi Juara Matematika!"*.

### 4.3. Halaman Petunjuk (`petunjuk.html`)
*   Papan kayu besar di tengah layar yang menampilkan cara bermain menggunakan ikon visual dan teks langkah-langkah yang mudah dipahami anak-anak.
*   Tombol kembali berbentuk tanda panah kayu (Back button) ke `index.html`.

### 4.4. Halaman Materi (`materi.html`)
*   **Slider Pecahan Interaktif:** Area di mana anak bisa menggeser slider pembilang (numerator) dan penyebut (denominator) lalu melihat perubahan visual lingkaran pizza atau kue secara dinamis dan real-time.
*   **Kartu Penjelasan:** Penjelasan sederhana tentang arti pecahan (misal: "1 dari 4 bagian disebut 1/4").

---

## 5. Detail Modul Game (Setiap Game Beda HTML)

Setiap game memiliki berkas HTML terpisah di dalam folder `/games/` dengan logika permainan mandiri:

### 5.1. Level 1: Dasar Pecahan (`games/dasar-pecahan.html`)
*   **Gameplay:** Pemain diberikan tantangan untuk mencocokkan nilai pecahan (contoh: "Tunjukkan pecahan 2/4!"). Pemain harus mengetuk 2 dari 4 bagian pizza yang disediakan di layar.
*   **Interaktivitas:** Bagian lingkaran pizza yang diklik akan berubah warna (menjadi terang/dipilih). Jika jumlah bagian terpilih sesuai pembilang, klik tombol "Periksa".
*   **Reward:** Suara sorakan gembira dan animasi bintang terbang jika benar.

### 5.2. Level 2: Membandingkan & Mengurutkan (`games/membandingkan.html`)
*   **Gameplay:** Dua pecahan ditampilkan di layar (misal: `1/2` dan `1/3`). Pemain harus memilih tanda pembanding yang benar (`>`, `<`, atau `=`).
*   **Visual Balapan:** Jawaban benar akan membuat mobil balap karakter kelinci melaju mendekati garis finish. Jawaban salah membuat mobil mengeluarkan asap kecil dan tertahan.
*   **Pengurutan:** Game bagian kedua meminta anak menyeret (drag-and-drop) 3 kartu pecahan ke garis bilangan dari yang terkecil hingga terbesar.

### 5.3. Level 3: Penjumlahan Pecahan (`games/penjumlahan.html`)
*   **Gameplay:** Bertema laboratorium kimia. Pemain menuangkan cairan dari gelas ukur A (misal: `1/4` cairan biru) dan gelas ukur B (misal: `2/4` cairan merah) ke dalam tabung reaksi besar.
*   **Visualisasi:** Tabung reaksi besar akan menunjukkan kenaikan tingkat volume cairan menjadi gabungan (`3/4` cairan ungu). Pemain harus mengetikkan atau memilih jawaban pecahan hasil penjumlahannya.

### 5.4. Level 4: Pengurangan Pecahan (`games/pengurangan.html`)
*   **Gameplay:** Petualangan hutan mencari harta karun. Pintu peti harta karun dikunci dengan rantai berangka pecahan. Pemain harus memotong tali/kue pai (mengurangi pecahan) sesuai instruksi petunjuk kunci untuk membuka gembok.
*   **Visual:** Peti terbuka mengeluarkan koin emas berkilauan ketika tantangan pengurangan dijawab dengan tepat.

---

## 6. Halaman Quiz / Evaluasi (`soal.html`)

*   **Tampilan:** Papan tulis putih (whiteboard) berbingkai kayu.
*   **Soal Acak:** Menyajikan 10 pertanyaan pilihan ganda atau isian singkat secara acak yang mencakup semua materi level 1 hingga level 4.
*   **Hasil Akhir (Scoreboard):** Menampilkan papan nilai dengan bintang (1-3 bintang), animasi confetti, serta pesan penyemangat berdasarkan skor yang diperoleh.

---

## 7. Panduan Pembuatan Aset Gambar (PENTING untuk Agen Selanjutnya)

Agen pengeksekusi **WAJIB** menggunakan tool `generate_image` miliknya untuk memproduksi aset gambar berkualitas tinggi dengan gaya yang konsisten. Jangan menggunakan gambar placeholder kosong.

### Panduan Prompt Gambar (Gaya Konsisten):
*   **Gaya Desain Umum:** `"Cartoon vector style, vibrant colors, child-friendly, colorful 2D game asset, game UI, high quality"`
*   **Background Utama (`assets/images/backgrounds/garden_bg.png`):**
    *   *Prompt:* `"Charming fantasy cartoon garden background, lush green hills, clear blue sky with fluffy white clouds, colorful rainbow, whimsical castles in the distance, hot air balloons floating, flowers on the grass, 2D game background, bright colors"`
*   **Papan Papan Kayu (`assets/images/ui/wooden_board.png`):**
    *   *Prompt:* `"Fantasy cartoon style wooden sign board, rustic brown wood texture, hanging ropes, clean edges, game UI asset, transparent background"`
*   **Karakter Anak Laki-laki (`assets/images/characters/boy_student.png`):**
    *   *Prompt:* `"Cute schoolboy cartoon character, red and white Indonesian school uniform, wearing backpack, pointing up, smiling happily, 2D vector game asset, isolated transparent background"`
*   **Karakter Anak Perempuan (`assets/images/characters/girl_student.png`):**
    *   *Prompt:* `"Cute schoolgirl cartoon character, red and white school uniform, holding a math book, smiling, friendly expression, 2D vector game asset, isolated transparent background"`
*   **Aset Makanan Pecahan (`assets/images/ui/pizza_fraction.png`):**
    *   *Prompt:* `"Delicious cartoon pizza, sliced clearly into equal pieces, some slices slightly separated to show fractions, 2D game icon, transparent background"`

---

## 8. Panduan Eksekusi (Langkah-demi-Langkah untuk Agen Pengeksekusi)

1.  **Inisialisasi Folder:** Buat semua struktur direktori seperti pada poin #3.
2.  **Generate Aset Gambar:** Buat aset background, papan kayu, dan karakter terlebih dahulu menggunakan `generate_image`, simpan di `assets/images/`.
3.  **Buat Stylesheet Global (`assets/css/custom.css`):**
    *   Impor Google Fonts (*Fredoka* dan *Quicksand*).
    *   Tulis kelas animasi khusus untuk efek hover memantul (bounce), awan bergerak lambat, dan efek kilau (glow) pada tombol aktif.
4.  **Tulis Logika Audio (`assets/js/audio.js`):**
    *   Buat objek Audio untuk backsound dan efek suara tombol/kebenaran.
    *   Implementasikan fungsi mute/unmute yang konsisten di semua halaman menggunakan LocalStorage.
5.  **Implementasikan Halaman Beranda (`index.html`) & Menu Game (`game-menu.html`):**
    *   Pastikan navigasi antarhalaman berjalan lancar dengan tautan `href` relatif.
6.  **Bangun Logika Game Individu:**
    *   Pastikan logika perhitungan matematika menggunakan JavaScript valid.
    *   Tambahkan tombol "Periksa Jawaban" dan "Lanjut ke Level Berikutnya" di setiap game.
    *   Ketika level berhasil diselesaikan, ubah status level tersebut di LocalStorage menjadi `unlocked: true` dan arahkan pemain kembali ke `game-menu.html`.
7.  **Verifikasi & Uji Coba:** Pastikan tidak ada eror di konsol peramban (browser console) dan semua tombol berfungsi secara responsif di ukuran layar desktop maupun tablet.
