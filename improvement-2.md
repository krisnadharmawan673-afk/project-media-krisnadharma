# Panduan Peningkatan Proyek Tahap 2: Interaktivitas Laboratorium, Sistem Absensi Dinamis, & Perbaikan UI Versus

Dokumen ini berisi spesifikasi perbaikan lanjutan (**improvement-2**) untuk meningkatkan aspek keramahan pengguna (user-friendly), metode interaktif di laboratorium materi, sistem absensi dinamis untuk kelas besar (32 siswa), serta standarisasi visual matematika (pecahan vertikal atas-bawah).

---

## 1. Interaktivitas Laboratorium Materi (Pengenalan Pecahan)

Halaman materi (`materi.html`) yang sebelumnya terlalu sederhana harus dirombak menjadi **"Laboratorium Eksperimen Pecahan"** yang komprehensif untuk menjelaskan konsep dasar pecahan secara konkret:

*   **Penjelasan Konsep Utama (Visual & Terstruktur):**
    *   Mengajarkan definisi pecahan secara gamblang sebagai "Bagian dari Keseluruhan".
    *   Menampilkan struktur pecahan secara vertikal dengan label yang sangat jelas:
        *   **Angka Atas (Pembilang):** Menunjukkan berapa banyak bagian yang kita miliki/pilih.
        *   **Garis Tengah:** Garis bagi (per).
        *   **Angka Bawah (Penyebut):** Menunjukkan total seluruh bagian yang sama besar.
    *   Terdapat label interaktif yang jika didekati/diklik akan memunculkan penjelasan balon teks (tooltip) tentang peran "Pembilang" dan "Penyebut".
*   **Laboratorium Pizza Interaktif (SVG):**
    *   Menyediakan tombol interaktif untuk menambah/mengurangi jumlah potongan pizza (penyebut: dari 2 hingga 10).
    *   Setiap kali jumlah potongan berubah, visual pizza SVG di layar terpotong secara otomatis secara real-time.
    *   Siswa atau guru dapat mengetuk potongan pizza tersebut untuk memakannya (mengarsirnya).
    *   Di samping pizza, sistem secara otomatis merender teks pecahan vertikal yang dinamis berdasarkan jumlah potongan yang dimakan vs total potongan (misal: jika 3 dari 8 potongan dipilih, render $\frac{3}{8}$ secara vertikal).

---

## 2. Sistem Absensi Dinamis per Pertanyaan (Versus Mode untuk 32 Siswa)

Saat ini, input absensi hanya dilakukan satu kali di awal game dan berlaku global. Mengingat dalam satu kelas terdapat sekitar 32 siswa, sistem harus diubah agar dapat digunakan secara bergantian (turn-based challenger) per pertanyaan/ronde:

*   **Alur Input Absen Setiap Ronde:**
    *   Di awal **setiap ronde baru**, permainan akan memunculkan layar overlay pop-up: *"Siapakah Penantang Berikutnya?"*.
    *   Siswa Kiri memasukkan nomor absennya (1-32) dan Siswa Kanan memasukkan nomor absennya (1-32).
    *   Setelah dikonfirmasi, barulah soal/tantangan ronde tersebut ditampilkan.
    *   Siswa berduel menyelesaikan soal tersebut.
    *   Jika salah satu siswa menjawab salah atau kehabisan waktu (gagal), maka siswa dengan nomor absen tersebut mendapatkan skor 0 pada ronde itu, dan pemenang mendapatkan poin penuh.
*   **Penyimpanan Data ke JSON (Lokal Tracker):**
    *   Untuk memudahkan guru melacak performa ke-32 siswa tanpa excel yang rumit di awal, semua data hasil duel harus disimpan ke dalam struktur data JSON di `LocalStorage`.
    *   Guru dapat membuka menu "Laporan Guru" di bagian atas untuk mengunduh berkas `.json` tersebut atau melihat tabel skor sementara.

---

## 3. Penulisan Pecahan Vertikal (Atas - Bawah)

Format pecahan menyamping seperti `1/2`, `3/4`, atau `5/8` tidak standar untuk media pembelajaran sekolah dasar dan membingungkan siswa. 

