# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset           : Hasil eksperimen perbandingan TLS 1.3 dan DTLS pada MQTT IoT
Jumlah data awal  : 10 records (5 run DTLS dan 5 run TLS 1.3)

Cleaning:
| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing | 0|Tidak ada tindakan|Seluruh data berhasil tercatat|
| Duplikat| 0|Tidak ada tindakan|Setiap run memiliki Run ID yang unik|
| Error   |0|Standardisasi format CSV|Semua kolom menggunakan tipe data yang konsisten|

Transformation:
| Transformasi | Variabel | Detail | Alasan |
|-------------|----------|--------|--------|
|Konversi tipe data|Latency, Memory Usage|Dari string menjadi float|Memudahkan analisis statistik|
Standardisasi satuan|Memory Usage|Seluruh nilai menggunakan KB|Menjaga konsistensi data|
Penamaan variabel|Semua kolom|Menggunakan nama kolom yang seragam|Mempermudah proses analisis|

Normalization:
  Metode    :Tidak dilakukan
  Alasan    :Data hanya akan dianalisis menggunakan statistik deskriptif dan Independent t-test, sehingga tidak memerlukan normalisasi. Selain itu, seluruh metrik sudah berada pada satuan yang jelas (ms dan KB), sehingga transformasi tambahan dapat mengurangi interpretabilitas hasil.
  Parameter :Tidak ada

Leakage Check:
  [☑] Parameter normalisasi dari training set saja
  [☑] Tidak ada informasi test set dalam preprocessing
  [☑] Cross-validation dilakukan setelah split

Jumlah data akhir : 10 records
Script tersedia   : ☑ Ya → preprocessing.py
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
|Missing value|0|Tidak ada|Semua data lengkap|
|Data duplikat|0|Tidak ada|Run ID berbeda untuk setiap eksperimen|
|Error format|0|Tidak ada|Format CSV telah sesuai|

**Jumlah data sebelum cleaning:** 10
**Jumlah data setelah cleaning:** 10
**Persentase data yang hilang/berubah:** 0%

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|-----------|-----------|----------|-------------------|--------|
|Latency (ms)|17.8 – 19.3|Hampir normal|Tidak|Tidak perlu|Uji statistik menggunakan data asli agar hasil mudah diinterpretasikan|
|Memory Usage (KB)	28.4 – 31.2|Hampir normal|Tidak|Tidak perlu|Semua data berada pada rentang yang seragam|
|Throughput (KB/s)|56 – 61|Hampir normal|Tidak|Tidak perlu|Tidak digunakan algoritma berbasis jarak|

**Apakah normalisasi diperlukan?** [ ] Ya / [☑] Tidak
**Justifikasi:**
> Normalisasi tidak diperlukan karena analisis menggunakan Independent Samples t-test, yang tidak mensyaratkan data berada pada skala tertentu. Selain itu, seluruh variabel telah memiliki satuan yang konsisten dan tidak menunjukkan perbedaan skala yang ekstrem.

**Leakage check:**
- [☑]Tidak ada parameter normalisasi yang dihitung dari seluruh dataset.
- [☑]Tidak ada proses normalisasi sebelum pemisahan data.
- [☑]Tidak terjadi data leakage.

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY
1. Dataset:
   Hasil eksperimen TLS 1.3 dan DTLS pada protokol MQTT di perangkat IoT.
2. Data awal:
   10 records, 6 features
3. Cleaning:
   - Missing values : 0 kasus, tidak ada tindakan.
   - Duplikat       : 0 kasus, seluruh Run ID unik.
   - Error format   : 0 kasus, format CSV telah konsisten.
4. Transformation:
   - Konversi tipe data numerik ke format float.
   - Standardisasi satuan memori ke KB.
   - Penamaan kolom dibuat seragam.
5. Normalisasi:
   Tidak dilakukan karena analisis menggunakan Independent Samples t-test dan seluruh variabel telah berada pada skala yang konsisten.
6. Data akhir:
   10 records, 6 features
7. Leakage Check:
   ☑ Lulus
   Tidak ditemukan data leakage selama proses preprocessing.
```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

>Pada beberapa tugas sebelumnya, normalisasi sering diterapkan secara otomatis tanpa mempertimbangkan kebutuhan metode analisis yang digunakan. Setelah mempelajari materi ini, dipahami bahwa normalisasi hanya dilakukan jika memang diperlukan oleh algoritma atau metode statistik tertentu.
>Over-preprocessing dapat mengubah karakteristik asli data sehingga hasil analisis menjadi kurang representatif. Selain itu, transformasi yang tidak diperlukan dapat mengurangi interpretabilitas data, memperkenalkan bias, atau bahkan menyebabkan data leakage apabila parameter preprocessing dihitung menggunakan seluruh dataset sebelum pemisahan data. Oleh karena itu, setiap langkah preprocessing harus memiliki alasan yang jelas, terdokumentasi, dan dapat direplikasi.
