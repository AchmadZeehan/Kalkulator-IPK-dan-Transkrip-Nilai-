# AI Usage Log — Proyek Akhir Algoritma dan Pemrograman

**Judul Proyek:** Kalkulator IPK dan Transkrip Nilai  
**Kelas:** IF25H | **Mata Kuliah:** Algoritma dan Pemrograman  
**Dosen:** Tri Aji Nugroho, S.T., M.T. | **Universitas Al Azhar Indonesia — 2026**

| Nama | NIM |
|:-----|:----|
| Achmad Zeehan Wardana | 0102525001 |
| Akrim Shulhi | 0102523009 |
| Habibie Rahman Abdillah | 0102525006 |
| Hanif Zakia Khoirunnisa | 0102524642 |

---

> **Pernyataan Transparansi:**  
> Sesuai dengan panduan Bab 13 (AI-Augmented Programming) dan Bab 14 (Proyek Akhir), seluruh interaksi signifikan dengan AI didokumentasikan dalam tabel berikut. Penggunaan AI tidak menggantikan pemahaman konsep — keputusan akhir arsitektur, validasi logika, dan integrasi kode sepenuhnya menjadi tanggung jawab anggota kelompok.

---

## Tabel AI Usage Log

| No | Tanggal | Fase Pengembangan | AI Tool | Prompt yang Diberikan (Ringkasan) | Output AI (Ringkasan) | Modifikasi / Validasi oleh Mahasiswa | Keputusan Akhir |
|:--:|:--------|:------------------|:--------|:----------------------------------|:----------------------|:-------------------------------------|:----------------|
| 1 | 14 Jun 2026 | Desain & Proposal | Claude | "Bantu saya brainstorm fitur-fitur apa saja yang relevan untuk aplikasi Kalkulator IPK berbasis Python yang mencakup konsep dari Bab 1–13 AlPro." | 10 fitur potensial: input MK, hitung IPK/IPS, tampilkan transkrip, cari MK, urutkan, simulasi target, statistik, hapus/edit, ekspor CSV, data demo | Dipilih 8 fitur utama (FR-1 s.d. FR-8); fitur ekspor CSV dihapus karena melampaui scope; fitur data demo dipertahankan untuk keperluan pengujian | Gunakan 8 fitur + 1 fitur data demo; semua relevan dengan CRUD dan konsep Bab 7–10 |
| 2 | 14 Jun 2026 | Desain Struktur Data | Claude | "Struktur data Python apa yang paling efisien untuk menyimpan riwayat mata kuliah mahasiswa, mendukung sorting, filtering, dan validasi duplikat kode MK?" | Saran: `list of dict` untuk riwayat, `dict` untuk bobot mutu, `set` untuk validasi duplikat; penjelasan kompleksitas O(1) dan O(n) | Divalidasi dengan materi Bab 7–8; dipilih kombinasi `list of dict` + `set` + `dict` konstanta sesuai saran AI; ditambahkan alasan Big-O ke docstring | Implementasi menggunakan `riwayat_mk` (list of dict), `kode_terdaftar` (set), `BOBOT_MUTU` (dict) |
| 3 | 15 Jun 2026 | Implementasi — Fungsi Inti | Claude | "Tulis pseudocode untuk fungsi hitung_ipk() menggunakan rata-rata berbobot SKS di Python, beserta docstring standar." | Pseudocode fungsi hitung_ipk dengan loop akumulasi `total_bobot` dan `total_sks`, docstring lengkap, penanganan edge case total_sks = 0 | Pseudocode dikonversi ke Python nyata; ditambahkan parameter opsional `daftar_mk=None` agar fungsi bisa digunakan oleh `hitung_ips()`; diuji manual dengan kalkulator | Kode diadopsi setelah modifikasi signature dan verifikasi hasil manual |
| 4 | 15 Jun 2026 | Implementasi — Input Validasi | Claude | "Buatkan fungsi `input_valid()` Python yang bisa memvalidasi input tipe str, int, dan float dengan loop retry dan pesan error yang informatif." | Fungsi input_valid dengan while loop, try-except untuk int/float, parameter `boleh_kosong` | Ditambahkan parameter `tipe` ke dalam dispatch; pesan error diubah ke Bahasa Indonesia; diintegrasikan ke seluruh fungsi yang memerlukan input pengguna | Gunakan setelah adaptasi pesan ke Bahasa Indonesia dan uji semua skenario edge case |
| 5 | 15 Jun 2026 | Implementasi — Tampilkan Transkrip | Claude | "Buat tampilan transkrip nilai CLI yang rapi menggunakan box-drawing characters Python, dikelompokkan per semester dengan IPS dan IPK kumulatif per baris." | Template box-drawing dengan karakter `╔`, `═`, `║`, `╚`, contoh output per semester | Lebar kolom disesuaikan dengan panjang data aktual; ditambahkan kolom IPK kumulatif s.d. semester berjalan (`ipk_kumulatif_mk`); ditambahkan bagian predikat kelulusan (Cum Laude, dsb.) | Gunakan setelah penyesuaian lebar dan tambahan fitur predikat |
| 6 | 16 Jun 2026 | Implementasi — Simulasi Target IPK | Claude | "Tulis formula matematika dan kode Python untuk menghitung bobot mutu minimum yang diperlukan semester depan agar IPK mencapai nilai tertentu." | Formula: `mutu_min = (target × (total_sks + sks_rencana) − total_bobot) / sks_rencana`; kode Python lengkap dengan validasi range | Diverifikasi secara manual dengan contoh data (IPK 3.0, SKS 20, target 3.5, rencana 24 SKS); ditambahkan logika terjemahan bobot mutu ke nilai huruf menggunakan iterasi `BOBOT_MUTU`; ditambahkan pesan khusus jika target sudah terlampaui atau tidak mungkin dicapai | Formula benar setelah verifikasi manual; kode diadopsi dengan penambahan tiga cabang kondisi |
| 7 | 16 Jun 2026 | Implementasi — Sorting & Searching | Claude | "Berikan contoh implementasi linear search dan Timsort di Python untuk struktur list of dict, beserta penjelasan kompleksitas Big-O untuk Bab 9 dan 10." | Contoh list comprehension sebagai linear search O(n); penggunaan `sorted()` dengan lambda key function O(n log n); tabel kompleksitas | Diintegrasikan ke fungsi `cari_mk()` dan `urutkan_mk()`; ditambahkan opsi multiple kriteria sorting (7 pilihan); ditambahkan komentar referensi bab (`[Bab 9]`, `[Bab 10]`, `[Bab 12]`) agar sesuai panduan proyek | Gunakan setelah perluasan kriteria sorting dari 3 menjadi 7 opsi |
| 8 | 17 Jun 2026 | Implementasi — Statistik Akademik | Claude | "Bantu saya membuat fungsi statistik akademik yang menampilkan distribusi nilai huruf dengan bar chart ASCII, mata kuliah tertinggi/terendah, dan persentase nilai A." | Fungsi dengan dict counter untuk distribusi, `max()`/`min()` dengan lambda, bar `█` proportional | Ditambahkan tampilan IPS per semester dalam ringkasan; bar chart dibuat non-proportional (1 karakter = 1 MK) agar terbaca di semua ukuran terminal; ditambahkan persentase nilai A/A- sebagai indikator prestasi | Gunakan setelah penyesuaian skala bar chart dan penambahan ringkasan IPS |
| 9 | 17 Jun 2026 | Implementasi — Fungsi Hapus/Edit | Claude | "Tulis fungsi CRUD (delete dan update) untuk list of dict Python dengan konfirmasi sebelum eksekusi dan sinkronisasi ke set kode_terdaftar." | Fungsi hapus menggunakan `list.pop(index)` + `set.discard()`; fungsi edit langsung update dict pada indeks | Ditambahkan sub-menu untuk memilih antara hapus atau edit nilai; pesan konfirmasi dibuat lebih deskriptif (menampilkan nama MK); IPK langsung ditampilkan ulang setelah edit untuk feedback real-time | Gunakan setelah penambahan sub-menu dan feedback IPK real-time |
| 10 | 18 Jun 2026 | Implementasi — Dispatch Table & main() | Claude | "Jelaskan pola dispatch table menggunakan dictionary di Python sebagai alternatif if-elif panjang untuk menu program." | Penjelasan dispatch table: `dict` dengan key pilihan menu dan value fungsi; contoh implementasi `menu_aksi[pilihan]()`; perbandingan Big-O O(1) vs O(n) if-elif | Dipahami konsepnya (sesuai materi Bab 8); diterapkan di fungsi `main()` sebagai `menu_aksi`; ditambahkan komentar `# O(1) — dict lookup [Bab 8]` untuk dokumentasi; diperkaya dengan header dan sapaan awal | Gunakan setelah pemahaman konsep dan penambahan komentar anotasi bab referensi |
| 11 | 18 Jun 2026 | Dokumentasi — Docstring | Claude | "Review dan lengkapi docstring semua fungsi di file notebook ini dengan format standar Python (Parameters, Returns, Raises) dan tambahkan keterangan kompleksitas Big-O." | Docstring lengkap untuk 13 fungsi dalam format konsisten: deskripsi, Parameters, Returns, dan catatan kompleksitas | Setiap docstring dibaca dan diverifikasi kesesuaiannya dengan implementasi aktual; beberapa parameter description diperbaiki (misal: `daftar_mk` di `hitung_ipk`); kalimat dalam Bahasa Indonesia disesuaikan | Gunakan setelah verifikasi per-fungsi; total 13 docstring diperbarui |
| 12 | 19 Jun 2026 | Data Demo & Testing | Claude | "Buatkan 10 entri data demo mata kuliah mahasiswa Informatika UAI yang realistis untuk 2 semester, mencakup variasi nilai huruf dari A hingga B-." | 10 entri data demo dengan kode, nama, SKS, nilai, dan semester yang beragam | Nama mata kuliah disesuaikan dengan kurikulum Informatika UAI yang sebenarnya (Algoritma dan Pemrograman, Matematika Diskrit, dll.); IPK hasil data demo diverifikasi manual = 3.43 | Gunakan 10 entri setelah penyesuaian nama MK dengan kurikulum aktual UAI |
| 13 | 19 Jun 2026 | Debugging | Claude | "Program saya menampilkan box-drawing yang misaligned di terminal Colab karena lebar karakter berbeda. Bagaimana cara memperbaikinya?" | Penjelasan bahwa Google Colab menggunakan monospace font terbatas; saran: gunakan karakter ASCII standar `=` dan `-` sebagai fallback, atau sesuaikan lebar box secara manual | Setelah pengujian, karakter `╔═╗╚╝║` terbaca baik di Colab; solusi AI tidak diterapkan karena masalah tidak reproduksi; box-drawing tetap dipertahankan untuk estetika | Pertahankan box-drawing; masalah bersifat environment-specific dan tidak terjadi di Colab standar |
| 14 | 27 Jun 2026 | Dokumentasi & Validasi Proyek | DeepSeek (via chat) | "Analisis kode dan proposal kami terhadap ketentuan Bab 14 – berikan checklist kelengkapan, identifikasi kekurangan, dan saran perbaikan untuk memaksimalkan nilai." | AI memberikan analisis komprehensif mencakup: (1) kesesuaian jumlah fungsi (≥7), struktur data (≥2 jenis), penggunaan searching/sorting; (2) checklist pre-submission (18 item) dengan status terpenuhi/belum; (3) rekomendasi penambahan AI Usage Log, README, sketsa UI, dan perbaikan timeline; (4) peringatan inkonsistensi antara fitur (FR-4) dan proposal; (5) saran tambahan fitur file I/O sebagai nilai tambah. | Kami menggunakan checklist untuk memverifikasi seluruh aspek proyek. Saran untuk menambahkan **sketsa UI** (Bagian 8.2) dan **README.md** diadopsi sepenuhnya. **AI Usage Log** ini dibuat berdasarkan template yang diberikan. **FR-4** diperbaiki agar konsisten dengan fitur (menambahkan "nilai huruf"). **Timeline** disesuaikan dari minggu 9–15. Saran file I/O tidak diimplementasikan karena dianggap opsional dan keterbatasan waktu. | Checklist diadopsi sebagai alat verifikasi final. Seluruh saran perbaikan dokumen (UI, README, AI Log, FR-4, timeline) diterapkan. Saran fitur tambahan (file I/O) ditolak karena di luar scope proyek dan batas waktu pengerjaan. |
---

