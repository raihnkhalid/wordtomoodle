# Panduan Format Soal di Word

Dokumen ini menjelaskan cara menulis soal di **Microsoft Word** agar bisa dikonversi otomatis ke Moodle XML menggunakan script converter.

---

## Struktur Dasar Soal

Setiap soal terdiri dari 3 bagian:

```
[NOMOR]. [TEKS SOAL]
[OPSI A-E]
[KUNCI JAWABAN]
```

### Contoh Lengkap

```
1. Apa ibukota Indonesia?
A. Jakarta
B. Bandung
C. Surabaya
D. Medan
E. Yogyakarta
ANS: A
```

---

## 1. Nomor Soal

Format yang didukung:

| Format | Contoh | Status |
|--------|--------|--------|
| Titik | `1. Teks soal...` | Didukung |
| Kurung | `1) Teks soal...` | Didukung |
| Tanpa teks | `1.` (teks di baris berikutnya) | Didukung |

Soal **harus bernomor urut** (1, 2, 3, ...). Nomor digunakan untuk deteksi awal soal baru.

---

## 2. Opsi Jawaban

Format yang didukung:

| Format | Contoh | Status |
|--------|--------|--------|
| Huruf + titik | `A. Jakarta` | Didukung |
| Huruf + kurung | `A) Jakarta` | Didukung |
| Huruf kecil | `a. Jakarta` | Didukung |

Huruf yang dikenali: **A–F** (mendukung hingga 6 opsi).

---

## 3. Kunci Jawaban

### 3a. Single Answer (1 Jawaban Benar)

Tulis setelah opsi terakhir menggunakan salah satu keyword berikut:

```
ANS: A
JAWABAN: A
KUNCI: A
KEY: A
```

Bisa juga ditulis dalam blockquote Word (indented / formatted):
```
> ANS: A
```

### 3b. Multiple Correct Answers (Beberapa Jawaban Benar)

Gunakan separator `/` antara huruf jawaban:

```
ANS: A/B/D
JAWABAN: A/C
KUNCI: B/D/E
```

**Catatan:** Setiap jawaban benar mendapat **100%** (bukan dibagi). Mahasiswa tetap hanya pilih 1 jawaban (radio button), tapi beberapa opsi dianggap benar.

**Contoh penggunaan:**
```
10. Siapa presiden Indonesia pertama?
A. Soekarno
B. Ir. Soekarno
C. Mohammad Hatta
D. Bung Karno
E. Soeharto
ANS: A/B/D
```
Mahasiswa pilih A, B, atau D → benar (100%).

### 3c. Bobot per Opsi — Khusus TKP (BARU)

Untuk soal **TKP (Tes Karakteristik Pribadi)**, tidak ada jawaban benar/salah — setiap opsi punya **bobot skor** berbeda (skala 1–5).

Gunakan keyword `BOBOT:` dengan format `HURUF=SKOR`:

```
BOBOT: A=1 B=2 C=3 D=4 E=5
```

Skor akan dikonversi ke persentase Moodle:

| Skor | Fraction Moodle |
|------|----------------|
| 5 | 100% |
| 4 | 80% |
| 3 | 60% |
| 2 | 40% |
| 1 | 20% |

**Contoh soal TKP:**
```
66. Anda diminta menyelesaikan tugas yang tidak sesuai kompetensi Anda. Apa yang Anda lakukan?
A. Menolak karena bukan bidang saya
B. Menerima tapi menunda pengerjaannya
C. Meminta bantuan rekan yang lebih kompeten
D. Menerima dan berusaha belajar hal baru
E. Menerima dengan antusias dan segera mengerjakan
BOBOT: A=1 B=2 C=3 D=4 E=5
```

