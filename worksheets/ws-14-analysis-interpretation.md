# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

```
ANALYSIS & INTERPRETATION

1. Statistik Deskriptif:
   | Skenario | Mean | Std | Median | Min | Max | n |
   |----------|------|-----|--------|-----|-----|---|
|TLS 1.3|17.8|0.9|17.7|16.9|19.1|5|
|DTLS|19.3|1.2|19.2|18.0|21.0|5|
2. Uji Hipotesis:
   Uji yang digunakan  : Independent Samples t-test
   Justifikasi          :Penelitian membandingkan dua kelompok independen (TLS 1.3 dan DTLS). Data diasumsikan berdistribusi normal dan setiap kelompok berasal dari run yang terpisah.
   p-value = 0.031
   Cohen's d = 1.12
   95% Confidence Interval = [-2.80, -0.20] ms (selisih rata-rata latensi)

3. Keputusan
  ☑ H₀ ditolak → H₁ diterima
   Karena p < 0,05, terdapat perbedaan yang signifikan antara TLS 1.3 dan DTLS         terhadap latensi komunikasi pada eksperimen ini.

4. Interpretasi:
   Hubungan ke RQ:
Hasil menunjukkan bahwa TLS 1.3 menghasilkan rata-rata latensi yang lebih rendah dibandingkan DTLS pada perangkat IoT yang diuji. Dengan demikian, hipotesis penelitian didukung berdasarkan data eksperimen.
   Practical significance:
Nilai Cohen's d = 1.12 menunjukkan large effect, sehingga perbedaan tersebut bukan hanya signifikan secara statistik tetapi juga cukup besar untuk dianggap bermakna dalam praktik.
   Perbandingan literatur:
Hasil penelitian ini sejalan dengan beberapa studi yang melaporkan bahwa optimasi pada TLS 1.3 mampu mengurangi overhead komunikasi dibandingkan protokol keamanan sebelumnya. Namun, generalisasi hasil masih perlu diuji pada perangkat IoT dan kondisi jaringan yang lebih beragam.

5. Limitation:
   | Jenis | Ancaman | Dampak | Mitigasi |
   |-------|---------|--------|----------|
   |Internal validity|Variasi kondisi jaringan|Latensi dapat berubah antar-pengujian|	Gunakan jaringan yang sama dan lakukan beberapa kali pengulangan|
   |External validity|Hanya menggunakan ESP8266|Hasil belum tentu berlaku pada perangkat IoT lain|Tambahkan pengujian pada beberapa jenis perangkat|
   |Construct validity|Hanya mengukur latensi dan memori|Performa belum tergambar secara menyeluruh|Tambahkan throughput, packet loss, dan CPU utilization|
   |Statistical limitation|Jumlah sampel hanya 5 run per skenario|Kekuatan uji statistik relatif terbatas|Tingkatkan jumlah run pada penelitian berikutnya|

6. Failure Analysis (jika H₀ tidak ditolak):
   Penyebab potensial  : Tidak ditemukan kegagalan karena H₀ ditolak. Namun, pada kondisi jaringan yang tidak stabil atau perangkat dengan spesifikasi berbeda, performa TLS 1.3 dapat berubah.
   Boundary condition   : Hasil penelitian berlaku pada perangkat IoT dengan RAM <64 KB, komunikasi MQTT, ukuran payload tetap, dan konfigurasi jaringan yang terkontrol.
   Insight              : Efektivitas TLS 1.3 dipengaruhi oleh karakteristik perangkat dan lingkungan jaringan. Oleh karena itu, diperlukan evaluasi lebih lanjut pada berbagai platform IoT dan kondisi jaringan nyata untuk mengetahui batas penerapan (boundary conditions) protokol tersebut.
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|-----------|---------|
|Berapa grup yang dibandingkan?|2 grup (TLS 1.3 dan DTLS)|
|Apakah data berpasangan (paired)?|Tidak|
|Apakah distribusi normal?|Diasumsikan normal berdasarkan uji normalitas|
|Uji yang dipilih|Independent Samples t-test|
|Justifikasi|Membandingkan rata-rata dua kelompok independen dengan data yang memenuhi asumsi normalitas|
**Effect size yang akan dilaporkan:** [☑] Cohen's d 

---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

**Data:**
| Model | Accuracy (mean ± std) | n |
|-------|----------------------|---|
| A | 89.2 ± 1.5 | 10 |
| B | 87.8 ± 2.1 | 10 |

p = 0.045, Cohen's d = 0.74, CI 95% = [0.03, 2.77]

| Aspek | Interpretasi |
|-------|-------------|
|Signifikansi statistik|Nilai p = 0,045 lebih kecil dari α = 0,05 sehingga terdapat perbedaan yang signifikan secara statistik.|
|Effect size|Cohen's d = 0,74 menunjukkan ukuran efek sedang hingga besar, sehingga perbedaannya cukup bermakna.|
|Practical significance|Peningkatan performa sekitar 1,4% dapat memberikan manfaat nyata apabila diterapkan pada sistem yang membutuhkan akurasi tinggi.|
|Hubungan ke RQ|Hasil mendukung hipotesis bahwa Model A memiliki performa lebih baik daripada Model B.|
|Perbandingan literatur|Temuan ini konsisten dengan penelitian sebelumnya yang menunjukkan bahwa pendekatan serupa mampu meningkatkan akurasi dibandingkan metode pembanding.|
---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** Metode baru Anda mendapat F1 = 83.2%, baseline = 84.7%. p = 0.12 (tidak signifikan).

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah ini "gagal"? |Tidak. Hipotesis tidak didukung tetap merupakan hasil penelitian yang valid.|
| Kemungkinan penyebab? |Jumlah sampel terlalu sedikit, kondisi jaringan relatif stabil sehingga perbedaan kedua protokol menjadi sangat kecil, atau perangkat ESP8266 memiliki keterbatasan yang membuat performa keduanya hampir sama.|
| Boundary condition? |TLS 1.3 mungkin hanya menunjukkan keunggulan yang jelas pada ukuran payload lebih besar atau pada kondisi jaringan yang lebih kompleks.|
| Insight yang bisa diambil?|Pada perangkat dengan sumber daya terbatas dan trafik ringan, TLS 1.3 belum memberikan peningkatan performa yang signifikan dibandingkan DTLS.|
| Apakah layak dilaporkan? Mengapa? |Ya. Hasil negatif tetap penting karena membantu menunjukkan batas penerapan metode dan mencegah peneliti lain mengulang eksperimen yang sama tanpa informasi tambahan.|

**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
|Statistical|Hanya 5 run per skenario|Power uji statistik relatif rendah|
|External|Pengujian hanya pada ESP8266|Hasil sulit digeneralisasikan ke perangkat IoT lain|
|Construct|Metrik hanya latensi dan memori|Belum menggambarkan performa sistem secara menyeluruh|

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Dalam penelitian, failure tidak selalu berarti kegagalan. Hasil yang tidak mendukung hipotesis tetap memiliki nilai ilmiah karena dapat menunjukkan batasan suatu metode (boundary condition), mengidentifikasi faktor-faktor yang memengaruhi performa, dan menjadi dasar bagi penelitian lanjutan.

Melalui failure analysis, hasil negatif tidak dipandang sebagai sesuatu yang harus disembunyikan, tetapi sebagai sumber pengetahuan baru. Analisis terhadap penyebab kegagalan, keterbatasan eksperimen, dan kondisi ketika suatu metode tidak bekerja justru dapat memberikan kontribusi yang lebih mendalam serta meningkatkan kualitas dan transparansi penelitian.
