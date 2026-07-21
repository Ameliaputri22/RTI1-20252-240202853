# WS-16: Presentation & Defense (UAS)

> **Bab 16 — Presentasi & Pertahanan Ilmiah**

---

## Ringkasan Materi

### Scientific Defense Model

```
Research Work → Presentation → Questioning → Defense → Evaluation → Acceptance
```

### Presentasi ≠ Ringkasan Paper

| Paper | Presentasi |
|-------|-----------|
| Dibaca (self-paced) | Didengar (presenter-paced) |
| Detail lengkap | Ide kunci + highlight |
| Tabel numerik detail | Grafik visual + angka kunci |
| Pembaca bisa re-read | Audiens dengar sekali |

**Prinsip:** Presentasi membutuhkan **reformulasi**, bukan kompresi. Medium berbeda = pendekatan berbeda.

### Claim-Evidence-Reasoning (CER)

Setiap jawaban defense harus memiliki:
1. **Claim** — Pernyataan yang dijawab
2. **Evidence** — Data/fakta pendukung
3. **Reasoning** — Logika yang menghubungkan evidence ke claim

**Contoh:**
| Pertanyaan | Bad Answer | Good Answer (CER) |
|-----------|-----------|-------------------|
| "Kenapa hanya 3 dataset?" | "Tiga sudah cukup" | "3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy [E]. Generalisasi perlu validasi lanjut — listed as limitation [R]" |
| "Hasil DS-3 menurun?" | "Itu outlier" | "Ya, karena distribusi heavy-tail melanggar asumsi Gaussian [E]. Ini menunjukkan boundary condition metode [R]" |
| "Effect size?" | "p=0.003, jadi signifikan" | "Cohen's d=1.2 (large effect) [E] — bukan hanya signifikan tapi substansial [R]" |

### Slide Design — One Slide, One Message

**Optimal 9-Slide Plan (15 menit):**

| # | Slide | Waktu | Pesan |
|---|-------|-------|-------|
| 1 | Title + context | 1 min | Apa ini tentang apa |
| 2 | Problem + motivation | 2 min | Mengapa penting |
| 3 | Gap + RQ | 1.5 min | Apa yang belum terjawab |
| 4 | Method overview | 2 min | Bagaimana dijawab (diagram) |
| 5 | Key result — tabel | 2 min | Temuan utama |
| 6 | Key result — grafik | 2 min | Pola visual |
| 7 | Interpretation + failure | 2 min | Apa artinya |
| 8 | Limitation + future | 1.5 min | Batasan & arah |
| 9 | Conclusion + contribution | 1 min | Closing message |

### Anticipatory Defense

Prediksi pertanyaan berdasarkan kategori:

| Kategori | Contoh Pertanyaan |
|---------|------------------|
| Problem | "Mengapa masalah ini penting?" |
| Gap | "Bagaimana dengan studi X yang sudah menjawab ini?" |
| Method | "Mengapa metode ini, bukan Y?" |
| Results | "Bagaimana menjelaskan anomali di DS-3?" |
| Generalization | "Apakah bisa diterapkan di domain lain?" |

### Tiga Prinsip Jawaban

1. **Direct** — Jawab dulu, elaborasi kemudian
2. **Data-based** — Tunjuk evidence spesifik
3. **Honest** — Akui limitasi jika memang ada

### Jebakan Kognitif

1. "Presentasi = semua yang ada di paper" → terlalu padat
2. "Slide cantik = presentasi bagus" → konten > estetika
3. "Tidak bisa jawab = gagal" → "I don't know, but..." menunjukkan kejujuran
4. "Tidak perlu latihan — saya paham riset saya" → latihan = menemukan celah

---

## Template A.16 — Defense Preparation Sheet

