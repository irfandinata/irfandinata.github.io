# EcoRumah

Website Edukasi Hemat Energi & Rumah Ramah Lingkungan
**SDG 7 (Energi Bersih dan Terjangkau) dan SDG 13 (Penanganan Perubahan Iklim)**

Proyek UTS Mata Kuliah Pemrograman Web — Responsive Educational Website.

---

## 1. Anggota Kelompok

| No | Nama | NIM | Tugas |
|----|------|-----|-------|
| 1 | Gede Irfandinata Kusuma | 2515091020 | index HTML dan index CSS |
| 2 | I Gede Dibya Adinatha Mahasanti|2515091071| Panduan HTML dan Panduan css |
| 3 | Nur Asima Manik | 2515091006 | html edukasi dan css edukasi |
| 4 | Aqif Sultan Maulana | 2515091112 | tentang html dan tentang css |

---

## 2. Judul, Tema, dan Sasaran Pengguna

- **Judul:** EcoRumah – Mewujudkan Rumah Ramah Lingkungan & Hemat Energi
- **Tema:** Hemat Energi – Rumah Ramah Lingkungan (tema nomor 6)
- **SDGs:** SDG 7 dan SDG 13
- **Sasaran pengguna:** masyarakat umum, terutama keluarga atau rumah tangga yang ingin menghemat pemakaian listrik di rumah.

---

## 3. Tujuan, Manfaat, dan Deskripsi Halaman

### Tujuan
Memberikan edukasi sederhana tentang cara menghemat energi listrik di rumah, mulai dari pemahaman konsep, fakta konsumsi energi, sampai langkah praktis yang bisa langsung dilakukan.

### Manfaat
- Pengunjung memahami peralatan rumah tangga mana yang paling banyak memakai energi.
- Pengunjung mendapat langkah praktis untuk mengurangi tagihan listrik.
- Ikut mendukung pengurangan emisi karbon dari pemakaian listrik berbahan bakar fosil.

### Deskripsi Setiap Halaman

| Halaman | File | Isi |
|---|---|---|
| Beranda | `index.html` | Hero dengan foto penuh, kotak statistik energi rumah tangga, alasan pentingnya hemat energi, dan cuplikan 4 langkah dari halaman Panduan. |
| Edukasi | `edukasi.html` | Penjelasan SDG 7 dan SDG 13, serta fakta konsumsi energi rumah tangga beserta sumbernya. |
| Panduan | `panduan.html` | Empat langkah praktis hemat listrik, masing-masing dengan foto. |
| Artikel | `artikel.html` | Daftar artikel berbentuk kartu dan dua artikel lengkap: Zero Energy Building dan Ventilasi Silang. |
| Tentang | `tentang.html` | Tujuan website, anggota kelompok, daftar referensi, dan atribusi foto. |

---

## 4. Teknologi yang Digunakan

- **HTML5** dengan elemen semantik (`header`, `nav`, `main`, `section`, `article`, `footer`)
- **CSS3** eksternal, satu file CSS untuk setiap halaman
- **Flexbox** dan **CSS Grid** untuk tata letak
- **CSS Media Queries** untuk tampilan tablet dan smartphone
- **CSS Variables** (`:root`) untuk warna dan font
- **Font Segoe UI** (font bawaan Windows) dengan cadangan `sans-serif`, tanpa memuat font dari internet
- **GitHub Pages** untuk publikasi



---

## 5. Penjelasan Implementasi

### 5.1 Struktur HTML Semantik
Setiap halaman memakai susunan yang sama: `header` berisi navigasi, `main` berisi konten, dan `footer` di bagian bawah. Konten utama dibagi dengan `section`, sedangkan isi yang bisa berdiri sendiri (kartu dan artikel) memakai `article`.

```html
<header>
    <nav class="navbar"> ... </nav>
</header>

<main>
    <section class="section-block">
        <h2>Judul Bagian</h2>
        <article class="card"> ... </article>
    </section>
</main>

<footer> ... </footer>
```

Dengan elemen semantik, browser dan pembaca layar (screen reader) bisa mengenali fungsi tiap bagian halaman.

### 5.2 Navigasi Antarhalaman
Menu yang sama dipasang di kelima halaman. Halaman yang sedang dibuka diberi class `active` supaya pengunjung tahu sedang berada di mana.

```html
<ul class="nav-links">
    <li><a href="index.html">Beranda</a></li>
    <li><a href="edukasi.html" class="active">Edukasi</a></li>
    ...
</ul>
```

```css
/* Setiap menu berbentuk "pil" */
.nav-links a {
    display: inline-block;
    padding: 0.6rem 1.1rem;
    border-radius: 999px;
    color: var(--white);
}

/* Menu halaman yang sedang dibuka: pil putih */
.nav-links a.active {
    background: var(--white);
    color: var(--dark-color);
}
```

`border-radius: 999px` membuat sudut menu membulat penuh sehingga berbentuk pil. Di halaman selain Beranda, `header` dibuat `position: sticky; top: 0;` agar navbar tetap terlihat saat halaman di-scroll.

