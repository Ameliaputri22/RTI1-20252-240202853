# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST
Completeness
☑ Semua skenario tercakup
☑ Jumlah run sesuai rencana
☑ Tidak ada file output hilang
Missing: 0 dari 10 data

Format Consistency
☑ Semua file menggunakan format CSV
☑ Header konsisten
☑ Seluruh kolom numerik bertipe numerik
Range & Logic
☑ Latency > 0 ms
☑ Tidak ada waktu negatif
☑ Memory Usage berada dalam batas kapasitas ESP8266 (<64 KB)
☑ CPU Usage dan Packet Loss berada pada rentang yang valid
Anomali ditemukan:
1 nilai latensi tinggi pada Run 4 (27.9 ms), diduga dipengaruhi kondisi jaringan sementara.
Cross Validation
☑ Run dengan parameter identik menghasilkan nilai yang relatif serupa.
☑ Hasil sesuai dengan teori bahwa TLS 1.3 dan DTLS memiliki karakteristik performa yang berbeda pada perangkat IoT.

Keputusan
☑ Data siap dianalisis
☐ Perlu cleaning
☐ Perlu re-run

```

---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
|TLS (Control)	|5	|5	|0|	—|
|TLS 1.3 (Treatment)	|5	|5	|0	|—|

**Total expected:** 10 run | **Total actual:** 10 run| **Missing:** 10 run

**Keputusan untuk data missing:**
> Tidak terdapat data yang hilang. Seluruh skenario dan jumlah run telah sesuai dengan execution plan sehingga tidak diperlukan pengulangan eksperimen karena kehilangan data.
---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (atau data Anda sendiri):**

| Run | Accuracy (%) |
|-----|-------------|
|1    |18.5|
|2	  |18.7|
|3	  |18.6|
|4	  |27.9|
|5	  |18.4|

**Deteksi outlier:**
Data terurut:
18.4, 18.5, 18.6, 18.7, 27.9
Q1 = 18.5
Q3 = 18.7
IQR = 0.2
Batas bawah
18.5 − (1.5 × 0.2) = 18.2
Batas atas
18.7 + (1.5 × 0.2) = 19.0
Outlier terdeteksi
Run 4 (27.9 ms)

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| *Run 4* |27.9 ms|Gangguan jaringan atau proses handshake ulang sehingga latensi meningkat|Tidak langsung dihapus. Dilakukan investigasi terhadap log jaringan dan pengulangan (re-run) menggunakan seed yang sama.|

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:**100% data berhasil dikumpulkan (10 dari 10 run)% data terkumpul
**2. Format:** [☑] Konsiste. Seluruh data disimpan dalam format CSV dengan struktur kolom yang sama pada setiap run.
**3. Range check (anomali):** Seluruh nilai masih berada dalam rentang yang logis.
Contoh:
-Latency > 0 ms
-Memory Usage < 64 KB
-CPU Utilization 0–100%
-Packet Loss 0–100%
Ditemukan 1 nilai latensi yang tergolong outlier, namun masih valid secara teknis sehingga perlu investigasi, bukan langsung dihapus.
**4. Logic check:** [☑ ] Parameter sesuai plan 
Semua eksperimen menggunakan:
-Payload 512 Byte
-MQTT QoS 1
-Hardware ESP8266
-Seed sesuai rencana
-Skenario DTLS dan TLS 1.3 tidak tercampur

**Kesimpulan:** [☑ ] Data siap analisis 
Dataset telah memenuhi aspek completeness, consistency, accuracy, dan validity. Meskipun ditemukan satu nilai outlier pada metrik latensi, hasil tersebut telah didokumentasikan dan akan dipertimbangkan dalam analisis statistik tanpa dihapus secara langsung.

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> Data yang benar (correct data) adalah data yang tampak sesuai atau tidak mengandung kesalahan yang terlihat. Namun, data yang dipercaya (trusted data) adalah data yang telah melalui proses validasi sehingga terbukti lengkap, konsisten, berada dalam rentang yang masuk akal, dan sesuai dengan desain eksperimen.
> Karena proses pencatatan otomatis tidak menjamin data bebas dari kesalahan. Bug pada sistem logging, konfigurasi yang keliru, kehilangan data, atau kondisi lingkungan yang tidak terkontrol dapat menghasilkan data yang menyesatkan. Oleh sebab itu, validasi formal diperlukan untuk memastikan bahwa data yang digunakan dalam analisis statistik benar-benar berkualitas dan dapat dipertanggungjawabkan secara ilmiah.
