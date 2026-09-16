# Kuis Esai Sistem Kendali & Penilaian

Aplikasi kuis esai berbasis web (single-file HTML) untuk mata pelajaran Sistem Kendali. Program menampilkan 10 soal esai dari 20 bank soal secara acak, menilai jawaban siswa secara otomatis menggunakan rubrik bertingkat berbasis kata kunci, serta menyediakan fitur koreksi mandiri.

Fitur utama:

- Terdiri dari satu file HTML tanpa dependensi (tanpa framework, tanpa backend).
- 20 bank soal, 10 soal ditampilkan secara acak setiap sesi.
- Penilaian otomatis dengan rubrik bertingkat 0-10 per soal.

## Fitur

- **Form identitas siswa** — Nama dan kelas wajib diisi sebelum mulai mengerjakan.
- **Pengacakan soal** — 10 dari 20 soal dipilih acak setiap kali kuis dimulai atau diacak ulang.
- **Penilaian otomatis** — Jawaban dinilai dari kecocokan kata kunci dengan bobot ganda pada kata kunci inti, deteksi sinonim, struktur kalimat, dan pola negasi.
- **Umpan balik edukatif** — Menampilkan kunci jawaban, kata kunci yang cocok/belum, rasio kecocokan, serta peringatan jika jawaban menyebutkan hal yang seharusnya tidak disebut (konsep terbalik).
- **Koreksi mandiri** — Siswa dapat menyesuaikan skor tiap soal secara manual (Benar 10, Hampir 8, Setengah 5, Kurang 2, Salah 0).
- **Hasil akhir** — Total skor (maks 100), progress bar, dan predikat LULUS / BELUM LULUS.
- **Mode ujian (CBT)** — Layar otomatis masuk mode penuh; jika tab/browser ditinggalkan lebih dari 5 detik, kuis otomatis dikumpulkan.
- **Acak ulang soal** — Mengacak dan mereset seluruh jawaban dan skor dengan konfirmasi.

## Cara Menjalankan

1. Buka folder tempat file `system kendali kwis.html` berada.
2. Klik dua kali file tersebut (buka dengan browser modern: Chrome, Edge, Firefox).
3. Isi nama dan kelas, lalu klik **Mulai Kuis**.

Tidak diperlukan server web, instalasi, atau koneksi internet.

## Cara Penggunaan

1. **Mulai kuis** — Isi nama lengkap dan kelas, lalu tekan tombol *Mulai Kuis*.
2. **Mengerjakan** — Jawab 10 soal esai pada kolom teks yang tersedia.
3. **Mengirim jawaban** — Tekan *Kirim & Hitung Nilai* untuk menilai seluruh jawaban.
4. **Meninjau** — Setiap soal menampilkan kunci jawaban, kata kunci yang cocok/belum, dan rekomendasi nilai.
5. **Koreksi mandiri** — Jika perlu, ubah skor tiap soal dengan tombol penyesuaian, nilai akhir terhitung ulang otomatis.
6. **Acak ulang** — Tekan *Acak Ulang Soal* untuk menjawab dengan 10 soal baru.

> Catatan: Mode ujian mengaktifkan layar penuh. Meninggalkan tab/browser lebih dari 5 detik akan mengumpulkan kuis secara otomatis.

## Cara Kerja Penilaian

Setiap soal memiliki kata kunci yang diuji pada jawaban siswa:

1. **Kata kunci inti berbobot ganda** — Beberapa konsep penting (contoh: `umpan balik`, `target`, `sensor`, `error`) bernilai 2 poin bobot, sisanya bernilai 1.
2. **Deteksi sinonim** — Kata yang maknanya setara (contoh: `umpan balik`/`feedback`, `target`/`setpoint`) dianggap satu kelompok sehingga tidak dihitung ganda.
3. **Deteksi struktur kalimat** — Jawaban berbentuk kalimat utuh (minimal 5 kata dengan kata hubung) dinilai lebih tinggi daripada sekadar daftar kata.
4. **Deteksi negasi** — Kata kunci yang didahului negasi (`tidak`, `tanpa`, `kurang`, dll.) dianggap pemahaman terbalik dan diberi peringatan.
5. **Konsep "harus tidak ada"** — Untuk soal tentang sistem terbuka, penyebutan `umpan balik` tanpa negasi akan mengurangi skor (penalti).

Skor tiap soal berkisar 0-10, total akhir maksimal 100:

| Total Nilai | Predikat |
|---|---|
| ≥ 70 | LULUS / SANGAT BAIK |
| < 70 | BELUM LULUS / PERLU EVALUASI |

## Struktur Proyek

```
.
├── system kendali kwis.html   # Seluruh aplikasi (HTML, CSS, JavaScript)
└── README.md                  # Dokumentasi ini
```

## Teknologi

- HTML5, CSS3 (murni/style internal)
- JavaScript (vanilla, tanpa library eksternal)

## Kustomisasi

Dokumen soal tersimpan dalam array `questionDatabase` di dalam tag `<script>`. Untuk menambah/mengubah soal, edit bagian tersebut dengan pola berikut:

```js
{
    id: 1,
    question: "Teks pertanyaan...",
    keywords: ["kata", "kunci", "penilaian"],
    absent: ["kata", "yang", "seharusnya", "tidak", "disebut"],  // opsional
    answer: "Kunci jawaban / referensi..."
}
```

Kata kunci inti berbobot ganda dapat disesuaikan pada set `importantKeywords` dan pengelompokan sinonim pada objek `synonymGroups`.

## Lisensi

Proyek ini dibuat untuk keperluan pembelajaran (Telkom University Online Learning). Silakan digunakan dan dimodifikasi bebas untuk keperluan pendidikan.