### 5.3 CSS Eksternal dan Variabel Warna
Setiap halaman memanggil satu file CSS miliknya sendiri, misalnya:

```html
<link rel="stylesheet" href="css/edukasi.css">
```

Isi setiap file CSS diurutkan mengikuti struktur HTML-nya: dasar halaman, `header`, `main`, lalu `footer`, dan diakhiri media queries. Warna utama disimpan sebagai variabel di `:root` agar mudah diganti dan konsisten.

```css
:root {
    --primary-color: #2e7d32;   /* Hijau Lingkungan */
    --secondary-color: #fbc02d; /* Kuning Energi/Matahari */
    --dark-color: #1b5e20;
}
```

### 5.4 Flexbox
Flexbox dipakai untuk menyusun elemen dalam satu baris, misalnya navbar: logo di kiri dan menu di kanan.

```css
.navbar {
    display: flex;
    justify-content: space-between; /* logo kiri, menu kanan */
    align-items: center;            /* sejajar secara vertikal */
}
```

Di Beranda, Flexbox dengan `flex-wrap` dipakai untuk baris foto dan teks yang selang-seling. Class `terbalik` membalik urutannya sehingga foto pindah ke kanan.

```css
.alasan-item {
    display: flex;
    flex-wrap: wrap;   /* turun ke baris baru jika layar sempit */
    gap: 3rem;
}

.alasan-item.terbalik {
    flex-direction: row-reverse;
}

.alasan-item img {
    flex: 1 1 380px;   /* lebar dasar 380px, boleh membesar dan mengecil */
}
```

### 5.5 CSS Grid
CSS Grid dipakai untuk kartu di halaman Edukasi dan Artikel.

```css
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
}
```

`repeat(auto-fit, minmax(280px, 1fr))` artinya: buat kolom sebanyak yang muat, dengan lebar minimal 280px. Di layar lebar kartu tampil berdampingan, sedangkan di HP otomatis menjadi satu kolom tanpa perlu media query.

Di halaman Edukasi, Grid juga dipakai untuk membagi foto dan daftar fakta dengan perbandingan kolom 1 : 1,5.

```css
.fakta-wrapper {
    display: grid;
    grid-template-columns: 1fr 1.5fr;
}
```

### 5.6 Media Queries (Responsif)
Website dirancang untuk desktop terlebih dahulu, lalu disesuaikan untuk layar yang lebih kecil.

```css
/* Tablet (lebar <= 768px) */
@media (max-width: 768px) {
    .navbar {
        flex-direction: column;   /* logo di atas, menu di bawah */
    }

    .fakta-wrapper {
        grid-template-columns: 1fr;  /* foto pindah ke atas daftar */
    }
}

/* Smartphone (lebar <= 480px) */
@media (max-width: 480px) {
    .nav-links {
        flex-direction: column;   /* menu tersusun ke bawah */
        align-items: center;
    }
}
```

Website diuji pada lebar 1440px (desktop), 768px (tablet), dan 375px (smartphone).

### 5.7 Hero dan Kotak Statistik di Beranda
Foto latar hero diberi lapisan hijau gelap transparan dengan `linear-gradient` agar teks putih tetap terbaca.

```css
.hero {
    background: linear-gradient(rgba(12, 40, 16, 0.65), rgba(12, 40, 16, 0.65)),
                url("../Gambar/photo index.avif") center 40% / cover no-repeat;
}
```

Kotak statistik dinaikkan dengan margin negatif sehingga menimpa bagian bawah hero. `position: relative` membuat kotak tampil di atas foto.

```css
.stats {
    position: relative;
    margin-top: -90px;
}
```

### 5.8 Foto Tidak Gepeng
Semua foto memakai `object-fit: cover` supaya foto dipotong rapi mengikuti ukuran kotaknya, bukan ditarik sampai gepeng.

```css
.card img {
    width: 100%;
    height: 180px;
    object-fit: cover;
}
```

### 5.9 Link ke Artikel Lengkap
Kartu di halaman Artikel berisi link ke artikel lengkap di halaman yang sama memakai `id`. `scroll-margin-top` memberi jarak agar judul artikel tidak tertutup navbar.

```html
<a href="#zero-energy-building" class="baca-link">Baca selengkapnya →</a>
...
<article class="section-block artikel-isi" id="zero-energy-building">
```

```css
.artikel-isi {
    scroll-margin-top: 110px;
}
```

---

## 6. Struktur Folder

```
UTS/
├── index.html        → Beranda
├── edukasi.html      → Edukasi
├── panduan.html      → Panduan
├── artikel.html      → Artikel
├── tentang.html      → Tentang & Referensi
├── README.md         → Dokumentasi proyek
├── css/
│   ├── index.css     → gaya halaman Beranda
│   ├── edukasi.css   → gaya halaman Edukasi
│   ├── panduan.css   → gaya halaman Panduan
│   ├── artikel.css   → gaya halaman Artikel
│   └── tentang.css   → gaya halaman Tentang
└── Gambar/           → semua foto 
```

