# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

> **Mengapa reproducibility penting?** Sains dibangun di atas prinsip verifikasi — temuan harus bisa dikonfirmasi oleh peneliti lain. _Replicability crisis_ yang terjadi di banyak paper riset ML/AI disebabkan oleh environment tidak terdokumentasi: orang lain tidak bisa reproduksi, hasil diragukan, kepercayaan terhadap temuan hilang. Prinsip: **dokumentasi environment = snapshot kredibilitas riset Anda.**

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
   - **Docker** = teknologi container yang "membungkus" aplikasi beserta seluruh dependency-nya dalam satu unit terisolasi. Hasilnya: kode berjalan identik di laptop, server, maupun reviewer lain. Intro singkat: `docker run -v $(pwd):/workspace environment-image python run_experiment.py`
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Dependency Locking

Mengandalkan "install library terbaru" berbahaya: versi berbeda = perilaku berbeda = hasil tidak reproducible. Praktik:
- **Python**: buat `requirements.txt` dengan versi eksplisit: `scikit-learn==1.3.2`, lalu kunci dengan `pip freeze > requirements.txt`
- **Conda**: gunakan `conda env export > environment.yml` untuk snapshot lengkap
- **Node.js/R/Julia**: gunakan `package-lock.json` / `renv.lock` / `Project.toml` — semua fungsi serupa: lock versi + hash

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : Intel Core i5-1135G7
  RAM     : 8 GB DDR4
  GPU     : Intel Iris Xe Graphics
  Storage : SSD 512 GB

Software:
  OS        : Windows 11 Pro 64-bit
  Runtime   : Arduino IDE 2.3.2
  Framework : Blynk IoT Platform dan ESP8266 Board Package

Dependencies:

| Library           | Version | Sumber                  | Hash/Checksum |
|-------------------|---------|-------------------------|---------------|
| ESP8266WiFi       | 1.0     | Arduino Library Manager | N/A |
| Blynk             | 1.3.2   | Arduino Library Manager | N/A |
| ArduinoJson       | 7.0.4   | Arduino Library Manager | N/A |
| ESP8266HTTPClient | 1.2     | Arduino Library Manager | N/A |
| Wire              | 1.0     | Arduino IDE Default     | N/A |

Konfigurasi:
  Config file     : config.h
  Random seed     : 42
  Hyperparameters :
                   - Ambang batas LDR = 500 lux
                   - Interval monitoring = 5 detik
                   - WiFi update rate = 1 detik
                   - Status relay = ON/OFF otomatis
                   - Jadwal operasi lampu = 18.00–06.00

Reproducibility Check:
  [✓] Dependency terdokumentasi (requirements.txt / lock file)
  [✓] Seed ditetapkan di semua level (Arduino program)
  [✓] Config di version control (GitHub)
  [✓] README instruksi reproduksi lengkap
## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU |Intel Core i5-1135G7 |
| RAM |8 GB DDR4|
| GPU |Intel Iris Xe Graphics |
| OS |Windows 11 Pro 64-bit |
| Runtime |Arduino IDE 2.3.2|
| Framework |ESP8266 Board Package, Blynk IoT|
| Random Seed |42|

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
|ESP8266WiFi|1.0|Menghubungkan NodeMCU ke jaringan WiFi|
|Blynk |1.3.2|Komunikasi antara perangkat IoT dan aplikasi smartphone |
|ArduinoJson |7.0.4|Pengolahan data JSON |
|ESP8266HTTPClient|1.2|Komunikasi HTTP dengan server|
|Wire |1.0|Komunikasi sensor dan modul tambahan |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | 42 |Konsumsi Energi (kWh)| — |
| 2 |42|Konsumsi Energi (kWh)| [☑] Ya |
| 3 |42 |Konsumsi Energi (kWh) | [☑] Ya|

**Jika hasil berbeda, kemungkinan penyebab:**
Koneksi WiFi tidak stabil.
Intensitas cahaya lingkungan berubah selama pengujian.
Sensor LDR mengalami noise pembacaan.
Waktu pengujian tidak konsisten.
Adanya perangkat listrik lain yang memengaruhi konsumsi energi.

___________________________________________________

**Checklist kontrol yang sudah diterapkan:**
- [☑] Random seed di-set di semua level
- [☑] Tidak ada background process yang mengganggu
- [☑] Cache dibersihkan antar-run
- [☑] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen
Rancang Bangun Sistem Pencahayaan Cerdas Berbasis IoT untuk Optimalisasi Konsumsi Energi Listrik

## 1. Environment
Hardware:
- Intel Core i5
- RAM 8 GB
- NodeMCU ESP8266
- Sensor LDR
- Modul Relay 1 Channel
- Lampu LED 10 Watt

Software:
- Windows 11
- Arduino IDE 2.3.2
- Blynk IoT

## 2. Installation
1. Install Arduino IDE.
2. Tambahkan Board ESP8266.
3. Install library ESP8266WiFi dan Blynk.
4. Upload program ke NodeMCU.
5. Hubungkan perangkat ke WiFi dan aplikasi Blynk.

## 3. Data
Data berupa:
- Status lampu (ON/OFF)
- Intensitas cahaya dari sensor LDR
- Lama penggunaan lampu (jam)
- Konsumsi energi listrik (kWh)

## 4. Execution
1. Nyalakan sistem Smart Lamp.
2. Hubungkan ke aplikasi Blynk.
3. Jalankan pengujian selama periode tertentu.
4. Simpan hasil monitoring ke file log.

## 5. Configuration
File konfigurasi:
- SSID WiFi
- Password WiFi
- Token Blynk
- Ambang batas sensor LDR
- Jadwal otomatis lampu

## 6. Expected Output
Output yang dihasilkan:
- Monitoring status lampu secara real-time.
- Grafik penggunaan energi listrik.
- Data konsumsi energi dalam satuan kWh.
- Perbandingan konsumsi energi antara sistem konvensional dan Smart Lamp IoT.

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [☑] Repeatability
**Komponen yang belum terdokumentasi:**
> Diagram rangkaian lengkap Smart Lamp.
Dokumentasi konfigurasi Blynk.
File source code yang digunakan.
Data hasil pengujian mentah.
Prosedur kalibrasi sensor LDR.
