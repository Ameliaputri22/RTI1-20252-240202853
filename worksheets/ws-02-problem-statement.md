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
  Domain   :  Internet of Things (IoT)
  Konteks  : Sistem pencahayaan rumah dan ruang kelas yang masih dioperasikan secara manual

 
System Context
Input       : Data intensitas cahaya dan keberadaan pengguna dari sensor
Process     : NodeMCU memproses data sensor dan mengontrol lampu secara otomatis
Output      : Status lampu (ON/OFF) sesuai kondisi lingkungan
Outcome     : Penghematan energi listrik dan peningkatan efisiensi penggunaan lampu
Constraints : Keterbatasan jaringan internet, daya perangkat, dan biaya implementasi
Stakeholders: Pengguna rumah, sekolah, pengelola gedung, dan peneliti IoT
 
Fenomena → Problem
Fenomena yang diamati :Banyak lampu masih menyala meskipun ruangan kosong atau kondisi ruangan sudah cukup terang.
Gejala (symptom) yang terukur : Tingginya konsumsi energi listrik akibat penggunaan lampu yang tidak efisien.
Masalah yang didiagnosis :Pengoperasian lampu secara manual menyebabkan pengguna sering lupa mematikan lampu sehingga terjadi pemborosan energi.
Masalah riset (researchable) :Bagaimana merancang sistem pencahayaan cerdas berbasis IoT yang mampu mengontrol lampu secara otomatis untuk mengoptimalkan penggunaan energi listrik?
Variabel yang terukur :Konsumsi energi listrik (Wh), waktu aktif lampu (menit/jam), intensitas cahaya (lux), dan efisiensi energi (%).
Problem Quality Check
  [☑] Clarity — Apakah satu orang membaca akan paham?
  [☑] Measurability — Apakah ada metrik kuantitatif?
  [☑] Relevance — Apakah penting untuk domain?
  [☑] Testability — Apakah bisa gagal?
  [☑] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
Penggunaan lampu yang masih dikendalikan secara manual sering menyebabkan pemborosan energi listrik karena lampu tetap menyala meskipun ruangan tidak digunakan atau kondisi pencahayaan sudah memadai. Permasalahan ini berdampak pada meningkatnya konsumsi listrik dan biaya operasional, terutama pada rumah, sekolah, maupun perkantoran. Seiring berkembangnya teknologi Internet of Things (IoT), sistem pencahayaan dapat diotomatisasi dengan memanfaatkan sensor dan mikrokontroler untuk mengontrol lampu berdasarkan kondisi lingkungan secara real-time. Namun, masih diperlukan penelitian mengenai efektivitas penerapan sistem pencahayaan cerdas dalam mengoptimalkan konsumsi energi listrik. Oleh karena itu, penelitian ini bertujuan merancang dan membangun sistem pencahayaan cerdas berbasis IoT yang mampu mengontrol lampu secara otomatis serta mengukur tingkat efisiensi energi yang dihasilkan.
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

**Apakah terjebak solution-first thinking?** ☑ Tidak
---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input |Data sensor dari perangkat IoT |
| Process | Pengiriman data melalui MQTT dengan enkripsi|
| Output |Data diterima server|
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
> Penggunaan lampu secara manual masih menjadi penyebab utama pemborosan energi listrik karena pengguna sering lupa mematikan lampu saat ruangan tidak digunakan. Kondisi tersebut menyebabkan konsumsi energi meningkat dan biaya listrik menjadi lebih besar. Pemanfaatan teknologi Internet of Things (IoT) memungkinkan pengembangan sistem pencahayaan cerdas yang mampu mengontrol lampu secara otomatis berdasarkan kondisi lingkungan dan keberadaan pengguna. Namun, efektivitas sistem tersebut dalam mengoptimalkan konsumsi energi listrik masih perlu dievaluasi. Oleh karena itu, penelitian ini berfokus pada perancangan dan pembangunan sistem pencahayaan cerdas berbasis IoT serta pengukuran tingkat efisiensi energi yang dihasilkan dibandingkan dengan sistem pencahayaan konvensional.
---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
>Masalah dalam coding biasanya berupa bug, error, atau kegagalan fungsi program yang dapat langsung diidentifikasi dan diperbaiki. Fokusnya adalah membuat sistem berjalan sesuai kebutuhan pengguna. Sementara itu, masalah riset berfokus pada pencarian pengetahuan baru atau solusi yang belum terbukti secara ilmiah. Dalam penelitian, masalah harus dirumuskan secara sistematis, memiliki variabel yang dapat diukur, serta dapat diuji melalui eksperimen sehingga menghasilkan bukti ilmiah yang dapat dipertanggungjawabkan.

