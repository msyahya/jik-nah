# Spesifikasi UI/UX & Dekonstruksi Desain UNESCO untuk WordPress
**Tema Proyek:** Portal Representatif Organisasi / Lembaga Budaya Nahdliyin (Jombang Ibu Kota Nahdliyin / JIK-NAH)  
**Tumpukan Teknologi:** WordPress CMS, Custom Post Types (CPT UI / ACF / Pods), Advanced Custom Fields (ACF Pro), Tailwind CSS  
**Referensi Utama:** [unesco.org](https://www.unesco.org/)

---

## 1. Analisis Visual & Brand Identity (Turunan Logo)

Logo memiliki identitas visual bernuansa kebangsaan dan nilai Nahdliyin (Merah Putih, Hijau Nahdliyin, Emas/Kuning Tali Jagat & Bintang, serta Biru Bumi). Agar tetap berwibawa, modern, dan bernuansa institusional layaknya UNESCO, warna-warna ini dikelompokkan ke dalam sistem token Tailwind CSS.

### 1.1. Color Palette Tokens (Tailwind Configuration)

| Peran Token | Kode Hex | Deskripsi & Penggunaan UI |
| :--- | :--- | :--- |
| **Primary (Brand Green)** | `#0D6E3F` | Warna identitas utama (Aksen NU, tombol primer, active link header, icon aksen) |
| **Primary Dark** | `#084A2A` | Hover state tombol primer, top bar dark option, badge khusus |
| **Secondary (National Red)** | `#D32F2F` | Mengambil elemen merah bendera; dipakai untuk *breaking news*, alert bar, label kategori *urgent* |
| **Accent Gold (Tali & Bintang)**| `#E5A932` | Pembeda visual untuk rating, highlight garis batas (border decor), icon kehormatan |
| **Earth Cyan/Blue** | `#1976D2` | Aksen sekunder data/infografis (mengadopsi warna bola dunia) |
| **Neutral 900 (Text Body)** | `#1E293B` | Teks utama (`slate-800` / `slate-900`) untuk keterbacaan tinggi |
| **Neutral 100 (Surface Light)**| `#F8FAFC` | Latar belakang section kartu konten |
| **Base White** | `#FFFFFF` | Background utama halaman & kartu putih |

```js
// tailwind.config.js snippet
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: {
          green: '#0D6E3F',
          'green-dark': '#084A2A',
          red: '#D32F2F',
          gold: '#E5A932',
          blue: '#1976D2',
        }
      },
      fontFamily: {
        sans: ['Inter', 'system-ui', 'sans-serif'],
        serif: ['Merriweather', 'serif'], // opsional untuk headline artikel / kutipan
      }
    }
  }
}
```

---

## 2. Dekonstruksi Struktur UI/UX UNESCO

Situs UNESCO memiliki formula desain khas lembaga global multilateral: **Authority, High Scannability, Dynamic Editorial, dan Deep Hierarchy**.

### 2.1. Anatomi Layout Utama

1. **Utility Top Bar:**
   - Navigasi global mikro (Bahasa/Pilihan Wilayah, Aksesibilitas, Search trigger).
2. **Main Header & Navigation Bar:**
   - Logo kiri (Logo JIK-NAH + teks branding).
   - Menu horizontal dengan mega-menu dropdown (Pilar Utama: *Keahlian, Warisan & Situs, Program Strategis, Riset & Publikasi, Berita*).
   - Tombol aksi utama / CTA di kanan (misal: "Dokumentasi", "Pustaka Digital", atau "Kontribusi").
3. **Hero Editorial Section:**
   - Desain asimetris atau split-grid: 1 Berita Utama besar di kiri (foto rasio 16:9 dengan overlay judul tebal dan kicker category) + 2-3 Berita Penting vertikal di kanan.
4. **Thematic Pillars / Key Themes (Grid UNESCO style):**
   - 4-5 kolom kartu kategori dengan visual minimalis, tipografi tegas, dan hover zoom effect pada thumbnail.
5. **Impact / Data Figures Counter:**
   - Strip monokrom/hijau tua dengan angka statistik besar (Jumlah situs cagar, pesantren terdata, dokumen arsip, dsb.).
6. **Featured Publications & Stories (Card Slider / Grid):**
   - Kartu vertikal bersih dengan aspect ratio 3:4 atau 16:9, label kategori pill-style, tanggal, dan judul singkat.
7. **Footer Institusional 3-Tier:**
   - Tier 1: Form langganan warta berita (Newsletter).
   - Tier 2: Sitemap direktori (4-5 kolom navigasi link).
   - Tier 3: Copyright, Legalitas, Kebijakan Privasi, dan tautan sosial media.

---

## 3. Struktur Informasi & Arsitektur Menu (Bahasa Indonesia)

* **Beranda**
* **Tentang Kami**
  * Profil & Sejarah Jombang Kota Nahdliyin
  * Visi, Misi & Khidmah
  * Struktur Organisasi / Tokoh Penggerak
* **Pilar Program (What We Do)**
  * Pelestarian Warisan Budaya & Tradisi
  * Pendidikan & Literasi Pesantren
  * Riset, Naskah & Pustaka Digital
  * Pemberdayaan Sosial & Kemasyarakatan
* **Situs & Warisan Sejarah (Heritage)**
  * Direktori Makam Auliya & Muassis
  * Cagar Budaya & Bangunan Bersejarah
  * Peta Interaktif Warisan
* **Kabar & Publikasi**
  * Berita & Siaran Pers
  * Opini & Wawasan
  * Dokumen Resmi & Jurnal Digital
  * Galeri Foto & Multimedia
* **Agenda & Kegiatan**
* **Kontak & Pengaduan**

---

## 4. Pemetaan WordPress CPT & ACF (Custom Fields)

Untuk memastikan pengelola web mudah menginput data tanpa merusak tata letak, data dipisahkan ke dalam Custom Post Type:

### 4.1. Custom Post Types (CPT)
1. `cpt_heritage` (**Warisan & Situs Sejarah**)
2. `cpt_program` (**Program Unggulan**)
3. `cpt_publication` (**Riset & Publikasi / Dokumen**)
4. `cpt_event` (**Agenda Kegiatan**)
5. Default `post` (**Berita & Artikel**)

### 4.2. Skema Field ACF

#### A. CPT: Warisan & Situs (`cpt_heritage`)
- `lokasi_situs` (Text - Nama Kecamatan/Desa di Jombang)
- `titik_koordinat` (Google Maps / Lat-Long Text)
- `tahun_penetapan_estimasi` (Text/Number)
- `status_cagar` (Select: Terdaftar Nasional, Daerah, Koleksi Khusus)
- `galeri_foto` (Gallery)
- `dokumen_kajian` (File upload / PDF)

#### B. CPT: Publikasi / Dokumen (`cpt_publication`)
- `tipe_dokumen` (Select: Jurnal, Buku Putih, Arsip Naskah, Buletin)
- `penulis_kontributor` (Text)
- `berkas_pdf` (File Download)
- `nomor_arsip_isbn` (Text)

#### C. Post Berita (Tambahan Field)
- `is_headline` (True/False - Untuk memfilter masuk ke Hero Utama UNESCO style)
- `kicker_label` (Text - Sub-label kecil di atas judul, misal: *INISIATIF LOKAL*)

---

## 5. Implementasi UI / Tailwind CSS Component Recipes

### 5.1. Header & Mega Menu Nav (Tailwind)
```html
<header class="w-full bg-white border-b border-slate-200 sticky top-0 z-50">
  <!-- Top Bar -->
  <div class="bg-brand-green text-white text-xs py-1.5 px-4 sm:px-8 flex justify-between items-center">
    <div class="flex space-x-4">
      <span>Portal Resmi Jombang Ibu Kota Nahdliyin</span>
    </div>
    <div class="flex items-center space-x-3">
      <a href="/arsip" class="hover:underline">Pustaka Digital</a>
      <span>|</span>
      <a href="/kontak" class="hover:underline">Bantuan</a>
    </div>
  </div>

  <!-- Main Navbar -->
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
    <div class="flex items-center space-x-3">
      <img src="logo.png" alt="Logo JIK-NAH" class="h-14 w-auto">
      <div class="leading-tight">
        <span class="block font-bold text-lg text-slate-900 tracking-tight">JOMBANG</span>
        <span class="block text-xs font-semibold text-brand-green uppercase tracking-wider">Ibu Kota Nahdliyin</span>
      </div>
    </div>

    <!-- Nav Links Desktop -->
    <nav class="hidden lg:flex items-center space-x-8 text-sm font-medium text-slate-700">
      <a href="#" class="text-brand-green font-semibold">Beranda</a>
      <a href="#" class="hover:text-brand-green transition-colors">Tentang Kami</a>
      <a href="#" class="hover:text-brand-green transition-colors">Pilar Program</a>
      <a href="#" class="hover:text-brand-green transition-colors">Situs & Warisan</a>
      <a href="#" class="hover:text-brand-green transition-colors">Publikasi</a>
      <a href="#" class="hover:text-brand-green transition-colors">Agenda</a>
    </nav>

    <!-- Right Action -->
    <div class="hidden sm:flex items-center space-x-4">
      <button class="bg-brand-green hover:bg-brand-green-dark text-white text-sm font-semibold px-4 py-2.5 rounded-none border-b-2 border-brand-gold transition duration-200">
        Jelajahi Arsip
      </button>
    </div>
  </div>
</header>
```

### 5.2. UNESCO-Style Hero Editorial Grid
```html
<section class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
  <div class="grid grid-cols-1 lg:grid-cols-12 gap-6">
    
    <!-- Hero Main (Left 8 Cols) -->
    <div class="lg:col-span-8 group relative overflow-hidden bg-slate-900 min-h-[460px] flex items-end">
      <img src="featured-image.jpg" alt="Headline" class="absolute inset-0 w-full h-full object-cover opacity-80 group-hover:scale-105 transition-transform duration-500 ease-out">
      <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/40 to-transparent"></div>
      
      <div class="relative p-6 sm:p-8 text-white z-10">
        <span class="inline-block bg-brand-red text-white text-xs font-bold uppercase tracking-wider px-2.5 py-1 mb-3">
          Warisan Sejarah
        </span>
        <h1 class="text-2xl sm:text-4xl font-bold leading-tight mb-3 group-hover:text-amber-300 transition-colors">
          Digitalisasi Manuskrip Kuno Pesantren Jombang Menuju Pengakuan Cagar Budaya Dunia
        </h1>
        <p class="text-slate-300 text-sm line-clamp-2 max-w-2xl mb-4 font-light">
          Langkah konkret pelestarian ratusan kitab peninggalan muassis sebagai fondasi peradaban literasi Islam Nusantara.
        </p>
        <span class="text-xs text-slate-400">06 November 2026 • 5 menit baca</span>
      </div>
    </div>

    <!-- Secondary Articles (Right 4 Cols) -->
    <div class="lg:col-span-4 flex flex-col justify-between space-y-4">
      <!-- Item 1 -->
      <article class="bg-slate-50 border-t-2 border-brand-green p-5 hover:shadow-md transition">
        <span class="text-xs font-semibold text-brand-green uppercase tracking-wider">Pendidikan</span>
        <h3 class="font-bold text-slate-900 text-base mt-1 hover:text-brand-green cursor-pointer">
          Revitalisasi Kurikulum Turats di Era Transformasi Digital
        </h3>
        <p class="text-xs text-slate-500 mt-2">Ditinjau oleh Tim Riset Pesantren</p>
      </article>

      <!-- Item 2 -->
      <article class="bg-slate-50 border-t-2 border-brand-gold p-5 hover:shadow-md transition">
        <span class="text-xs font-semibold text-brand-gold uppercase tracking-wider">Agenda Mendatang</span>
        <h3 class="font-bold text-slate-900 text-base mt-1 hover:text-brand-green cursor-pointer">
          Halaqah Internasional: Refleksi Perjuangan Muassis Nahdliyin
        </h3>
        <p class="text-xs text-slate-500 mt-2">12 November 2026 • Tebuireng, Jombang</p>
      </article>

      <!-- Item 3 -->
      <article class="bg-slate-50 border-t-2 border-brand-blue p-5 hover:shadow-md transition">
        <span class="text-xs font-semibold text-brand-blue uppercase tracking-wider">Publikasi Riset</span>
        <h3 class="font-bold text-slate-900 text-base mt-1 hover:text-brand-green cursor-pointer">
          Laporan Tahunan Status Pelestarian Makam & Kompleks Bersejarah
        </h3>
        <p class="text-xs text-slate-500 mt-2">PDF Unduh (14.2 MB)</p>
      </article>
    </div>

  </div>
</section>
```

---

## 6. Rekomendasi UX & Accessibility (a11y)

1. **Rasio Kontras Tinggi:** Pastikan teks putih di atas latar hijau Nahdliyin memenuhi standar WCAG AAA (menggunakan warna `#0D6E3F` atau `#084A2A`).
2. **Sharp / Flat Edge Estetika UNESCO:** UNESCO tidak banyak menggunakan `rounded-2xl` atau `rounded-full` pada kartu utama; gunakan sudut tajam (`rounded-none` atau `rounded-sm`) untuk menegaskan kesan resmi, monumental, dan kredibel.
3. **Typography Scaling:** Buat hierarki ukuran tipografi yang jelas antara Kicker (11-12px bold uppercase), Heading (24-36px semibold/bold), dan Excerpt teks (14-15px regular).