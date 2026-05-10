# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question :Apakah TLS 1.3 menghasilkan latensi dan penggunaan memori yang lebih rendah dibandingkan DTLS pada protokol MQTT di perangkat IoT dengan RAM <64KB?
Hypothesis        :
H₀ : Tidak ada perbedaan signifikan antara TLS 1.3 dan DTLS terhadap latensi dan penggunaan memori
H₁ : Ada perbedaan signifikan antara TLS 1.3 dan DTLS terhadap latensi dan penggunaan memori
Tipe Eksperimen
Tipe Eksperimen   : [☑] Comparison
Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control |Baseline menggunakan DTLS|DTLS|Dataset sama, payload sama, seed 42|
| Treatment |Pengujian menggunakan TLS 1.3|TLS 1.3|Dataset sama, payload sama, seed 42|

Fairness Checklist:
  [☑] Dataset identik untuk semua kondisi
  [☑] Preprocessing setara
  [☑] Tuning effort setara
  [☑] Environment identik
  [☑] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    |Perbedaan kondisi jaringan|Gunakan jaringan dan konfigurasi yang sama|
| External    |Dataset hanya simulasi|Tambahkan skenario real IoT|
| Construct   |Latensi tidak sepenuhnya merepresentasikan performa|Tambahkan throughput sebagai secondary metric|
| Conclusion  |Jumlah sampel eksperimen terlalu kecil|Lakukan pengulangan eksperimen beberapa kali|

Statistical Plan:
  Uji statistik   :Independent t-test
  Justifikasi      :Membandingkan rata-rata dua kelompok independen
  Alpha            :0.005
  Effect size min  :0.2
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Apakah TLS 1.3 lebih efisien dibandingkan DTLS pada MQTT IoT?
**Tipe eksperimen:** [☑] Comparison
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control |DTLS sebagai baseline|DTLS|Payload 512B, dataset sama, seed 42|
| Treatment |TLS 1.3 sebagai metode pembanding|TLS 1.3|Payload 512B, dataset sama, seed 42|

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik |✅|Menggunakan dataset yang sama|
| Preprocessing setara|✅|Data diproses dengan metode yang sama|
| Tuning effort setara|✅|Konfigurasi diuji dengan effort seimbang|
| Environment identik |✅|Hardware dan jaringan sama|
| Metrik evaluasi sama |✅|Sama-sama memakai latensi & memori|

**Ada yang tidak fair?**☑ Tidak

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal |Perbedaan traffic jaringan|Gunakan traffic generator yang sama|
| External |Hanya diuji pada satu jenis perangkat IoT|Tambahkan beberapa perangkat berbeda|
| Construct |Latensi belum cukup menggambarkan kualitas|Tambahkan throughput|
| Conclusion |Variasi hasil antar percobaan|Lakukan eksperimen berulang|

**Ancaman mana yang paling sulit dimitigasi?** External validity
**Mengapa?**
> Karena hasil eksperimen pada satu jenis perangkat atau lingkungan belum tentu dapat digeneralisasikan ke semua kondisi IoT di dunia nyata.

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah semua metode diuji menggunakan dataset dan kondisi yang sama?
2. Apakah baseline yang digunakan merupakan metode yang relevan dan representatif?
3. Apakah perbedaan hasil tersebut signifikan secara statistik dan bukan karena bias eksperimen?
