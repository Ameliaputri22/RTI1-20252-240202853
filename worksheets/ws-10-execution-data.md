# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1     |DTLS (Control)|42|Payload=512B, QoS=1|Planned |       |             |
| 2     |DTLS (Control)|123|Payload=512B, QoS=1|Planned|       |             |
| 3     |DTLS (Control)|256|Payload=512B, QoS=1|Planned|       |             |
| 4     |DTLS (Control)|512|Payload=512B, QoS=1|Planned|       |             |
| 5     |DTLS (Control)|1024|Payload=512B, QoS=1|Planned|
Jumlah runs per skenario : ____
Total runs               : ____

DATA LOG (per run):
Run ID      : run-001
Timestamp   : 2026-07-12 09:15:00
Scenario    : DTLS
Seed        : 42
Payload     : 512 Byte
QoS         : 1
Latency     : 18.75 ms
Memory      : 31.4 KB
Throughput  : 58.6 KB/s
CPU Usage   : 39 %
Packet Loss : 0 %
Status      : Success
Notes       : Tidak ditemukan anomali

```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| 1     |DTLS (Control)|42|Payload=512B, QoS=1|Planned |
| 2     |DTLS (Control)|123|Payload=512B, QoS=1|Planned|
| 3     |DTLS (Control)|256|Payload=512B, QoS=1|Planned|
| 4     |DTLS (Control)|512|Payload=512B, QoS=1|Planned|
| 5     |DTLS (Control)|1024|Payload=512B, QoS=1|Planned|
|6	    |TLS 1.3 (Treatment)|42|Payload=512B, QoS=1|Planned|
|7	    |TLS 1.3 (Treatment)|123|Payload=512B, QoS=1|Planned|
|8	    |TLS 1.3 (Treatment)|256|Payload=512B, QoS=1|Planned|
|9	    |TLS 1.3 (Treatment)|512|Payload=512B, QoS=1|Planned|
|10	    |TLS 1.3 (Treatment)|1024|Payload=512B, QoS=1|Planned|

**Total skenario:**2
**Run per skenario:** 5
**Total run keseluruhan:**10

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID | *run-001* |
| Timestamp |2026-07-12 09:15:00|
|Skenario|DTLS|
|Device|NodeMCU ESP8266|
|Operator|Peneliti|
**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| Seed | *42* |
| Code version | *commit abc1234* |
|Payload Size|512 Byte|
|MQTT QoS|1|
|MQTT Broker|Mosquitto|
|TLS Version|DTLS / TLS 1.3|
|Hardware|ESP8266 RAM <64KB|
|Firmware Version|v1.0|
|Code Version|commit abc1234|


**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
|Latency (ms)|Float	|>0|
|Memory Usage (KB)|Float|	0–64|
|Throughput (KB/s)|Float|>0|
|CPU Utilization (%)|Floa0–100|
|Packet Loss (%)	|Float|0–100|
|Execution Time (s)|Float|>0|

**Format output:** [☑] CSV / [☑] JSON / [ ] Database / [ ] Lainnya: ____

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Run gagal (crash) |NodeMCU restart saat proses handshake |Dokumentasikan penyebab, perbaiki konfigurasi, kemudian ulangi run dengan seed yang sama|
| Hasil ekstrem |Latensi mencapai 500 ms, jauh di atas rata-rata |Periksa kondisi jaringan, validasi log, ulangi eksperimen jika diperlukan|
| Waktu eksekusi anomali |Eksekusi berlangsung jauh lebih lama dibanding run lain |Cek penggunaan CPU, memori, dan kestabilan jaringan sebelum mengulang|
| Inkonsistensi dengan run lain |Penggunaan memori berbeda jauh pada parameter yang sama|Verifikasi konfigurasi, firmware, dan parameter eksperimen; jika perlu lakukan pengulangan|

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Pada beberapa tugas praktikum, hasil sering dilaporkan hanya berdasarkan satu kali pengujian (single run). Cara ini berisiko karena hasil dapat dipengaruhi oleh kondisi jaringan, variasi sistem, atau faktor acak sehingga kurang dapat dipercaya dan tidak mewakili performa sebenarnya.
**Yang akan dilakukan berbeda:**
> Pada penelitian ini, setiap skenario akan dijalankan sebanyak 5 kali dengan seed yang berbeda. Seluruh konfigurasi, metrik, dan metadata akan dicatat dalam format CSV dan JSON. Hasil akhir akan dianalisis menggunakan nilai mean, standar deviasi, dan uji statistik (Independent t-test) sehingga kesimpulan yang diperoleh lebih valid, reliabel, dan dapat dipertanggungjawabkan secara ilmiah.
