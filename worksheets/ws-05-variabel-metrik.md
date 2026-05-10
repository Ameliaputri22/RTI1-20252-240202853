# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question:Apakah TLS 1.3 menghasilkan latensi dan penggunaan memori yang lebih rendah dibandingkan DTLS pada protokol MQTT di perangkat IoT dengan RAM <64KB?

| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
|Jenis protokol|IV|Metode keamanan komunikasi|TLS 1.3 vs DTLS|Nominal|-|Konfigurasi sistem eksperimen|Variabel utama yang dibandingkan|
|Latensi|DV|Kecepatan komunikasi|Waktu pengiriman data|Ratio|ms|Mengukur waktu request-response MQTT|Mewakili performa sistem|
|Penggunaan memori|DV|Efisiensi resource|RAM yang digunakan|Ratio|KB|Monitoring penggunaan memori saat proses|Penting untuk IoT low-resource|
|Ukuran data|CV|Beban komunikasi|Ukuran paket data|Ratio|Byte|Mengontrol ukuran payload|Menghindari bias hasil|

Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  - [☑] Setiap langkah terdokumentasi
  - [☑] Tidak ada "lompatan logis"
  - [☑] Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Apakah TLS 1.3 lebih efisien dibandingkan DTLS dalam hal latensi dan penggunaan memori pada MQTT IoT?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
|Jenis protokol|IV|Metode keamanan|TLS vs DTLS|Nominal|—|
|Latensi|DV|Kecepatan sistem|Waktu kirim data|Ratio|ms|
|Penggunaan memori|DV|Efisiensi resource|RAM usage|Ratio|KB|
|Ukuran data|CV|Beban sistem |Payload size|Ratio|Byte|

**Apakah ada lompatan logis dalam rantai?** Tidak
---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative |5|Latensi & memori langsung merepresentasikan performa IoT|
| Sensitive |4 |Perubahan kecil masih bisa terdeteksi|
| Feasible |5|Mudah diukur dengan tools monitoring|

**Apakah perlu secondary metric?**Ya
> Jika ya, apa dan mengapa? Secondary metric:Throughput (jumlah data per detik)
> alasannya Untuk melengkapi analisis performa selain latensi dan memori

**Contoh kasus ceiling effect untuk metrik ini:**
> Jika semua metode menghasilkan latensi yang hampir sama (misalnya 1–2 ms), maka metrik tidak cukup sensitif untuk membedakan performa.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | Apakah semua data point terkumpul?|Bisa tidak lengkap|Logging otomatis|
| Consistency | Apakah ada kontradiksi?|Bisa terjadi noise|Ulangi eksperimen|
| Validity | Apakah benar-benar mengukur yang dimaksud?|Ya|Gunakan alat ukur valid|
| Representativeness | *Apakah sampel mewakili populasi target?|Terbatas|Gunakan variasi skenario|

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat data dianggap p-hacking karena peneliti bisa secara tidak sadar memilih metrik yang mendukung hasil yang diinginkan, sehingga hasil menjadi bias dan tidak objektif. Hal ini merusak validitas penelitian karena kesimpulan tidak lagi berdasarkan desain awal eksperimen.

Berbeda dengan eksplorasi data yang sah, eksplorasi dilakukan setelah analisis utama dan harus dilaporkan secara transparan sebagai temuan tambahan (exploratory), bukan sebagai bukti utama (confirmatory). Dengan demikian, eksplorasi tetap diperbolehkan selama tidak digunakan untuk memanipulasi hasil utama penelitian.