**Aturan BOBOT:**
- Gunakan keyword `BOBOT:` (bukan ANS/JAWABAN)
- Format: `HURUF=SKOR` dipisah spasi
- Skor: angka 1–5
- Urutan huruf bebas: `A=3 B=5 C=1 D=4 E=2` valid
- Bisa ditulis dalam blockquote: `> BOBOT: A=1 B=2 C=3 D=4 E=5`

---

## 4. Format Teks yang Didukung

### Bold
```
**teks tebal** → <strong>teks tebal</strong>
```

### Italic
```
*teks miring* → <em>teks miring</em>
```

### Underline
Gunakan fitur underline bawaan Word → otomatis terdeteksi.

### Strikethrough
```
~~teks coret~~ → <del>teks coret</del>
```

### Gambar
Sisipkan gambar langsung di Word. Gambar akan diekstrak otomatis ke folder `media/`.

> **Catatan:** Soal yang mengandung gambar akan diekspor sebagai **placeholder** dan perlu diedit manual di Moodle.

### Rumus Matematika
Gunakan **Equation Editor** bawaan Word. Pandoc akan mengonversi ke format LaTeX yang kompatibel dengan Moodle.

---

## 5. Contoh Soal Lengkap per Tipe

### TWK (Soal 1–33) — Single Answer
```
1. Pancasila sebagai dasar negara tercantum dalam...
A. Pembukaan UUD 1945
B. Batang Tubuh UUD 1945
C. Penjelasan UUD 1945
D. TAP MPR
E. Peraturan Presiden
ANS: A
```

### TIU (Soal 34–65) — Single Answer
```
34. Jika 3x + 7 = 22, maka nilai x adalah...
A. 3
B. 4
C. 5
D. 6
E. 7
ANS: C
```

### TIU — Multiple Correct Answers
```
40. Manakah bilangan prima di bawah ini?
A. 2
B. 4
C. 7
D. 9
E. 11
ANS: A/C/E
```

### TKP (Soal 66–100) — Bobot per Opsi
```
66. Atasan Anda memberikan tugas yang sangat banyak menjelang deadline. Apa yang Anda lakukan?
A. Mengeluh kepada rekan kerja
B. Mengerjakan sebisanya tanpa prioritas
C. Meminta perpanjangan waktu kepada atasan
D. Membuat prioritas dan mengerjakan yang terpenting dulu
E. Mengerjakan semua dengan lembur dan tetap menjaga kualitas
BOBOT: A=1 B=2 C=3 D=4 E=5
```

---

## 6. Tips Penting

1. **Konsistensi format** — Pastikan setiap soal mengikuti pola: nomor → teks → opsi → kunci/bobot.
2. **Satu keyword per soal** — Gunakan `ANS:` ATAU `BOBOT:`, jangan keduanya.
3. **Jangan campur format** — Soal TWK/TIU pakai `ANS:`, soal TKP pakai `BOBOT:`.
4. **Nomor urut** — Pastikan nomor soal berurutan (1, 2, 3, ...) tanpa lompat.
5. **Hindari tabel** — Soal dalam tabel Word bisa diproses tapi hasilnya kurang optimal.
6. **Bold pada kunci** — Tidak masalah jika `ANS:` atau `BOBOT:` ditulis bold di Word, script akan menangani.
7. **Mode SKD** — Saat menjalankan converter, pilih mode grading `2 (SKD)` agar poin TWK/TIU/TKP otomatis terhitung.

---

## 7. Rangkuman Keyword

| Keyword | Kegunaan | Contoh |
|---------|----------|--------|
| `ANS:` | Kunci jawaban (1 atau lebih) | `ANS: A` atau `ANS: A/B/D` |
| `JAWABAN:` | Sama dengan ANS | `JAWABAN: C` |
| `KUNCI:` | Sama dengan ANS | `KUNCI: B` |
| `KEY:` | Sama dengan ANS | `KEY: D` |
| `BOBOT:` | Bobot per opsi (TKP) | `BOBOT: A=1 B=2 C=3 D=4 E=5` |
