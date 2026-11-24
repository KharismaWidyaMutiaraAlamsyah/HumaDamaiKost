# 🏠 Huma Damai Kost — Sistem Informasi & Manajemen Penyewaan Kamar

**Live Demo:** [https://resplendent-flan-575828.netlify.app](https://resplendent-flan-575828.netlify.app)

Sistem informasi berbasis web untuk **Huma Damai Kost** (Palangka Raya, Kalimantan Tengah) yang memadukan katalog ketersediaan kamar *real-time* bagi calon penyewa dengan panel pengelolaan unit, reservasi (booking), dan arsip riwayat penghuni bagi pengelola kost.

---

## 📋 Ringkasan Sistem

Aplikasi ini dirancang sebagai *Single Page Application* (SPA) ringan tanpa memerlukan *backend server* terpisah. Seluruh status kamar disinkronkan secara langsung menggunakan **Firebase Realtime Database**, sedangkan akses perubahan data dilindungi menggunakan **Firebase Authentication** dan **Database Security Rules**.

---

## ✨ Daftar Fitur Utama

### 1. Halaman Publik (Calon Penghuni)
* **Katalog Kamar Real-Time & Filter Tipe:** Menampilkan daftar kamar **Type A** (5 unit standar) dan **Type B** (3 unit lebih luas berstatus *Coming Soon*) lengkap dengan indikator ketersediaan (*Kosong*, *Ter-booking*, *Sudah Terisi*, *Coming Soon*).
* **Galeri Foto Interaktif (Lightbox Slider):** Pengunjung dapat mengklik foto pada kartu kamar untuk melihat detail ruangan (tampak depan, bagian dalam, kasur, lemari & wastafel, kamar mandi dalam, dan meteran listrik) dengan dukungan navigasi *keyboard* (`ArrowLeft`, `ArrowRight`, `Escape`).
* **Peta Lokasi Terintegrasi & Tata Tertib:** Dilengkapi *mini-map* Google Maps langsung pada kartu utama, tombol salin alamat instan, serta rincian tata tertib dan ketentuan pembayaran.

### 2. Kalkulasi Harga Otomatis
* Penyesuaian tarif bulanan otomatis berdasarkan tipe kamar yang dipilih (**Type A: Rp 1.400.000/bulan** dan **Type B: Rp 1.600.000/bulan**).
* Rincian nominal DP Booking tetap sebesar **Rp 400.000** terhitung otomatis pada formulir pemesanan maupun rekapitulasi admin.

### 3. Integrasi WhatsApp Otomatis
* Calon penghuni dapat mengisi formulir pemesanan (pilihan unit kosong, nama sesuai KTP, nomor HP, pekerjaan, dan estimasi tanggal masuk).
* Sistem secara otomatis menyusun format pesan terstruktur (*URL-encoded*) dan mengarahkannya ke WhatsApp pengelola untuk konfirmasi pembayaran DP dan pengiriman foto KTP.

### 4. Panel Admin CRUD & Arsip Penghuni
* **Autentikasi Admin Aman:** Login pengelola menggunakan **Firebase Authentication** (Email & Password).
* **Manajemen Data Kamar (CRUD):** Tambah unit baru, ubah status kamar (*Kosong*, *Booking*, *Terisi*, *Coming Soon*), perbarui data penghuni, dan verifikasi kelengkapan KTP.
* **Checkout & Arsip Mantan Penghuni:** Fitur *checkout* otomatis mengosongkan unit kamar dan memindahkan data penyewa lama ke tabel **Riwayat Mantan Penghuni**, lengkap dengan fitur **Check-in Ulang** jika penyewa lama kembali menyewa.

---

## 🛠️ Teknologi yang Digunakan

* **Frontend:** HTML5, Vanilla JavaScript (ES6+)
* **Styling:** Tailwind CSS (CDN) dengan palet warna kustom (*Huma Cream*, *Huma Brown*, *Huma Sage*)
* **Database & Auth:** Firebase Realtime Database & Firebase Authentication (v9 Compat SDK)
* **Peta & Integrasi:** Google Maps Embed API & WhatsApp Click-to-Chat API
* **Hosting:** Netlify

---

## 🔒 Konfigurasi & Keamanan Firebase

1. Salin `config.example.js` menjadi `config.js` dan masukkan konfigurasi proyek Firebase Anda. Pastikan `config.js` terdaftar di `.gitignore`.
2. Aktifkan metode login **Email/Password** di menu **Firebase Authentication** dan daftarkan akun admin.
3. Terapkan **Database Security Rules** berikut pada konsol Firebase Realtime Database agar data dapat dibaca publik tetapi hanya dapat diubah oleh admin yang terautentikasi:

```json
{
  "rules": {
    ".read": true,
    ".write": "auth != null"
  }
}