# Rencana Implementasi: Laporan Guru PDF (Game & Arena) & Absen 45 Siswa

Rencana ini merinci pembaruan fitur Laporan Guru agar mendukung ekspor format **.pdf** (menggantikan .json), memisahkan laporan antara **Nilai Game Operasi** dan **Rekap Arena Duel**, serta memperluas kapasitas nomor absen pada seluruh modul Arena Versus hingga **45 siswa**.

## User Review Required

> [!IMPORTANT]
> - Output unduhan data pada Laporan Guru kini menghasilkan dokumen **.pdf** resmi (bukan berkas `.json`).
> - Terdapat **dua jenis laporan terpisah**:
>   1. **Laporan Nilai Game Operasi Pecahan**: Berisi nilai Penjumlahan, Pengurangan, Perkalian, Pembagian, Rata-rata 4 materi, dan status ketuntasan KKM (70) untuk 45 siswa.
>   2. **Laporan Rekapitulasi Arena Duel**: Berisi statistik Menang, Kalah, Total Main, Win Rate, Total Skor Duel, serta Riwayat Ronde Pertandingan Duel untuk 45 siswa.
> - Menggunakan pustaka client-side `html2pdf.js` untuk unduhan langsung `.pdf` otomatis, dilengkapi **fallback cetak PDF offline** (`window.print()`) berformat Kop Resmi Sekolah jika perangkat guru sedang offline.

---

## Proposed Changes

### 1. Modul Arena Versus (Absen 1–45)

#### [MODIFY] [versus-pizza.html](file:///c:/Users/krisn/OneDrive/Dokumen/sd-belajar-pecahan-krisnadharma/games/versus-pizza.html)
- Perbarui deskripsi instruksi: `(1–32)` menjadi `(1–45)`.
- Perbarui input `leftAbsent` dan `rightAbsent`: `min="1" max="45" placeholder="1–45"`.

#### [MODIFY] [versus-memory.html](file:///c:/Users/krisn/OneDrive/Dokumen/sd-belajar-pecahan-krisnadharma/games/versus-memory.html)
- Perbarui deskripsi instruksi: `(1–32)` menjadi `(1–45)`.
- Perbarui input `leftAbsent` dan `rightAbsent`: `min="1" max="45" placeholder="1–45"`.

#### [MODIFY] [versus-menu.html](file:///c:/Users/krisn/OneDrive/Dokumen/sd-belajar-pecahan-krisnadharma/versus-menu.html), [game-menu.html](file:///c:/Users/krisn/OneDrive/Dokumen/sd-belajar-pecahan-krisnadharma/game-menu.html), [index.html](file:///c:/Users/krisn/OneDrive/Dokumen/sd-belajar-pecahan-krisnadharma/index.html)
- Perbarui atribut `title` pada tombol Laporan Guru menjadi `Laporan Guru (45 Siswa)`.

---

### 2. Sistem Tracker & Laporan Guru

#### [MODIFY] [tracker.js](file:///c:/Users/krisn/OneDrive/Dokumen/sd-belajar-pecahan-krisnadharma/assets/js/tracker.js)
- **Tab Navigasi pada Modal Laporan Guru:**
  - Tab 1: 🎮 **Nilai Game Operasi** (Penjumlahan, Pengurangan, Perkalian, Pembagian, Rata-rata 4 materi).
  - Tab 2: ⚔️ **Rekap Arena Duel** (Menang, Kalah, Total Main, Win Rate, Total Skor, Riwayat Ronde).
- **Generator Dokumen PDF Resmi:**
  - Fungsi `generateGameReportHtml(data)`: Membentuk dokumen cetak A4 landscape dengan Kop Resmi Krisna Media, identitas sekolah, statistik ringkas kelas (rata-rata kelas, nilai tertinggi, persentase tuntas), tabel 45 siswa terformat rapi, dan kolom tanda tangan guru.
  - Fungsi `generateArenaReportHtml(data)`: Membentuk dokumen cetak A4 landscape/portrait dengan Kop Resmi, statistik kompetisi (juara duel, total ronde), tabel statistik 45 siswa, serta tabel riwayat ronde duel.
  - Fungsi `exportPdf(type)`: Memuat `html2pdf.js` dinamis untuk langsung mengunduh berkas `.pdf` (`Laporan_Nilai_Game_SD_45Siswa.pdf` atau `Laporan_Arena_Duel_SD_45Siswa.pdf`). Jika offline/gagal, membuka dialog cetak PDF browser dengan layout cetak `@media print` resmi.
- **Tombol Unduh Terpisah:**
  - `[📄 Unduh PDF Game (.pdf)]` pada Tab Game Operasi.
  - `[📄 Unduh PDF Arena (.pdf)]` pada Tab Arena Duel.
- **Pembersihan Data:**
  - Tombol `[🗑️ Hapus Data]` tetap tersedia dengan konfirmasi dialog.

---

### 3. Tampilan & Desain Visual

#### [MODIFY] [custom.css](file:///c:/Users/krisn/OneDrive/Dokumen/sd-belajar-pecahan-krisnadharma/assets/css/custom.css)
- Styling tab switcher modal laporan (`.report-tab-bar`, `.report-tab-btn`, `.report-tab-btn.active`).
- Styling kartu ringkasan metrik statistik (`.report-stats-grid`, `.report-stat-card`).
- Styling tabel riwayat duel dan badge hasil pertandingan (`.badge-win`, `.badge-loss`).
- CSS cetak khusus (`@media print`) untuk memastikan dokumen PDF tampak rapi, tajam, dan tidak terpotong saat diekspor.

---

## Verification Plan

### Manual Verification
1. **Verifikasi Input Absen 45 Siswa:**
   - Buka `games/versus-pizza.html`, coba masukkan absen `45` pada kedua sisi -> Pastikan validasi lolos dan tombol "Mulai Duel" aktif.
   - Buka `games/versus-memory.html`, coba masukkan absen `45` pada kedua sisi -> Pastikan validasi lolos.
   - Coba masukkan absen `46` atau `0` -> Pastikan muncul pesan error validasi (harus 1–45).
2. **Verifikasi Laporan Guru - Tab Game Operasi:**
   - Buka modal Laporan Guru.
   - Cek tab default "Nilai Game Operasi": Menampilkan 45 siswa dengan kolom Penjumlahan, Pengurangan, Perkalian, Pembagian, Rata-Rata, dan Status.
   - Klik tombol "Unduh PDF Game (.pdf)" -> Pastikan file `.pdf` terunduh atau jendela cetak PDF terbuka dengan format Kop resmi.
3. **Verifikasi Laporan Guru - Tab Arena Duel:**
   - Klik tab "Rekap Arena Duel" -> Menampilkan 45 siswa dengan Menang, Kalah, Total Main, Total Skor, serta Riwayat Duel.
   - Klik tombol "Unduh PDF Arena (.pdf)" -> Pastikan file `.pdf` terunduh dengan format Kop resmi.
