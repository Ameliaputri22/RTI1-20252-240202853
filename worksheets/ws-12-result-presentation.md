# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question : Apakah TLS 1.3 menghasilkan latensi komunikasi dan penggunaan memori yang lebih rendah dibandingkan DTLS pada protokol MQTT di perangkat IoT dengan RAM kurang dari 64 KB?
Metrik Utama      :
-Latency (ms)
-Memory Usage (KB)

Tabel Hasil:
| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
|          |                      |                      |   |

Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama | Metrik |
|---|-------------|-------------|--------|
|1	|Bar chart + error bar|Membandingkan rata-rata latensi TLS 1.3 dan DTLS|Mean latency ± std|
|2	|Box plot|Menunjukkan distribusi penggunaan memori pada setiap skenario|Seluruh data memory usage|
|3	|Scatter plot|Melihat hubungan antara latensi dan penggunaan memori|Latency vs Memory Usage|

Bias Check:
  [☑] Y-axis mulai dari 0 (atau dijustifikasi)
  [☑] Error bar/CI ditampilkan
  [☑] Semua data disertakan (tidak cherry-picked)
  [☑] Tidak menggunakan 3D tanpa alasan
```

---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Skenario | Metrik 1 (mean ± std) | Metrik 2 (mean ± std) | n |
|----------|----------------------|----------------------|---|
|TLS 1.3	 |17.8 ± 0.9	          |28.4 ± 1.1            |	5|
|DTLS	     |19.3 ± 1.2	          |31.2 ± 1.4            |	5|

**Checklist tabel:**
- [☑] Self-contained (judul jelas, satuan ada, N tercantum)
- [☑] Mean ± std (bukan single number)
- [☑] Diurutkan berdasarkan metrik utama
- [☑] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan | Data yang Digunakan |
|---|-------------|-------|---------------------|
| 1 | *Contoh: Bar chart + error bar* |Membandingkan rata-rata latensi TLS 1.3 dan DTLS|Mean latency ± std|
| 2 | *Box plot* |Menampilkan sebaran penggunaan memori pada masing-masing skenario| Seluruh data memory usage|
| 3 | *Scatter plot* |Menunjukkan hubungan antara latensi dan penggunaan memori | Data tiap run (latency vs memory usage)|

---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah Y-axis menyesatkan? |Ya. Perbedaan terlihat jauh lebih besar daripada kondisi sebenarnya karena sumbu Y tidak dimulai dari nol.|
| Apakah error bar ditampilkan? |Belum. Error bar perlu ditambahkan agar variasi data terlihat.|
| Apakah semua kondisi ditampilkan? |Ya. Kedua skenario (TLS 1.3 dan DTLS) ditampilkan.|
| Apa solusinya? |Gunakan sumbu Y yang dimulai dari nol atau berikan justifikasi jika menggunakan rentang terbatas, serta tampilkan error bar pada setiap batang.|

**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [☑] Semua bias check lulus
- [ ] Ada yang perlu diperbaiki: ____

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Tabel dan grafik memiliki fungsi yang saling melengkapi. Tabel menyajikan nilai secara presisi sehingga memudahkan pembaca mengetahui angka rata-rata, standar deviasi, dan jumlah sampel. Sementara itu, grafik memudahkan pembaca melihat pola, tren, perbandingan, dan distribusi data dengan cepat. Oleh karena itu, keduanya diperlukan agar hasil penelitian dapat dipahami secara lengkap.
> Dalam beberapa tugas sebelumnya, grafik batang dibuat tanpa menampilkan error bar dan menggunakan rentang sumbu Y yang terlalu sempit sehingga perbedaan antar-metode terlihat lebih besar daripada kondisi sebenarnya. Dari materi ini dipahami bahwa visualisasi harus dibuat secara objektif, menggunakan skala yang konsisten, menampilkan seluruh data, dan menyertakan ukuran variasi seperti standar deviasi agar tidak menimbulkan interpretasi yang keliru.