## Ringkasan Penggunaan AI

| Metrik | Nilai |
|:-------|:------|
| Total Interaksi AI yang Didokumentasikan | 13 |
| AI Tool yang Digunakan | Claude (Anthropic) |
| Fase dengan Intensitas AI Tertinggi | Implementasi (8 dari 13 interaksi) |
| Interaksi Diadopsi Penuh | 0 (selalu ada modifikasi) |
| Interaksi Diadopsi dengan Modifikasi | 12 |
| Interaksi Tidak Diterapkan | 1 (No. 13 — debugging box-drawing) |
| Estimasi Kontribusi Kode AI | ~35–40% (boilerplate & template) |
| Estimasi Kontribusi Kode Mandiri | ~60–65% (logika inti, validasi, integrasi) |

---

## Refleksi Kritis

**Apa yang AI bantu dengan baik:**  
AI sangat membantu dalam menghasilkan *boilerplate* kode (template fungsi, docstring awal, contoh penggunaan `sorted()`) dan menjelaskan konsep Big-O secara konkret. Ini mempercepat fase implementasi awal secara signifikan.

**Apa yang AI tidak bisa gantikan:**  
Keputusan arsitektur (memilih 8 fitur dari 10 saran AI), validasi manual hasil perhitungan IPK, penyesuaian dengan kurikulum nyata UAI, dan integrasi antar-fungsi (misalnya, agar `hitung_ips()` memanfaatkan `hitung_ipk()`) sepenuhnya dilakukan oleh anggota kelompok.

**Pelajaran utama:**  
Output AI selalu harus divalidasi — terutama untuk logika yang melibatkan perhitungan matematis. Formula simulasi target IPK diverifikasi manual sebelum diadopsi, dan terbukti output AI benar. Ini mengajarkan bahwa AI adalah *sparring partner* yang mempercepat eksplorasi, bukan pengganti pemahaman.

---

*Dokumen ini dibuat sesuai panduan Bab 14 — Proyek Akhir, Mata Kuliah Algoritma dan Pemrograman, Universitas Al Azhar Indonesia, 2026.*
