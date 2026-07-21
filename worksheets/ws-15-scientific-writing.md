# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title   : Analisis Perbandingan TLS 1.3 dan DTLS terhadap Latensi dan Penggunaan Memori pada Protokol MQTT di Perangkat Internet of Things (IoT)
Target  : [☑] Jurnal  [ ] Konferensi  [ ] Laporan

Section Check:
  [☑] Abstract — masalah, metode, hasil utama, kontribusi (max 250 kata)
  [☑] Introduction — konteks → gap → RQ → kontribusi → struktur paper
  [☑] Related Work — concept-centric, gap positioning
  [☑] Method — reproducible: desain, variabel, metrik, setup, prosedur
  [☑] Results — tabel + grafik + observasi (tanpa interpretasi)
  [☑] Discussion — interpretasi, perbandingan, implikasi, limitation
  [☑] Conclusion — jawaban RQ, kontribusi, future work

Consistency Matrix:
  [☑] RQ di Introduction = RQ di Method = RQ di Conclusion
  [☑] Variabel di Method = variabel di Results
  [☑] Klaim di Discussion didukung data di Results
  [☑] Limitasi di Discussion di-address di Conclusion/Future Work

Writing Quality:
  [☑] Clarity — mudah dipahami tanpa re-read
  [☑] Precision — tidak ada istilah ambigu
  [☑] Conciseness — tidak ada kalimat redundan
```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section | Konten Utama (2-3 kalimat) | Target Kata |
|---------|---------------------------|------------|
| Abstract |Menjelaskan pentingnya keamanan komunikasi MQTT pada IoT. Penelitian membandingkan TLS 1.3 dan DTLS terhadap latensi dan penggunaan memori menggunakan eksperimen pada ESP8266. Hasil menunjukkan TLS 1.3 memiliki latensi dan penggunaan memori yang lebih rendah dibandingkan DTLS.| 200-250 |
| Introduction |Menguraikan perkembangan IoT, kebutuhan keamanan komunikasi, penggunaan MQTT, serta keterbatasan penelitian sebelumnya dalam membandingkan TLS 1.3 dan DTLS pada perangkat dengan sumber daya terbatas. Diakhiri dengan Research Question dan kontribusi penelitian.| 500-700 |
| Related Work |Membahas penelitian terdahulu mengenai MQTT, TLS, DTLS, keamanan komunikasi IoT, serta mengidentifikasi kesenjangan penelitian yang menjadi dasar eksperimen.| 700-1000 |
| Method |Menjelaskan desain eksperimen, perangkat ESP8266, konfigurasi MQTT, variabel independen dan dependen, prosedur pengujian, proses pengumpulan data, serta metode analisis menggunakan Independent Samples t-test.| 800-1200 |
| Results |Menyajikan hasil eksperimen dalam bentuk tabel dan grafik yang menampilkan nilai rata-rata, standar deviasi, serta hasil uji statistik tanpa interpretasi.| 500-800 |
| Discussion |Menginterpretasikan hasil penelitian, menjelaskan penyebab perbedaan performa TLS 1.3 dan DTLS, membandingkan dengan penelitian sebelumnya, serta membahas keterbatasan penelitian dan implikasinya.| 600-900 |
| Conclusion |Menyimpulkan jawaban terhadap Research Question, menjelaskan kontribusi penelitian, serta memberikan saran untuk penelitian selanjutnya.| 200-400 |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

|  | Intro | Method | Result | Discussion | Conclusion |
|--|-------|--------|--------|-----------|-----------|
RQ1	✓	✓	✓	✓	✓
RQ2	✓	✓	✓	✓	✓
Metrik utama (Latency & Memory)	✓	✓	✓	✓	✓
Variabel Independen (TLS 1.3/DTLS)	✓	✓	✓	✓	✓
Variabel Dependen (Latency, Memory)	✓	✓	✓	✓	✓
Klaim/Kontribusi	✓	✓	✓	✓	✓
**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan:**
> Tidak ditemukan inkonsistensi. Seluruh Research Question, variabel penelitian, metrik evaluasi, dan kontribusi telah muncul secara konsisten pada setiap bagian artikel.

**Tindakan perbaikan:**
> Memastikan setiap hasil yang ditampilkan pada bagian Results dijelaskan pada Discussion dan seluruh kesimpulan secara langsung menjawab Research Question yang telah dirumuskan pada bagian Introduction.

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:**
> Protokol TLS 1.3 mempunyai performa yang lebih baik daripada DTLS sehingga lebih bagus digunakan pada perangkat IoT. Berdasarkan hasil penelitian, performanya meningkat dan sistem menjadi lebih baik. Oleh karena itu, TLS 1.3 direkomendasikan untuk digunakan.

| Kriteria | Evaluasi | Perbaikan |
|----------|---------|-----------|
|Clarity|Istilah "performa" dan "lebih baik" masih umum.|Sebutkan metrik yang meningkat, misalnya latensi dan penggunaan memori.|
|Precision|Tidak mencantumkan data pendukung.|Tambahkan nilai rata-rata atau hasil uji statistik.|
|Conciseness|Kalimat kedua dan ketiga bersifat berulang.|Gabungkan menjadi satu pernyataan yang ringkas dan informatif.|

**Paragraf setelah perbaikan:**
> Berdasarkan hasil eksperimen, TLS 1.3 menghasilkan rata-rata latensi sebesar 17,8 ± 0,9 ms dan penggunaan memori sebesar 28,4 ± 1,1 KB, sedangkan DTLS menghasilkan latensi 19,3 ± 1,2 ms dan penggunaan memori 31,2 ± 1,4 KB. Hasil uji *Independent Samples t-test* menunjukkan bahwa perbedaan latensi antara kedua protokol signifikan secara statistik (p < 0,05), sehingga TLS 1.3 dapat dipertimbangkan sebagai alternatif yang lebih efisien untuk komunikasi MQTT pada perangkat IoT dengan sumber daya terbatas.


---

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> Menulis tentang riset hanya menjelaskan apa yang telah dilakukan, sedangkan menulis sebagai argumen riset berarti menyusun alur yang logis mulai dari permasalahan, kesenjangan penelitian, pertanyaan penelitian, metode, hasil, hingga kontribusi yang didukung oleh bukti. Dengan demikian, setiap bagian artikel saling berkaitan dan memperkuat kesimpulan yang dihasilkan.

Urutan penulisan Method → Results → Discussion → Introduction → Conclusion membantu meningkatkan kualitas tulisan karena bagian yang paling objektif dan stabil disusun terlebih dahulu. Setelah hasil dan pembahasannya jelas, bagian pendahuluan dapat disesuaikan agar benar-benar mengarah pada temuan penelitian, sedangkan abstrak dan kesimpulan dapat merangkum isi artikel secara lebih akurat dan konsisten.

