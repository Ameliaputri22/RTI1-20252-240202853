# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik : Keamanan IoT pada MQTT (TLS vs DTLS)
Database : Google Scholar
Query : ("IoT security" OR "MQTT security") AND ("TLS" OR "DTLS") AND ("performance" OR "overhead") NOT ("medical")
Tahun : 2020–2025
Hasil awal : 30 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
| Kim et al.|2020|TLS pada MQTT|Dataset jaringan IoT|Latensi meningkat 20%|Tidak bandingkan DTLS| 
Singh et al.|2021|DTLS untuk IoT|Simulasi|Lebih ringan dari TLS|Tidak diuji di MQTT|
Zhang et al.|2022|CNN untuk deteksi intrusi IoT|KDD Dataset|Akurasi 94%|Dataset lama
Lee et al.|2023|Hybrid security IoT|Dataset real IoT|	Keamanan meningkat|Resource tinggi
Ahmed et al|2024|Lightweight encryption|Simulasi IoT|	Overhead rendah|Belum dibanding TLS/DTLS|

Pola yang ditemukan:
  Metode dominan     : TLS, DTLS, dan lightweight encryption
  Dataset umum       : Dataset simulasi dan dataset lama (KDD, NSL-KDD)
  Limitasi berulang  :  -Tidak ada perbandingan langsung TLS vs DTLS pada MQTT
                        -Dataset tidak realistis
                        -Fokus hanya pada satu metode

GAP IDENTIFICATION

Gap 1: (Method + Performance Gap)
  Deskripsi    : Belum ada penelitian yang secara langsung membandingkan performa TLS 1.3 dan DTLS pada protokol MQTT
  Bukti        :Studi hanya fokus pada salah satu metode tanpa komparasi
  Signifikansi : Penting untuk menentukan metode keamanan paling efisien pada IoT

Gap 2: [Jenis:Data + Context Gap]
  Deskripsi    :Sebagian besar penelitian menggunakan dataset simulasi atau dataset lama
  Bukti        :Tidak banyak studi menggunakan data real-time IoT
  Signifikansi :Hasil penelitian mungkin tidak relevan dengan kondisi dunia nyata

Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|DTLS pada IoT|Alternatif TLS untuk perangkat ringan|Banyak digunakan pada IoT low-resource|Singh et al., 202|
| TLS pada MQTT|Digunakan untuk keamanan komunikasi IoT|Umum digunakan di banyak penelitian|Kim et al., 2020|
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:**Keamanan MQTT pada IoT
**Query pencarian:** ("MQTT security" AND "TLS" AND "DTLS" AND "IoT performance")
**Database:** Google Scholar

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | |Kim et al.|2020|TLS|IOT traffic|Latensi tinggi|
| 2 | |Singh et al.|2021|DTLS |simulasi|lebih ringan|
| 3 | | Zhang et al.|2022 |CNN |KDD|akurasi tinggi|
| 4 | |Lee et al.|2023 |Hybrid |Real IOT|Aman|
| 5 | |Ahmad et al.|2024 |Lightweight|Simulasi|Efisien|

**Pola yang terlihat — Metode dominan:**TLS & DTLS
**Limitasi yang berulang:**Tidak ada perbandingan langsung + dataset kurang realistis

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | Ya|Performa TLS menyebabkan latensi tinggi pada IoT
| Method Gap |Ya|Belum ada perbandingan TLS vs DTLS pada MQTT|
| Data Gap |Ya|Dataset banyak yang tidak realistis|
| Context Gap |Ya|Belum diuji pada perangkat low-resource nyata|

**Gap utama yang dipilih:**Method + Performance Gap
**Mengapa gap ini penting **
> Karena pemilihan metode keamanan yang tidak tepat dapat menyebabkan sistem IoT menjadi lambat atau tidak efisien, sehingga diperlukan perbandingan yang jelas untuk menentukan solusi terbaik.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 |TLS pada MQTT |Digunakan dalam sistem keamanan IoT|Banyak dipakai| Tidak|Kim et al., 2020|
| 2 |DTLS pada IoT | Alternatif untuk resource rendah|Umum digunakan|Tidak|Singh et al., 2021|

**Apakah pemilihan baseline ini bisa dianggap straw man?** |tidak|
> Justifikasi: Kedua baseline merupakan metode yang benar-benar digunakan dalam praktik dan literatur, sehingga perbandingan adil.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Perbedaan antara klaim “belum ada yang meneliti ini” dengan research gap yang valid adalah bahwa klaim tanpa bukti hanya berupa asumsi, sedangkan research gap harus didukung oleh hasil pencarian literatur yang sistematis. Gap yang valid ditunjukkan dengan adanya pola dari beberapa penelitian yang memiliki keterbatasan serupa, misalnya tidak adanya perbandingan metode atau penggunaan dataset yang tidak representatif. Cara membuktikan gap adalah dengan mendokumentasikan proses pencarian (query, database, tahun), menganalisis beberapa paper secara concept-centric, lalu menunjukkan secara jelas keterbatasan yang berulang sehingga dapat disimpulkan bahwa masih ada ruang penelitian yang belum terjawab.
> ___________________________________________________