```
DEFENSE PREPARATION

Slide Deck Plan:
  Total slides : 9 slide utama
  Time per slide : ±1,5–2 menit
  Total waktu : ±15 menit

Slide Outline:
| # | Pesan Utama | Visual | Waktu |
|---|-------------|--------|-------|
1	Judul penelitian dan latar belakang singkat	Cover + ilustrasi IoT	1 menit
2	Permasalahan penelitian	Diagram komunikasi MQTT dan isu keamanan	2 menit
3	Research Gap dan Research Question	Tabel penelitian terdahulu + RQ	1,5 menit
4	Metode penelitian	Diagram alur eksperimen dan blok sistem	2 menit
5	Hasil utama (tabel)	Tabel perbandingan TLS 1.3 dan DTLS	2 menit
6	Hasil utama (grafik)	Bar chart dan box plot	2 menit
7	Interpretasi hasil dan keterbatasan	Diagram hubungan hasil dengan teori	2 menit
8	Limitasi dan penelitian selanjutnya	Daftar poin + diagram future work	1,5 menit
9	Kesimpulan dan kontribusi	Ringkasan hasil penelitian	1 menit

Anticipatory Defense Matrix:
| Kategori | Pertanyaan Potensial | Jawaban (CER) |
|----------|---------------------|---------------|
|Problem|Mengapa memilih keamanan MQTT pada IoT?|Claim: MQTT banyak digunakan pada IoT sehingga keamanan komunikasi penting. Evidence: MQTT digunakan pada perangkat dengan sumber daya terbatas yang rentan terhadap serangan. Reasoning: Perbandingan TLS 1.3 dan DTLS membantu menentukan protokol yang lebih efisien.|
|Gap|Bukankah TLS dan DTLS sudah sering dibandingkan?|Claim: Perbandingan pada perangkat IoT dengan RAM <64 KB masih terbatas. Evidence: Literatur lebih banyak berfokus pada komputer atau server. Reasoning: Penelitian ini mengisi kesenjangan pada perangkat IoT berdaya rendah.|
|Method|Mengapa menggunakan ESP8266?|Claim: ESP8266 mewakili perangkat IoT dengan sumber daya terbatas. Evidence: RAM kurang dari 64 KB dan banyak digunakan dalam aplikasi IoT. Reasoning: Hasil lebih relevan untuk implementasi IoT sederhana.|
|ResultsMengapa TLS 1.3 memiliki latensi lebih rendah?|Claim: TLS 1.3 mengurangi jumlah proses handshake. Evidence: Hasil menunjukkan rata-rata latensi lebih rendah dibandingkan DTLS. Reasoning: Pengurangan overhead komunikasi meningkatkan efisiensi.|
|Generalization|Apakah hasil dapat diterapkan pada semua perangkat IoT?|Claim: Belum sepenuhnya. Evidence: Eksperimen hanya menggunakan ESP8266. Reasoning: Pengujian pada perangkat lain diperlukan untuk meningkatkan validitas eksternal.|

Latihan:
  Latihan 1: [tanggal] — [catatan timing & feedback]
  Latihan 2: [tanggal] — [catatan timing & feedback]
  Latihan 3: [tanggal] — [catatan timing & feedback]
```

---

## Latihan 1 — Slide Outline

Rencanakan presentasi 15 menit untuk riset Anda.

| # | Pesan Utama | Visual yang Digunakan | Waktu |
|---|-------------|----------------------|-------|
|1|Judul penelitian dan tujuan|Cover penelitian|1 menit|
|2|Permasalahan keamanan MQTT pada IoT|Diagram komunikasi MQTT|2 menit|
|3|Research Gap dan Research Question|Tabel gap penelitian|1,5 menit|
|4|Metode penelitian dan desain eksperimen|Flowchart dan diagram blok sistem|2 menit|
|5|Hasil pengujian|Tabel hasil eksperimen|2 menit|
|6|Visualisasi hasil|Bar chart dan box plot|2 menit|
|7|Interpretasi hasil dan keterbatasan|Diagram hubungan hasil dengan teori|2 menit|
|8|Future work|Diagram pengembangan penelitian|1,5 menit|
|9|Kesimpulan dan kontribusi|Ringkasan poin utama|1 menit|
**Total waktu estimasi:** 15 menit

---

## Latihan 2 — Anticipatory Defense

Prediksi 5 pertanyaan yang mungkin diajukan penguji, lalu siapkan jawaban CER.

