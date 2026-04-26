# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (DSR). Penting untuk membedakan keduanya:

| Paradigma | Cara Kerja | Contoh di TI |
|-----------|-----------|---------------|
| **Positivis** | Uji hipotesis dengan eksperimen terkontrol | Apakah CNN lebih akurat dari RF pada dataset X? |
| **Design Science Research** | Bangun artefak (sistem/model/framework) untuk menguji proposisi | Dapatkah arsitektur hybrid CNN+LSTM membuktikan peningkatan recall ≥5%? |
| **Interpretivis** | Pahami makna melalui konteks & kualitatif | Bagaimana peneliti manafsirkan anomali data sensor IoT? |

Dalam DSR, artefak **bukan tujuan akhir** — ia adalah instrumen untuk menghasilkan pengetahuan. Pertanyaan riset tetap harus difalsifikasi.

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Amelia Putri Azzahra
Tanggal          : 06 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: Apakah akurasi tersebut diuji pada dataset yang seimbang dan apakah dibandingkan dengan metode lain secara adil?
Data yang dibutuhkan untuk verifikasi:
   - Data yang dibutuhkan untuk verifikasi: Metode evaluasi (cross-validation/test set), confusion matrix, serta perbandingan dengan baseline.

2. Posisi paradigma:
   - Pendekatan: Positivis dan Design Science
   - Alasan: Karena penelitian di bidang TI umumnya menggunakan data kuantitatif untuk menguji hipotesis (positivis) serta membangun model atau sistem untuk meningkatkan performa (design science).

3. Identifikasi distorsi:
   - Asumsi tersembunyi: Dataset dianggap mewakili kondisi dunia nyata.
   - Sumber bias potensial:Sampling bias (data tidak beragam), overfitting, dan pemilihan metrik yang tidak tepat.
   - Langkah mitigasi: Menggunakan dataset beragam, cross-validation, dan evaluasi dengan beberapa metrik (precision, recall, F1-score).
  
4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: Hasil eksperimen, termasuk data yang tidak sesuai harapan (negative result).
   - Batasan yang diakui sejak awal: Keterbatasan dataset, model, serta lingkungan pengujian.
   
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

> **Panduan pencarian paper:** Gunakan [IEEE Xplore](https://ieeexplore.ieee.org), [ACM Digital Library](https://dl.acm.org), atau Google Scholar. Pilih paper **tahun 2020 ke atas**, di topik yang Anda minati: deteksi anomali, klasifikasi citra, NLP, keamanan siber, IoT, dsb.
>
> **Contoh domain TI:** "Deteksi anomali lalu-lintas jaringan menggunakan CNN — akurasi meningkat 94% vs baseline SVM 87%." Distorsi potensial: apakah dataset normal/anomali seimbang? Apakah hanya diuji pada satu vendor traffic?

**Paper yang dipilih:**
> Judul:Network Intrusion Detection Using Deep Learning: A Review
> Penulis (Tahun):Kim et al. (2020)
> Sumber/Link DOI:

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data |Mengambil dataset trafik jaringan (misalnya KDD Cup) | Dataset lama, tidak mencerminkan kondisi terbaru |
| Data → Processing |Normalisasi dan pembersihan data | Menghapus data penting (outlier)|
| Processing → Analysis |Melatih model CNN | (outlier)Overfitting pada dataset |
| Analysis → Inference | Membandingkan akurasi dengan metode lain| Perbandingan tidak adil|
| Inference → Knowledge |Menyimpulkan CNN lebih baik | Generalisasi berlebihan |

**Distorsi paling besar di tahap:**  Data → Processing

**Dua distorsi spesifik yang teridentifikasi:**
1. Dataset tidak representatif (dataset lama)
2. Penghapusan outlier tanpa alasan yang jelas



---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Harus melaporkan hasil dengan dan tanpa outlier |
| Transparansi |Menjelaskan alasan penghapusan outlier secara jelas |
| Peer review |Reviewer dapat menilai apakah penghapusan valid |

**Keputusan akhir dan justifikasi:**
> Outlier boleh dihapus hanya jika terbukti merupakan kesalahan data atau noise, dan harus dilaporkan kedua hasilnya agar penelitian tetap transparan dan dapat dipercaya.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Deteksi Anomali Jaringan Menggunakan CNN

> **Skala 1–5:** 1 = tidak sesuai sama sekali dengan topik ini, 5 = sangat sesuai dan dominan digunakan pada riset bertopik serupa.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | 5 — berbasis data dan eksperimen | 1 — tidak fokus pada makna | 5 — membangun model CNN
| Jenis data yang dikumpulkan | Log jaringan, akurasi, precision | Wawancara | Hasil performa model |
| Limitasi paradigma |Tidak memahami konteks | Subjektif | Fokus pada artefak, bukan teori | 

**Paradigma yang dipilih:**Positivis + Design Science
Alasan: Karena penelitian menggunakan data numerik untuk menguji performa model dan juga membangun sistem (CNN) sebagai solusi.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelum membaca materi ini, saya belum terlalu kritis terhadap klaim seperti “95% akurat”. Setelah memahami rantai distorsi, saya akan mempertanyakan dataset, metode evaluasi, potensi bias, serta apakah hasil tersebut dapat digeneralisasi ke kondisi nyata.
