# AutoJadwal-SMKN1 📅
> **Sistem Pelacak Jadwal & Direktori Guru Digital**
> SMK Negeri 1 Maluku Tengah

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Status](https://img.shields.io/badge/status-active-success.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

**AutoJadwal-SMKN1** adalah aplikasi web berbasis *mobile-first* yang dirancang untuk mempermudah siswa dan guru dalam mengakses jadwal pelajaran serta direktori guru secara cepat, modern, dan otomatis. 

Aplikasi ini dibangun menggunakan **Vanilla JavaScript, HTML, dan CSS murni** tanpa *framework* berat, sehingga sangat ringan dan cepat diakses bahkan menggunakan jaringan internet yang lambat.

---

## ✨ Fitur Utama

- [x] **Auto-Sync Data (Web Scraping)**: Menarik data daftar kelas dan guru secara otomatis langsung dari repositori GitHub Papan Jadwal Sekolah.
- [x] **Penyimpanan Lokal (Offline Support)**: Mengingat kelas terakhir yang dipilih menggunakan `localStorage`. Kamu tidak perlu mencari kelasmu setiap kali membuka aplikasi.
- [x] **Mode Gelap (Premium Dark Mode)**: Desain antarmuka modern dan elegan yang nyaman untuk mata, terinspirasi dari aplikasi *fintech* kelas atas.
- [x] **Smart PDF Preview**: Menampilkan preview jadwal Google Drive langsung di dalam aplikasi. Dilengkapi dengan trik CSS untuk menyembunyikan antarmuka Google Drive yang mengganggu, sehingga PDF terlihat lebih penuh dan *native*.
- [x] **Pencarian Instan**: Mencari kelas atau guru tanpa perlu menekan tombol *Enter* (realtime search).
- [x] **Aksesibilitas Tinggi**: Desain *touch target* minimal 44px yang ramah jempol dan aman untuk *notch* (safe-area-inset).

---

## 🛠️ Cara Kerja Sistem (Arsitektur)

Aplikasi ini menggunakan pendekatan **Decoupled Architecture** (tanpa backend/server). Proses sinkronisasi data dilakukan langsung di sisi klien (browser).

1. Saat web dibuka, fungsi `syncDataFromGithub()` akan berjalan.
2. Fungsi ini melakukan *fetch* HTTP ke URL web Papan Jadwal Sekolah (GitHub Pages milik guru).
3. Respons HTML mentah diekstrak menggunakan **Regex** (`/const KELAS\s*=\s*(\[[\s\S]*?\]);/`) untuk mengambil variabel `KELAS` dan `GURU`.
4. Data yang berhasil diekstrak diubah menjadi objek JavaScript menggunakan `eval()`.
5. Tampilan di-render ulang dengan data terbaru.
6. **Live Preview**: Ketika kartu kelas/guru diklik, sistem akan mengarahkan pengguna ke *endpoint* `preview` Google Drive (`https://drive.google.com/file/d/{ID}/preview`).

---

## 🚀 Cara Menggunakan & Deploy

### Prasyarat
- Browser modern (Chrome, Safari, Firefox, Edge).
- Koneksi internet (untuk memuat data dan file PDF).

### Cara Deploy di GitHub Pages
1. Clone repository ini atau siapkan file secara lokal.
2. Pastikan file `index.html` dan `README.md` berada di direktori yang sama.
3. Buka terminal (Termux/CMD) di direktori proyek.
4. Jalankan inisialisasi Git:
   ```bash
   git init
   git add index.html README.md
   git commit -m "Initial commit: AutoJadwal-SMKN1"
   git branch -M main
   ```

5. Hubungkan ke repositori GitHub:
   ```bash
   git remote add origin https://github.com/Ikyletwar/AutoJadwal-SMKN1.git
   git push -u origin main
   ```
6. Buka pengaturan repositori di GitHub -> Pages.
7. Pada bagian Build and deployment, pilih Branch main, folder / (root), lalu klik Save.
8. Tunggu 1-2 menit, dan aplikasi dapat diakses melalui https://ikyletwar.github.io/AutoJadwal-SMKN1/.

---

📁 Struktur Data

Aplikasi ini tidak memerlukan file JSON atau database eksternal. Data kelas dan guru ditarik secara realtime dari repository web Papan Jadwal Sekolah yang dikelola oleh guru.

Struktur data yang di-scrape dari web guru:

```javascript
// Tipe data yang diekstrak
const KELAS = [
  { no: 13, tingkat: "XI", nama: "XI TJKT 1", id: "1VEpap9LQfYKn3zHUjR43xyQ6CoeVIIp3" },
  { no: 14, tingkat: "XI", nama: "XI TJKT 2", id: "1ZOcxvMS9cU1RQGuEqSdVUB8g_GsajbX_" }
];

const GURU = [
  { no: 1, nama: "A. Bahy, S.Pd., M.Pd", id: "1Db2EUmgpv4rL8lfItnPZIDUf3rQSlvdN" }
];
```

---

🎨 Tech Stack & Tips Modifikasi

· HTML5: Struktur semantik, tag meta untuk PWA (Progressive Web App) dasar.
· CSS3: Menggunakan variabel CSS (:root), Flexbox, CSS Grid, Animasi transisi, dan Glassmorphism.
· Vanilla JavaScript: DOM Manipulation, Fetch API, Regex parsing, localStorage API.

Mau ganti warna tema?
Buka file index.html, cari bagian :root di dalam tag <style>. Ubah kode hex pada --bg-base, --brand-primary, dan --brand-glow.

---

⚠️ Disclaimer & Catatan

· Aplikasi ini adalah proyek independen yang dibuat oleh siswa untuk mempermudah akses informasi jadwal. Data sepenuhnya milik SMK Negeri 1 Maluku Tengah.
· Sistem scraping akan gagal jika pihak sekolah mengubah struktur variabel const KELAS atau const GURU di web mereka. Jika gagal, aplikasi akan otomatis fallback ke data dummy.
· Fitur Smart PDF Preview sangat bergantung pada kebijakan Google Drive. Pastikan sharing file diatur ke "Anyone with the link can view".

---

👨‍💻 Author & Credits

Dikembangkan dengan ❤️ oleh:

· Hizkia Letwar (Kelas XI TJKT 1) - Frontend Developer
· A. Bahy, S.Pd., M.Pd - Data Provider (Papan Jadwal Sekolah)

"Teknologi terbaik adalah yang bisa membantu banyak orang, bukan yang paling rumit."