| # | Kategori | Pertanyaan | Claim | Evidence | Reasoning |
|---|----------|-----------|-------|----------|-----------|
1	Problem	Mengapa memilih MQTT?	MQTT merupakan protokol yang banyak digunakan pada IoT.	MQTT ringan dan sesuai untuk perangkat dengan sumber daya terbatas.	Oleh karena itu, keamanan MQTT menjadi penting untuk diteliti.
2	Method	Mengapa menggunakan ESP8266?	ESP8266 mewakili perangkat IoT berbiaya rendah.	Memiliki RAM <64 KB dan banyak digunakan dalam implementasi IoT.	Hasil penelitian relevan dengan kondisi nyata pada perangkat IoT sederhana.
3	Method	Mengapa menggunakan Independent Samples t-test?	Karena membandingkan dua kelompok independen.	Eksperimen terdiri atas kelompok TLS 1.3 dan DTLS yang berbeda.	Uji ini sesuai untuk mengetahui apakah terdapat perbedaan rata-rata yang signifikan.
4	Results	Mengapa TLS 1.3 lebih baik?	TLS 1.3 memiliki latensi dan penggunaan memori yang lebih rendah.	Berdasarkan hasil eksperimen, rata-rata latensi dan memori lebih kecil dibandingkan DTLS.	Hal tersebut menunjukkan TLS 1.3 lebih efisien pada kondisi pengujian yang dilakukan.
5	Generalization	Apakah hasil berlaku untuk semua perangkat IoT?	Belum tentu.	Pengujian hanya dilakukan pada ESP8266.

---

## Latihan 3 — Simulasi Q&A

Minta teman/kolega mengajukan 3 pertanyaan tentang riset Anda. Catat pertanyaan dan evaluasi jawaban Anda.

| # | Pertanyaan | Jawaban Saya | Evaluasi |
|---|-----------|-------------|---------|
|1|	Mengapa tidak menggunakan Raspberry Pi?|Karena penelitian berfokus pada perangkat dengan sumber daya terbatas. ESP8266 lebih mewakili mikrokontroler IoT dibandingkan Raspberry Pi yang memiliki spesifikasi jauh lebih tinggi|☑ Direct ☑ Data-based ☑ Honest|
|2|Mengapa hanya menggunakan dua metrik?|Latensi dan penggunaan memori dipilih karena sesuai dengan Research Question. Metrik lain seperti throughput dan CPU utilization direkomendasikan sebagai penelitian lanjutan.|☑ Direct ☑ Data-based ☑ Honest|
|3|Bagaimana jika hasil tidak signifikan?|Hasil tersebut tetap merupakan temuan ilmiah. Penelitian akan menganalisis penyebabnya, menjelaskan batasan metode, dan menyampaikan rekomendasi untuk penelitian berikutnya.|☑ Direct ☑ Data-based ☑ Honest|

**Pertanyaan yang paling sulit dijawab:**
>Bagaimana hasil penelitian dapat digeneralisasikan pada berbagai jenis perangkat IoT dengan spesifikasi yang berbeda?

**Apa yang perlu disiapkan lebih baik:**
> Menyiapkan referensi tambahan mengenai implementasi TLS 1.3 dan DTLS pada berbagai platform IoT serta memahami keterbatasan penelitian secara lebih mendalam agar dapat memberikan jawaban yang didukung oleh bukti.

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-16 — dari paradigma riset hingga presentasi — bagian mana yang paling mengubah cara Anda berpikir tentang riset? Apa satu hal yang akan selalu Anda terapkan di riset berikutnya?

**Insight terbesar:**
> Seluruh rangkaian WS-01 hingga WS-16 menunjukkan bahwa penelitian bukan hanya tentang memperoleh hasil yang baik, tetapi tentang menyusun argumen ilmiah yang sistematis, mulai dari identifikasi masalah, penyusunan pertanyaan penelitian, desain eksperimen yang adil, validasi data, analisis yang tepat, hingga kemampuan mempertanggungjawabkan hasil melalui presentasi dan sesi tanya jawab.

**Yang akan selalu diterapkan:**
> Pada penelitian berikutnya, saya akan selalu menyusun Research Question yang jelas, merancang eksperimen dengan variabel yang terkontrol, melakukan multiple run, mendokumentasikan seluruh proses secara lengkap, serta mendukung setiap kesimpulan dengan data, analisis statistik, dan interpretasi yang sesuai. Dengan demikian, hasil penelitian menjadi lebih valid, transparan, dapat direplikasi, dan lebih mudah dipertahankan dalam presentasi maupun publikasi ilmiah.
