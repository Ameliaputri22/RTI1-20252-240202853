# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  :Belum ada penelitian yang secara langsung membandingkan performa TLS 1.3 dan DTLS pada protokol MQTT di perangkat IoT dengan keterbatasan resource, khususnya dari segi latensi dan penggunaan memori.

Research Question:
  Tipe         :  Comparison
  Formulasi    : Apakah TLS 1.3 menghasilkan performa yang lebih baik dibandingkan DTLS dalam hal latensi dan penggunaan memori pada protokol MQTT di perangkat IoT dengan RAM <64KB?
  Variabel IV  : Jenis protokol keamanan (TLS 1.3 vs DTLS)
  Variabel DV  : Latensi dan penggunaan memori
  Metrik       : Latensi (ms), penggunaan memori (KB)
  Dataset      : Data trafik komunikasi IoT (simulasi atau real IoT dataset)
  Baseline     : DTLS (dibandingkan dengan TLS 1.3)

Quality Check RQ:
  [ ] Variabel spesifik
  [ ] Metrik jelas
  [ ] Baseline ada
  [ ] Konteks disebutkan
  [ ] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui :Perbandingan empiris antara TLS 1.3 dan DTLS dalam konteks MQTT pada perangkat IoT dengan resource terbatas
  Jenis kontribusi        :  Comparison
  Gap yang diisi          : Method gap dan performance gap terkait pemilihan protokol keamanan IoT

Hypothesis Pair:
  H₀ : Tidak terdapat perbedaan signifikan dalam latensi dan penggunaan memori antara TLS 1.3 dan DTLS pada MQTT di perangkat IoT.
  H₁ : Terdapat perbedaan signifikan dalam latensi dan penggunaan memori antara TLS 1.3 dan DTLS pada MQTT di perangkat IoT.
  Threshold              : p-value < 0.05
  Justifikasi threshold  : Nilai 0.05 merupakan standar umum dalam penelitian untuk menentukan signifikansi statistik
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:**Belum ada perbandingan langsung TLS vs DTLS pada MQTT untuk perangkat IoT low-resource

**RQ versi pertama (tulis bebas):**
> Bagaimana perbandingan TLS dan DTLS pada IoT?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik |Ya|TLS vs DTLS|
| Metrik terukur |Tidak |belum ada|
| Baseline |Tidak |belum jelas|
| Dataset/konteks |Tidak |belum disebut|

**Tipe RQ:** Comparison

**RQ versi revisi (setelah evaluasi):**
> Apakah TLS 1.3 menghasilkan latensi dan penggunaan memori yang lebih rendah dibandingkan DTLS pada protokol MQTT di perangkat IoT dengan RAM <64KB?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ |Tidak ada perbedaan signifikan latensi dan penggunaan memori antara TLS 1.3 dan DTLS|
| H₁ |Ada perbedaan signifikan latensi dan penggunaan memori antara TLS 1.3 dan DTLS|
| Metrik |Latensi (ms), memori (KB)|
| Threshold |p < 0.05|
| Justifikasi threshold |Standar umum penelitian statistik|

**Apakah hipotesis ini falsifiable?** Ya
> Bagaimana cara membuktikannya salah?Dengan melakukan eksperimen dan menunjukkan bahwa hasil uji statistik tidak signifikan (p ≥ 0.05), sehingga H₀ tidak dapat ditolak.

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ |Apakah TLS 1.3 lebih efisien dibandingkan DTLS pada MQTT IoT?|
| Variable (IV) |Jenis protokol (TLS vs DTLS)|
| Variable (DV) |Latensi, penggunaan memori|
| Metric |ms (latensi), KB (memori)|
| Data source |Trafik IoT (simulasi / real dataset)|
| Analysis method |Uji statistik (t-test atau Mann-Whitney)|

**Apakah rantai lengkap?** Ya


---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:**Analisis Performa Protokol Keamanan pada IoT
**RQ yang diekstrak:** Apakah metode keamanan tertentu meningkatkan performa sistem IoT?
**Komponen yang hilang:** -Tidak menyebutkan metode spesifik
                          -Tidak ada metrik yang jelas
                          -Tidak ada dataset
                          -Tidak ada baseline