*   **Ketentuan Desain Pecahan Baru:**
    *   Di semua halaman (Materi, Game Versus 1, 2, 3, dan Soal), penulisan pecahan wajib diubah menjadi format vertikal (stacked fraction).
    *   Gunakan struktur HTML + Tailwind untuk menampilkan pecahan bertumpuk:
        ```html
        <div class="inline-flex flex-col items-center align-middle font-bold text-2xl mx-1">
          <span class="border-b-2 border-slate-700 pb-0.5 px-1">Pembilang</span>
          <span class="pt-0.5 px-1">Penyebut</span>
        </div>
        ```
    *   Ini memastikan pembilang berada tepat di atas penyebut dengan garis pemisah horizontal yang jelas di tengahnya.

---

## 4. Perbaikan Tata Letak UI Game Versus 3 (Pembuat Pizza)

*   **Pemisahan Soal dan Ronde:**
    *   **Area Ronde (Round Info):** Letakkan di pojok kiri atas atau kanan atas dengan desain lencana (badge) kayu kecil yang manis, contoh: `Ronde: 3/5`.
    *   **Area Soal (Target Pecahan):** Tempatkan tepat di tengah-tengah atas dengan ukuran besar dan mencolok menggunakan format pecahan vertikal, contoh: *"Buatlah Pecahan: $\frac{5}{8}$"*. Ini meminimalisir kebingungan siswa dalam membedakan angka ronde dengan angka pecahan soal.
*   **Split-Screen yang Lebih Rapi:**
    *   Beri garis pemisah vertikal bermotif batang tanaman/kayu di tengah layar untuk mempertegas batas area pengerjaan Siswa Kiri dan Siswa Kanan.

---

## 5. Skema JSON Tracker (Data Hasil Uji Coba Siswa)

Struktur data JSON yang disimpan di dalam `LocalStorage` (dengan key `krisna_media_tracker`) untuk merekam aktivitas duel siswa dirancang sebagai berikut:

```json
{
  "tanggal_sesi": "2026-07-19T19:43:00Z",
  "data_absen": {
    "1": { "nama": "Siswa 1", "menang": 3, "kalah": 2, "total_skor": 75 },
    "2": { "nama": "Siswa 2", "menang": 1, "kalah": 4, "total_skor": 15 },
    "12": { "nama": "Siswa 12", "menang": 5, "kalah": 0, "total_skor": 150 }
  },
  "riwayat_ronde": [
    {
      "ronde": 1,
      "game": "versus-pizza",
      "absen_kiri": 12,
      "absen_kanan": 5,
      "pemenang": 12,
      "skor_kiri": 30,
      "skor_kanan": 0
    }
  ]
}
```

---

## 6. Panduan Prompt Eksekusi untuk Agen Selanjutnya

### Prompt Modifikasi Absensi Dinamis & Tracker JSON:
```text
Modifikasi sistem absensi pada semua game versus di folder 'games/'.
1. Di setiap awal ronde baru, tampilkan modal pop-up 'Input Absen Ronde X' untuk meminta input absen Siswa Kiri dan Siswa Kanan.
2. Setiap kali ronde berakhir, simpan data pertandingan (nomor absen, pemenang, skor) ke LocalStorage dengan format JSON terstruktur.
3. Buat menu tersembunyi 'Laporan Guru' di header halaman utama yang dapat menampilkan tabel skor ke-32 siswa berdasarkan data JSON tersebut, lengkap dengan tombol untuk mengekspor data ke file .json.
```

### Prompt Perbaikan UI Pecahan Vertikal:
```text
Perbaiki komponen teks pecahan di seluruh berkas HTML dan JS. 
Ubah semua format teks bertipe string 'A/B' (seperti 1/2) menjadi elemen HTML bertumpuk vertikal dengan pembilang di atas, garis pembagi di tengah, dan penyebut di bawah menggunakan Tailwind CSS flex-col. Pastikan penataan letak teks tetap sejajar dan rapi di dalam kalimat soal.
```
