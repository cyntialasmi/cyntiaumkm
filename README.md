# Cyntia Indomaret — Katalog Produk UMKM + Pemesanan WhatsApp

Aplikasi katalog digital interaktif untuk **Cyntia Indomaret**, dirancang untuk menampilkan produk-produk lokal berkualitas tinggi (dari dapur rumahan hingga kerajinan tangan) dan mempermudah pelanggan melakukan pemesanan langsung melalui WhatsApp hanya dalam beberapa klik.

Aplikasi ini dibangun menggunakan arsitektur modern Next.js 16 dengan Server Components, Server Actions, Tailwind CSS 4, dan backend Supabase (Database & Auth).

---

## Fitur Utama

### 🛍️ Untuk Pelanggan (Pengunjung)
- **Katalog Produk Terintegrasi Database (US-01):** Menampilkan seluruh produk toko secara *server-side* langsung dari tabel Supabase dengan kartu produk yang rapi, harga dalam format Rupiah, dan status jika katalog kosong.
- **Halaman Detail Produk (US-02):** Informasi rinci setiap produk yang memuat foto berkualitas, kategori, nama, harga, dan deskripsi lengkap, dilengkapi penanganan halaman 404 jika produk tidak ditemukan.
- **Pemesanan Cepat via WhatsApp (US-03):** Tombol pemesanan langsung yang membuka WhatsApp dengan draf pesan otomatis yang telah terisi nama produk dan harga tanpa perlu mengetik ulang.

### 🔐 Untuk Pemilik Toko (Admin)
- **Autentikasi Admin Aman (US-04):** Sistem login aman berbasis email dan password menggunakan Supabase Auth dan cookie sesi terenkripsi (`@supabase/ssr`), serta fitur keluar (*logout*).
- **Ganti Password (US-05):** Pengelolaan kredensial pemilik toko dengan validasi ketat di sisi server (minimal 8 karakter dan konfirmasi kecocokan).
- **Proteksi Akses Rute Admin (US-06):** Perlindungan rute `/admin` menggunakan proxy Next.js 16 (`proxy.js`), di mana pengunjung yang belum terautentikasi otomatis dialihkan ke halaman login.

---

## Teknologi yang Digunakan

- **Framework:** Next.js 16 (App Router, JavaScript, Turbopack)
- **Styling:** Tailwind CSS 4
- **Database & Autentikasi:** Supabase (`@supabase/supabase-js`, `@supabase/ssr`, PostgreSQL dengan Row Level Security)
- **Integrasi Komunikasi:** WhatsApp Click-to-Chat API
- **Deployment:** Vercel

---

## Struktur Folder

```
├── app/
│   ├── page.jsx                    # Katalog utama (US-01)
│   ├── layout.jsx                  # Root layout & header/footer
│   ├── not-found.jsx               # Halaman 404 kustom
│   ├── produk/[id]/page.jsx        # Detail produk (US-02)
│   └── admin/
│       ├── page.jsx                # Dasbor admin
│       ├── actions.js              # Server Actions (login, logout, ganti password)
│       ├── login/page.jsx          # Halaman masuk admin (US-04)
│       └── password/page.jsx       # Halaman ganti password (US-05)
├── components/                     # Komponen antarmuka (KartuProduk, TombolWhatsApp, NavAdmin, dll.)
├── lib/
│   ├── toko.js                     # Identitas toko & nomor WhatsApp
│   ├── format.js                   # Format mata uang Rupiah
│   └── supabase/                   # Inisialisasi client Supabase server & sesi cookie
├── docs/                           # Dokumentasi PRD, arsitektur, skema DB, dan checklist
├── proxy.js                        # Proxy middleware proteksi rute admin (US-06)
└── PROMPTS.md                      # Jurnal prompt pengembangan aplikasi
```

---

## Langkah Menjalankan Aplikasi

### 1. Salin Repositori & Instal Dependensi
```bash
git clone <url-repo-anda>
cd cyntiaumkm
npm install
```

### 2. Konfigurasi Environment Variables
Buat file `.env.local` di root proyek dengan variabel berikut (diambil dari dashboard Supabase):
```env
SUPABASE_URL=https://<project-ref>.supabase.co
SUPABASE_PUBLISHABLE_KEY=sb_publishable_...
SUPABASE_SECRET_KEY=sb_secret_...
```

> **Catatan Keamanan:** Semua variabel hanya digunakan di sisi server. Jangan menambahkan awalan `NEXT_PUBLIC_` untuk menjaga keamanan kredensial.

### 3. Siapkan Database
Jalankan skrip SQL di `docs/schema.sql` pada menu **SQL Editor** di dashboard Supabase untuk membuat tabel `produk` dan mengaktifkan Row Level Security (RLS).

### 4. Jalankan Server Pengembangan
```bash
npm run dev
```
Buka browser di `http://localhost:3000`.

---

## Tentang Aplikasi Ini

- **Nama usaha:** Cyntia Indomaret
- **Tagline:** Produk rumahan dari dapur dan perajin lokal, siap dipesan lewat WhatsApp.
- **Nomor WhatsApp Toko:** 6282283861533
- **Fitur wajib selesai:** US-01, US-02, US-03, US-04, US-05, US-06 (100% lengkap)
