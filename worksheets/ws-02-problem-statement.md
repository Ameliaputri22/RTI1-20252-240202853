# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Keamanan IoT
  Konteks  : Sistem komunikasi perangkat IoT menggunakan protokol MQTT pada perangkat dengan keterbatasan memori
 
System Context
Input : Data sensor yang dikirim dari perangkat IoT
Process : Pengiriman data melalui protokol MQTT dengan enkripsi (TLS/DTLS)
Output : Data yang diterima oleh server/broker MQTT
Outcome : Keamanan data meningkat tanpa mengorbankan performa sistem
Constraints : Keterbatasan RAM (<64KB), bandwidth terbatas, dan daya perangkat rendah
Stakeholders : Developer IoT, pengguna sistem, perusahaan teknologi, dan peneliti keamanan
 
Fenomena → Problem
Fenomena yang diamati :Penggunaan IoT semakin meningkat namun keamanan komunikasi masih menjadi tantangan
Gejala (symptom) yang terukur :Latensi meningkat dan penggunaan memori tinggi saat menggunakan enkripsi
Masalah yang didiagnosis : Protokol keamanan seperti TLS menambah overhead yang signifikan pada perangkat IoT dengan resource terbatas
Masalah riset (researchable) : Belum ada perbandingan yang jelas mengenai efisiensi overhead antara TLS 1.3 dan DTLS pada MQTT untuk perangkat IoT dengan RAM terbatas.
Variabel yang terukur : Latensi (ms), penggunaan memori (KB), throughput, dan tingkat keamanan
Problem Quality Check
  [ ] Clarity — Apakah satu orang membaca akan paham?
  [ ] Measurability — Apakah ada metrik kuantitatif?
  [ ] Relevance — Apakah penting untuk domain?
  [ ] Testability — Apakah bisa gagal?
  [ ] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
  Dalam sistem IoT yang menggunakan protokol MQTT, penerapan mekanisme keamanan seperti TLS seringkali menimbulkan overhead yang signifikan pada perangkat dengan keterbatasan sumber daya, terutama pada memori dan latensi komunikasi. Hal ini menjadi masalah karena perangkat IoT umumnya memiliki RAM yang sangat terbatas (<64KB), sehingga penggunaan protokol keamanan dapat mempengaruhi performa sistem secara keseluruhan. Meskipun keamanan merupakan aspek penting, belum terdapat studi yang secara komprehensif membandingkan efisiensi antara TLS 1.3 dan DTLS dalam konteks MQTT pada perangkat IoT dengan resource terbatas. Oleh karena itu, penelitian ini bertujuan untuk mengukur dan membandingkan overhead kedua protokol tersebut berdasarkan metrik seperti latensi, penggunaan memori, dan throughput guna menentukan solusi yang paling optimal.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Keamanan IoT

| Tahap | Hasil |
|-------|-------|
| Reality |Banyak perangkat IoT menggunakan komunikasi yang tidak aman |
| Observed Issue (Symptom) | Terjadi peningkatan latensi saat menggunakan enkripsi|
| Diagnosed Problem (Root Cause) | Overhead enkripsi tidak sesuai dengan keterbatasan perangkat |
| Researchable Problem |Belum ada perbandingan efisiensi TLS vs DTLS pada MQTT di perangkat low-resource |
| Measurable Variable |Latensi, penggunaan RAM, throughput |

**Apakah terjebak solution-first thinking?** [ X]  Ya / [ ] Tidak
---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input |Data sensor dari perangkat IoT |
| Process | Pengiriman data melalui MQTT dengan enkripsi|
| Output | Pengiriman data melalui MQTT dengan enkripsi|
| Outcome | Keamanan dan efisiensi sistem|
| Constraints |RAM kecil, bandwidth terbatas |
| Stakeholders |Developer, pengguna, peneliti |

**Komponen mana yang paling relevan dengan masalah riset?** Process (karena terkait langsung dengan penggunaan TLS/DTLS)

---

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity | 5 |Masalah dijelaskan dengan jelas dan spesifik | 
| Measurability |5|Menggunakan metrik kuantitatif |
| Relevance | 5 |Penting untuk keamanan IoT |
| Testability | 5 |Bisa diuji melalui eksperimen |
| Impact | 5 |Memberikan solusi optimal untuk IoT |

**Skor total:** 25 / 25

**Problem statement versi final (1 paragraf):**
> Dalam implementasi sistem IoT berbasis MQTT, penggunaan protokol keamanan seperti TLS dan DTLS berpotensi menimbulkan overhead yang signifikan terhadap performa perangkat dengan keterbatasan sumber daya. Permasalahan ini menjadi krusial karena sebagian besar perangkat IoT memiliki kapasitas memori dan daya yang rendah. Hingga saat ini, belum terdapat analisis komprehensif yang membandingkan efisiensi kedua protokol tersebut dalam kondisi resource terbatas. Oleh karena itu, penelitian ini berfokus pada pengukuran dan perbandingan performa TLS 1.3 dan DTLS berdasarkan metrik latensi, penggunaan memori, dan throughput untuk menentukan solusi keamanan yang paling optimal.

---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
>Masalah dalam coding biasanya berupa bug atau error yang langsung terlihat dan harus segera diperbaiki agar sistem dapat berjalan dengan baik. Sedangkan masalah riset lebih berfokus pada menemukan dan membuktikan gap dalam pengetahuan yang belum terjawab. Dalam riset, masalah harus dirumuskan secara sistematis, dapat diukur, dan dapat diuji, tidak hanya sekadar menyelesaikan masalah praktis tetapi juga menghasilkan pemahaman baru yang dapat digunakan oleh orang lain.