---

## 7. Website dan Repository

- **Website (GitHub Pages):** `https://irfandinata.github.io/`
- **Repository:** `https://github.com/irfandinata/irfandinata.github.io`

---

## 8. Referensi

### Referensi Informasi
- Kementerian ESDM. (2017). [Ini Dia Pentingnya Peran Rumah Tangga dalam Konservasi Energi](https://esdm.go.id/id/media-center/arsip-berita/ini-dia-pentingnya-peran-rumah-tangga-dalam-konservasi-energi).
- Kementerian ESDM. (2025). [Beri Kemudahan Pemilihan Alat Elektronik, Pemerintah Terapkan Standar Label Hemat Energi Sejak 2015](https://www.esdm.go.id/id/media-center/arsip-berita/beri-kemudahan-pemilihan-alat-elektronik-pemerintah-terapkan-standar-label-hemat-energi-sejak-2015).
- Kementerian ESDM. (2012). [Peraturan Menteri ESDM Nomor 13 Tahun 2012 tentang Penghematan Pemakaian Tenaga Listrik](https://jdih.esdm.go.id/storage/document/Permen%20ESDM%2013%202012.pdf).
- Kementerian ESDM. (2024). [Peraturan Menteri ESDM Nomor 2 Tahun 2024 tentang Pembangkit Listrik Tenaga Surya Atap](https://jdih.esdm.go.id/storage/document/Permen%20ESDM%20Nomor%202%20Tahun%202024.pdf).
- Bisnis.com. (2024). [Skema Ekspor Listrik PLTS Atap Dihapus, Ini Insentif yang Dapat Dinikmati Pelanggan](https://ekonomi.bisnis.com/read/20240225/44/1743805/skema-ekspor-listrik-plts-atap-dihapus-ini-insentif-yang-dapat-dinikmati-pelanggan).
- Lawrence Berkeley National Laboratory. [Standby Power](https://standby.lbl.gov/).
- U.S. Department of Energy. [Guide to Energy-Efficient Lighting](https://www.energy.gov/sites/prod/files/guide_to_energy_efficient_lighting.pdf).
- U.S. Department of Energy. (2015). A Common Definition for Zero Energy Buildings, diringkas dalam [EC&M: DOE Releases Common Definition for Zero Energy Buildings](https://www.ecmweb.com/renewables/article/20900683/doe-releases-common-definition-for-zero-energy-buildings).
- Building Performance, Pemerintah Selandia Baru. [Passive Ventilation](https://building.govt.nz/getting-started/smarter-homes-guides/air-quality-moisture-and-ventilation/passive-ventilation).
- Kartikawati, D., & Pramesti, P. U. (2024). [Evaluasi Aspek Penghawaan Alami Terkait Sistem Ventilasi Bangunan Berdasarkan Standar Nasional Indonesia (SNI)](https://ejurnal.undana.ac.id/index.php/gewang/article/view/15188). *GEWANG*, 6(1), 53–60.
- United Nations. [SDG 7: Affordable and Clean Energy](https://sdgs.un.org/goals/goal7) dan [SDG 13: Climate Action](https://sdgs.un.org/goals/goal13).

### Atribusi Foto
Semua foto berasal dari [Unsplash](https://unsplash.com) dan bebas digunakan di bawah [Unsplash License](https://unsplash.com/license).

| Halaman | Foto |
|---|---|
| Beranda | [rumah kayu (hero & navbar)](https://images.unsplash.com/photo-1774597998353-2b8be5199a01), [panel surya](https://images.unsplash.com/photo-1624397640148-949b1732bb0a), [lampu](https://images.unsplash.com/photo-1532007271951-c487760934ae), [bangunan hijau](https://images.unsplash.com/photo-1556983852-43bf21186b2a) |
| Edukasi | [turbin angin](https://images.unsplash.com/photo-1548337138-e87d889cc369), [gunung es](https://images.unsplash.com/photo-1562089727-90aa996a6f18), [AC di ruang keluarga](https://images.unsplash.com/photo-1761330440311-16e160cad236) |
| Panduan (juga di Beranda) | [jendela](https://images.unsplash.com/photo-1495524455245-b0f961d738a9), [steker](https://images.unsplash.com/photo-1586943029669-98ae685c5c4c), [AC dinding](https://images.unsplash.com/photo-1759772238012-9d5ad59ae637), [dapur & kulkas](https://images.unsplash.com/photo-1484154218962-a197022b5858) |
| Artikel | [rumah berpanel surya](https://images.unsplash.com/photo-1655300256335-beef51a914fe), [jendela kayu](https://images.unsplash.com/photo-1534175262708-ebf71ac916c2) |
| Tentang | [mahasiswa di depan laptop](https://unsplash.com/photos/diverse-group-of-students-gathered-around-laptop-kp7qkHTgSKc) |
