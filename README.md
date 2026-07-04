# 📊 Kalkulator IPK dan Transkrip Nilai

**Proyek Akhir — Algoritma dan Pemrograman**  
Universitas Al Azhar Indonesia | Semester Genap 2025/2026

| Nama Anggota | NIM |
|:-------------|:----|
| Achmad Zeehan Wardana | 0102525001 |
| Akrim Shulhi | 0102523009 |
| Habibie Rahman Abdillah | 0102525006 |
| Hanif Zakia Khoirunnisa | 0102524642 |

**Kelas:** IF25H  
**Dosen:** Tri Aji Nugroho, S.T., M.T.  
**Tanggal Pengumpulan:** 20 Juni 2026  

---

## Daftar Isi

1. [Deskripsi Proyek](#deskripsi-proyek)  
2. [Fitur Aplikasi](#fitur-aplikasi)  
3. [Cara Menjalankan](#cara-menjalankan)  
4. [Struktur Data](#struktur-data)  
5. [Daftar Fungsi](#daftar-fungsi)  
6. [Konsep Pemrograman yang Diterapkan](#konsep-pemrograman-yang-diterapkan)  
7. [Contoh Penggunaan](#contoh-penggunaan)  
8. [Test Cases](#test-cases)  
9. [Struktur File](#struktur-file)  
10. [Referensi](#referensi)  

---

## Deskripsi Proyek

Aplikasi **Kalkulator IPK dan Transkrip Nilai** adalah program konsol berbasis Python yang membantu mahasiswa Universitas Al Azhar Indonesia (UAI) dalam:

- Menghitung **Indeks Prestasi Semester (IPS)** dan **Indeks Prestasi Kumulatif (IPK)** secara otomatis menggunakan sistem bobot mutu SKS.
- Menampilkan **transkrip nilai** yang terformat rapi dan dikelompokkan per semester.
- Mensimulasikan **nilai minimum** yang dibutuhkan agar IPK mencapai target pada semester berikutnya.
- Menyediakan **statistik akademik** lengkap termasuk distribusi nilai huruf.

Proyek ini merupakan implementasi nyata dari seluruh konsep Algoritma dan Pemrograman yang dipelajari dari **Bab 1 hingga Bab 13**, mulai dari variabel, seleksi, perulangan, fungsi, string, list, dictionary, set, algoritma pencarian (searching), pengurutan (sorting), hingga analisis kompleksitas Big-O.

### Latar Belakang

Portal akademik UAI ([studentdesk.uai.ac.id](https://studentdesk.uai.ac.id)) tidak menyediakan fitur simulasi target IPK. Proses perhitungan manual juga rentan kesalahan dan memakan waktu. Aplikasi ini hadir sebagai solusi mandiri, efisien, dan mudah digunakan.

---

## Fitur Aplikasi

| No | Kode FR | Fitur | Deskripsi |
|:--:|:--------|:------|:----------|
| 1 | FR-1 | **Input Mata Kuliah** | Menambahkan data mata kuliah (kode, nama, SKS, nilai huruf, semester) dengan validasi lengkap |
| 2 | FR-2 | **Hitung IPS & IPK** | Menghitung IPS per semester dan IPK kumulatif menggunakan rata-rata berbobot SKS |
| 3 | FR-3 | **Tampilkan Transkrip** | Menampilkan transkrip nilai terformat per semester, lengkap dengan predikat kelulusan |
| 4 | FR-4 | **Cari Mata Kuliah** | Pencarian berdasarkan nama, kode, atau nilai huruf menggunakan linear search O(n) |
| 5 | FR-5 | **Urutkan Transkrip** | Pengurutan daftar mata kuliah berdasarkan 7 kriteria menggunakan Timsort O(n log n) |
| 6 | FR-6 | **Simulasi Target IPK** | Menghitung bobot mutu minimum yang diperlukan semester depan untuk mencapai target IPK |
| 7 | FR-7 | **Statistik Akademik** | Ringkasan statistik: total SKS, distribusi nilai, mata kuliah terbaik/terlemah, IPS per semester |
| 8 | FR-8 | **Hapus / Edit Data** | Menghapus atau memperbaiki data mata kuliah dengan konfirmasi (CRUD — Delete & Update) |
| — | — | **Data Demo** | Memuat 10 data mata kuliah contoh (2 semester) untuk keperluan pengujian dan demo |

---

## Cara Menjalankan

### Prasyarat

- Python **3.x** (tidak memerlukan library eksternal)
- Google Colab **atau** lingkungan Python lokal

### Langkah di Google Colab

```python
# 1. Jalankan semua sel secara berurutan (Runtime → Run All)
#    atau gunakan shortcut Ctrl + F9

# 2. Sel terakhir berisi entry point program:
if __name__ == "__main__":
    main()

# 3. Untuk memulai dengan data contoh, pilih menu 9 (Muat Data Demo)
#    saat program berjalan
```

### Langkah di Lokal (Terminal)

```bash
# Clone atau download file .ipynb, lalu jalankan:
jupyter notebook TA_AlPro_IF25H_KalkulatorIPKdanTranskrip.ipynb

# Atau konversi ke .py dan jalankan langsung:
jupyter nbconvert --to script TA_AlPro_IF25H_KalkulatorIPKdanTranskrip.ipynb
python TA_AlPro_IF25H_KalkulatorIPKdanTranskrip.py
```

### Navigasi Menu

Saat program berjalan, tekan angka sesuai pilihan dan tekan **Enter**:

```
╔══════════════════════════════════════════════════╗
║                MENU UTAMA                        ║
╠══════════════════════════════════════════════════╣
║  Status: 0 MK                     IPK: -         ║
╠──────────────────────────────────────────────────╣
║  1. Tambah Mata Kuliah                           ║
║  2. Hitung & Tampilkan Transkrip                 ║
║  3. Hitung IPS per Semester                      ║
║  4. Cari Mata Kuliah                             ║
║  5. Urutkan Daftar Mata Kuliah                   ║
║  6. Simulasi Target IPK                          ║
║  7. Statistik Akademik                           ║
║  8. Hapus / Edit Mata Kuliah                     ║
║  9. Muat Data Demo                               ║
║  0. Keluar                                       ║
╚══════════════════════════════════════════════════╝
```

> **Tips:** Tekan `9` terlebih dahulu untuk memuat 10 data demo, sehingga semua fitur langsung dapat diuji tanpa perlu input manual.

---

## Struktur Data

Pemilihan struktur data mengacu pada prinsip efisiensi akses dan operasi CRUD (Bab 7–8).

### Struktur Utama

| Variabel | Tipe | Kompleksitas Akses | Fungsi |
|:---------|:-----|:-------------------|:-------|
| `riwayat_mk` | `list of dict` | O(n) iterasi | Menyimpan seluruh riwayat mata kuliah |
| `kode_terdaftar` | `set` | O(1) lookup | Validasi duplikasi kode MK |
| `BOBOT_MUTU` | `dict` (konstanta) | O(1) lookup | Konversi nilai huruf ke bobot mutu numerik |
| `NILAI_VALID` | `set` (konstanta) | O(1) lookup | Validasi nilai huruf yang diizinkan |

### Format Entri Mata Kuliah (dict)

```python
{
    "kode"       : "IF1001",                  # str  — kode unik mata kuliah
    "nama"       : "Algoritma dan Pemrograman", # str  — nama mata kuliah
    "sks"        : 3,                          # int  — jumlah SKS (1–6)
    "nilai"      : "A",                        # str  — nilai huruf
    "bobot_mutu" : 4.0,                        # float — bobot mutu (0.0–4.0)
    "semester"   : 1                           # int  — nomor semester (1–14)
}
```

### Tabel Konversi Bobot Mutu

| Nilai Huruf | Bobot Mutu |
|:-----------:|:----------:|
| A | 4.0 |
| A- | 3.7 |
| B+ | 3.3 |
| B | 3.0 |
| B- | 2.7 |
| C+ | 2.3 |
| C | 2.0 |
| D | 1.0 |
| E | 0.0 |

---

## Daftar Fungsi

| No | Nama Fungsi | Parameter Utama | Return | Kompleksitas | FR |
|:--:|:------------|:----------------|:-------|:-------------|:--:|
| 1 | `input_valid()` | `prompt, tipe, boleh_kosong` | `str/int/float` | O(1) | — |
| 2 | `tambah_mk()` | — (menggunakan global) | `None` | O(1) amortisasi | FR-1 |
| 3 | `hitung_ipk()` | `daftar_mk=None` | `float` | O(n) | FR-2 |
| 4 | `hitung_ips()` | `semester` | `float` | O(n) | FR-2 |
| 5 | `tampilkan_transkrip()` | — | `None` | O(n log n) | FR-3 |
| 6 | `cari_mk()` | — | `None` | O(n) | FR-4 |
| 7 | `urutkan_mk()` | — | `None` | O(n log n) | FR-5 |
| 8 | `simulasi_target()` | — | `None` | O(n) + O(1) | FR-6 |
| 9 | `tampilkan_statistik()` | — | `None` | O(n) | FR-7 |
| 10 | `hapus_mk()` | — | `None` | O(n) | FR-8 |
| 11 | `muat_data_demo()` | — | `None` | O(k) | — |
| 12 | `tampilkan_header()` | — | `None` | O(1) | — |
| 13 | `tampilkan_menu()` | — | `None` | O(1) | — |
| 14 | `menu_ips_semester()` | — | `None` | O(n) | FR-2 |
| 15 | `main()` | — | `None` | O(1) dispatch | — |

### Fungsi Kunci — Penjelasan Singkat

**`hitung_ipk(daftar_mk=None)`**  
Menghitung IPK menggunakan formula rata-rata berbobot:  
`IPK = Σ(SKS × bobot_mutu) / Σ(SKS)`  
Menerima parameter opsional `daftar_mk` sehingga dapat digunakan oleh `hitung_ips()` maupun untuk kalkulasi kumulatif.

**`simulasi_target()`**  
Menggunakan formula balik rata-rata berbobot:  
`mutu_min = (target_ipk × (total_sks + sks_rencana) − total_bobot) / sks_rencana`  
Output otomatis diterjemahkan ke nilai huruf yang setara.

**`main()`**  
Menggunakan **dispatch table** (dictionary of functions) untuk routing menu:  
```python
menu_aksi = {"1": tambah_mk, "2": tampilkan_transkrip, ...}
menu_aksi[pilihan]()  # O(1) lookup — lebih efisien dari if-elif O(n)
```

---

## Konsep Pemrograman yang Diterapkan

| Bab | Konsep | Implementasi dalam Proyek |
|:---:|:-------|:--------------------------|
| Bab 2–4 | Variabel, Tipe Data, Seleksi | Variabel `total_bobot`, `total_sks`; seleksi `if nilai in NILAI_VALID` |
| Bab 4–5 | Perulangan & Fungsi | `while True` di menu utama; seluruh 15 fungsi bermodular |
| Bab 5 | Fungsi & Parameter | `hitung_ipk(daftar_mk=None)` dengan parameter default |
| Bab 6 | String | Format output transkrip menggunakan f-string dan string multiplication |
| Bab 7–8 | List, Tuple, Dictionary, Set | `riwayat_mk` (list), `BOBOT_MUTU` (dict), `kode_terdaftar` (set) |
| Bab 9 | Searching — Linear Search | `cari_mk()` menggunakan list comprehension O(n) |
| Bab 10 | Sorting | `urutkan_mk()` menggunakan `sorted()` Timsort O(n log n) |
| Bab 12–13 | Big-O & AI-Augmented | Komentar anotasi Big-O di setiap fungsi; AI Usage Log terlampir |

---

## Contoh Penggunaan

### Menghitung IPK dari Data Demo

```
Pilih menu: 9       ← Muat data demo (10 MK, 2 semester)
Pilih menu: 2       ← Tampilkan transkrip
```

Output yang diharapkan:

```
╔════════════════════════════════════════════════════════╗
║  Semester 1                                           ║
╠════════════════════════════════════════════════════════╣
║  Kode       Nama Mata Kuliah              SKS Nilai Mutu  ║
╠────────────────────────────────────────────────────────╣
║  IF1001     Algoritma dan Pemrograman      3     A   4.0  ║
║  IF1002     Matematika Diskrit             3    B+   3.3  ║
║  IF1003     Pengantar Ilmu Komputer        2     A   4.0  ║
║  UAI1001    Pendidikan Agama Islam         2     A   4.0  ║
║  UAI1002    Bahasa Indonesia               2    A-   3.7  ║
╠────────────────────────────────────────────────────────╣
║  Total SKS Semester : 12    IPS Semester : 3.83         ║
║  Total SKS Kumulatif: 12    IPK s.d. Smt ini: 3.83     ║
╚════════════════════════════════════════════════════════╝
```

### Simulasi Target IPK

```
Pilih menu: 6
IPK saat ini: 3.43
Target IPK  : 3.60
Rencana SKS : 24

→ Bobot Mutu Minimum: 3.88
→ Nilai minimum yang diperlukan: A- (Bobot Mutu ≥ 3.88)
```

### Mencari Mata Kuliah

```
Pilih menu: 4
Pilih kriteria: 1 (Berdasarkan Nama)
Kata kunci: "pemrograman"

→ Ditemukan 2 mata kuliah: 
   IF1001 — Algoritma dan Pemrograman | Semester 1 | Nilai A
   IF2001 — Pemrograman Berorientasi Objek | Semester 2 | Nilai B+
```

---

## Test Cases

| No | Test Case | Input | Expected Output | Status |
|:--:|:----------|:------|:----------------|:------:|
| 1 | Tambah MK valid | Kode: IF1001, Nama: Alpro, SKS: 3, Nilai: A, Semester: 1 | "✓ Mata kuliah 'Alpro' berhasil ditambahkan!" | ✅ |
| 2 | Tambah MK duplikat | Kode: IF1001 (sudah ada) | "⚠ Kode 'IF1001' sudah terdaftar." | ✅ |
| 3 | Tambah MK — SKS tidak valid | SKS: 0 atau 7 | "⚠ SKS harus antara 1 sampai 6." | ✅ |
| 4 | Tambah MK — Nilai tidak valid | Nilai: "Z" | "⚠ Nilai 'Z' tidak valid." | ✅ |
| 5 | Cari MK by nama | Keyword: "Alpro" | Menampilkan IF1001 | ✅ |
| 6 | Cari MK tidak ditemukan | Keyword: "xyz" | "Tidak ditemukan mata kuliah..." | ✅ |
| 7 | Hitung IPK — kosong | Tidak ada data | Menampilkan "⚠ Belum ada data" | ✅ |
| 8 | Simulasi — target tercapai | Target IPK < IPK saat ini | "✓ IPK Anda sudah melampaui target!" | ✅ |
| 9 | Simulasi — target mustahil | Target 4.0, SKS rencana kecil | "✗ Target IPK tidak dapat dicapai..." | ✅ |
| 10 | Sort berdasarkan nilai | Pilihan 5 (Nilai Tertinggi) | Urutan A, A-, B+, B, B-, C, D, E | ✅ |

---

## Struktur File

```
📁 Proyek Akhir — Kalkulator IPK
│
├── 📓 TA_AlPro_IF25H_KalkulatorIPKdanTranskrip.ipynb   ← Source code utama
├── 📄 Proposal_ProyekAkhir_KalkulatorIPK.docx           ← Dokumen proposal
├── 📄 README.md                                          ← File ini
└── 📄 AI_USAGE_LOG.md                                    ← Log penggunaan AI
```

---

## Referensi

1. Nugroho, T. A. (2026). *Algoritma dan Pemrograman: Panduan Lengkap untuk Mahasiswa Informatika*. Modul Kuliah UAI. (Bab 1–13)  
2. Downey, A. B. (2024). *Think Python* (3rd ed.). O'Reilly Media.  
3. Python Software Foundation. (2026). *Python 3.x Documentation*. [https://docs.python.org/3/](https://docs.python.org/3/)

---

*Proyek ini dibuat untuk memenuhi tugas Proyek Akhir Mata Kuliah Algoritma dan Pemrograman,  
Program Studi Informatika, Universitas Al Azhar Indonesia, Semester Genap 2025/2026.*
