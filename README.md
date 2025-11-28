# # 📘 ADS_10_RC – Analisis Data Statistik (Tugas Kelompok 2)

## Daftar Isi
- [Struktur Repository](#struktur-repository)
- [Cara Menjalankan Script](#cara-menjalankan-script)
- [Paket R yang Digunakan](#paket-r-yang-digunakan)
- [Penjelasan Dataset](#penjelasan-dataset)
- [Metode Analisis](#metode-analisis)
- [Output yang Dihasilkan](#output-yang-dihasilkan)

---

## 📁 Struktur Repository

```
ADS_10_RC/
├── README.md                 # Dokumentasi proyek
├── codeR_10_RC.Rmd            # Script R Markdown untuk analisis ANOVA
├── data_10_RC.xlsx            # Data jam belajar mahasiswa per kategori keterlibatan
├── Output_10_RC.pdf           # Folder untuk output analisis
├── poster_ads_10.pdf          # Poster penelitian
```

## Cara Menjalankan Script

### Prasyarat
- **RStudio** sudah terinstal
- **R** versi 3.6 atau lebih baru

### Langkah-langkah

1. **Buka file** `codeR_10_RC.Rmd` menggunakan RStudio

2. **Instal paket yang dibutuhkan** (jika belum terinstal):
   ```r
   install.packages(c("readxl", "dplyr", "tidyr"))
   ```

3. **Pastikan dataset tersedia** di folder `data/dataset.xlsx`

4. **Jalankan analisis** dengan mengklik tombol **Knit** di bagian atas RStudio
   - Pilih format output (HTML, PDF, atau Word)

5. **Output akan dihasilkan** dalam bentuk:
   - Laporan HTML/PDF/Word
   - File teks hasil analisis di folder `output/`
   - Visualisasi grafik

---

## Paket R yang Digunakan

| Paket | Fungsi |
|-------|--------|
| **readxl** | Membaca file Excel (.xlsx) yang berisi data penelitian |
| **dplyr** | Pembersihan data, seleksi kolom, manipulasi data, dan filtering |
| **tidyr** | Mengubah data dari format wide ke long (pivoting) sebelum analisis ANOVA |
| **ggplot2** | Untuk memvisualisasikan data |

---

## Penjelasan Dataset

### Deskripsi Umum
Dataset berisi **nilai akhir mata kuliah Algoritma dan Struktur Data (ADS)** dari tiga kelas berbeda, yaitu **RA**, **RB**, dan **RC**. Data ini berasal dari file Excel dengan format **wide**, di mana setiap kolom mewakili satu kelas. Dataset kemudian dianalisis menggunakan **ANOVA One-Way** untuk mengetahui apakah terdapat perbedaan nilai rata-rata antar kelas


### Variabel Utama

| Variabel | Penjelasan |
|----------|-----------|
| **kelas** | Kategori kelas mahasiswa yang dianalisis. Terdiri dari tiga kelompok:<br>• **RA**<br>• **RB**<br>• **RC** |
| **nilai** | Nilai akhir mata kuliah ADS dari masing-masing mahasiswa yang berasal dari tiap kelas. Variabel ini digunakan sebagai **respon ANOVA One-Way** untuk melihat apakah terdapat perbedaan rata-rata nilai antar kelas. |

### Transformasi Data
- Data awal berformat **wide**, di mana setiap kolom mewakili satu kelas (**RA**, **RB**, **RC**).
- Data kemudian diubah ke format **long** secara manual dengan menggabungkan seluruh nilai ke satu kolom `nilai`, dan membuat kolom `kelas` menggunakan fungsi `rep()` untuk memberi label setiap nilai.
- Format long ini memudahkan analisis statistik seperti:
  - uji normalitas per kelas
  - uji homogenitas varians (Levene dan Bartlett)
  - ANOVA One-Way
  - visualisasi (boxplot, density plot, mean ± SD)

---

## Metode Analisis

Penelitian ini menggunakan **ANOVA One-Way** untuk menguji apakah terdapat perbedaan nilai akhir mahasiswa antar kelas (RA, RB, RC).

Hipotesis yang diuji adalah:

- **H₀ (Hipotesis Nol)**: Rata-rata nilai akhir **sama** untuk semua kelas (RA = RB = RC).
- **H₁ (Hipotesis Alternatif)**: Minimal ada **satu kelas** yang memiliki rata-rata nilai akhir **berbeda** dari yang lain.

Sebelum melakukan ANOVA, script juga menjalankan beberapa pengujian asumsi, yaitu:
1. **Uji Normalitas** (Shapiro-Wilk) untuk setiap kelas dan residual model.
2. **Uji Homogenitas Varians** menggunakan:
   - **Levene Test** (disarankan)
   - **Bartlett Test** (sensitif terhadap non-normalitas)

Jika asumsi terpenuhi, maka hasil ANOVA valid untuk digunakan dalam penarikan kesimpulan.

---

## Output yang Dihasilkan

1. **Statistik Deskriptif**
   - Rata-rata (Mean), Standar Deviasi (SD), dan jumlah sampel (N) untuk setiap kelas (RA, RB, RC).
   - Output dihitung menggunakan `dplyr::summarise()`.

2. **Hasil Uji Normalitas**
   - Uji Shapiro-Wilk untuk setiap kelas: RA, RB, dan RC.
   - Uji normalitas residual model ANOVA.

3. **Hasil Uji Homogenitas Varians**
   - **Levene Test** dari paket `car` (disarankan).
   - **Bartlett Test** untuk perbandingan.

4. **Tabel ANOVA One-Way**
   - Menampilkan nilai F-statistic, p-value, dan analisis signifikansi perbedaan rata-rata antar kelas.

5. **Post Hoc Tukey (Opsional)**
   - Jika ANOVA signifikan, TukeyHSD digunakan untuk melihat pasangan kelas mana yang berbeda signifikan.

6. **Visualisasi Grafik**
   - **Boxplot** nilai akhir per kelas.
   - **Plot Rata-Rata + SD** per kelas.
   - **Density Plot** distribusi nilai untuk RA, RB, dan RC.
   - **QQ Plot Residual** untuk mengevaluasi asumsi normalitas residual ANOVA.

7. **Interpretasi Hasil**
   - Kesimpulan apakah terdapat perbedaan nilai akhir antar kelas.
   - Penjelasan berdasarkan p-value ANOVA dan (jika signifikan) hasil Tukey.
   - Untuk memvisualisasikan data sebenarnya cukup menggunakan Plot Rata-Rata dan Density Plot
