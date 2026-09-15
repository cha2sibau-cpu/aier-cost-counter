# AIER Pricing Package — Context Summary
*Disusun 15 September 2026 · Direvisi 15 September 2026 — disinkronkan dengan kalkulator internal (`index.html`)*

> **Status angka:** semua angka di dokumen ini diverifikasi langsung terhadap engine kalkulator
> (skenario **average**, **Hires = 0**, margin 25%, pembulatan harga Rp10.000). Kalau angka di sini
> dan di kalkulator berbeda, **kalkulator yang benar** — dokumen ini yang harus dikoreksi.

## Latar Belakang
AIER adalah lini layanan produksi gambar berbasis AI dari HIRA Imaji, diluncurkan sebagai brand terpisah (bukan di bawah nama HIRA) untuk menghindari konflik model bisnis: HIRA berbasis boutique/performa produksi, AIER berbasis multiplier (1 shoot/prompt → banyak output, bayar per deliverable). Nama AIER adalah akronim penghormatan ke co-author proposal (Arza, Iqmal, Edna, Rachel).

Kampanye rekrutmen 3 pilot brand (unpaid) berjalan 12–30 September 2026, lewat Threads (kredibilitas publik), LinkedIn DM (Plan A outreach), Instagram (portfolio visual). Infrastruktur kampanye (jadwal 12-post Threads, one-pager, template outreach 3 sender, daftar 187 prospek) sudah dibangun. Paket harga ini rencananya ditunjukkan ke 3 pilot brand **setelah** proyek pilot (yang unpaid) mereka selesai.

## Model Cost (tervalidasi via kalkulator internal)
Base formula: **Cost(N) = Biaya Kreatif(N) + Rp779.300 × N (variable, prompting/generation)**

- **Variable (Prompting Day)** = Rp779.300 per visual, konstan di semua volume. Terdiri dari machine Rp429.300 (300 generates × Rp1.431/generate) + labor Rp350.000 (7 jam × Rp50.000).
- **Biaya Kreatif** (Creative Conception + Concept Revision) di kalkulator lama di-cap "maks 10 image/paket" — begitu N > 10, kalkulator re-charge biaya kreatif penuh (Rp1.313.138) tiap kelipatan 10. Ini bikin masalah **cliff**: nambah 1 gambar dari N=10 ke N=11 bikin cost melompat Rp2.092.438 (sama kayak charge 1 paket baru dari nol) — nggak masuk akal secara produksi kalau riset diulang total gara-gara nambah 1 gambar.
- **Solusi yang dipilih** (sudah diimplementasikan di kalkulator): biaya kreatif di-scale pakai akar (√) dari rasio volume, bukan re-charge penuh tiap 10:
  **Biaya Kreatif(N) = Biaya Kreatif @ N basis × √(N / N basis)**, dengan N basis = 10 → Rp1.313.138 × √(N/10).
  Logikanya: makin banyak gambar, riset/eksplorasi emang perlu lebih banyak (sesuai insting Arza), tapi nggak linear 1:1 sama volume — ada diminishing returns. Setelah perubahan ini, N=10 → 11 cuma naik **Rp843.393** (Rp779.300 variable + Rp64.093 tambahan kreatif), bukan Rp2.092.438.
  Ini **asumsi pemodelan**, bukan angka tervalidasi dari data riil — perlu dikalibrasi ulang begitu ada data riil dari pilot soal berapa jam riset yang kepake di volume besar.
- Angka Rp1.313.138 **bukan konstanta hardcoded** di kalkulator — dia turunan dari rate engine, jam kerja, dan hourly rate di panel konfigurasi. Kalau salah satu parameter itu diubah, basis √ ikut bergeser.
- Labor cost basis: Rp50.000/jam
- **Catatan buffer generation**: formula variable ini pakai asumsi buffer tinggi, yaitu **300 generates per image** (range 200–400 di kalkulator, worst-case). Realitanya bervariasi jauh — kadang cuma ~3x generate + touch-up manual cukup, kadang jauh lebih banyak. Rata-rata real belum ada datanya — perlu ditrack selama pilot berjalan. Kalau nanti datanya keluar, cost bisa jauh lebih rendah dari estimasi ini (berpotensi naikin margin atau nurunin harga jual).

### Formula harga jual
**Harga = Cost ÷ (1 − margin)**, margin 25% → Harga = Cost ÷ 0,75. Ini *margin on price*, bukan markup.
Harga dibulatkan ke **kelipatan Rp10.000 terdekat**. (Kalkulator lama pakai "buffer ×1,5" yang setara margin 33,3% — sudah diganti.)

## Struktur Produk
> Struktur ini hidup di landing page & materi promosi, bukan di kalkulator. Kalkulator hanya menghitung cost + harga untuk satu skenario sekali jalan.

**A. One-off / Per-Project** — dua opsi:
  1. **Paket (Campaign scope)** — ladder tier di bawah, termasuk arahan kreatif AIER (Creative Conception + Concept Revision), biaya kreatif di-scale √ ke seluruh paket
  2. **Per-visual (ad hoc, tanpa arahan kreatif)** — klien wajib kasih brief/referensi visual sendiri, jadi AIER beneran skip proses kreatifnya. Harga **Rp1.040.000/image** (cost Rp779.300, margin 25%), berlaku di volume berapa pun. Ini yang jadi gate resminya: tanpa brief/referensi dari klien, pesanan otomatis masuk skema Campaign (dengan arahan kreatif).

**B. Retainer** — komitmen bulanan, mulai dari tier Plus ke atas (Starter dikecualikan, volumenya terlalu kecil buat sinyal kebutuhan recurring).

Photoshoot: **opsional**, add-on terpisah di semua tier (bukan dibundling ke tier tertentu — keputusan awal "Opsi A" sudah direvisi).

## Ladder Harga One-off (AI-only, margin 25%)

| Tier | Output | Faktor √ | Biaya Kreatif | Variable | Total Cost | Harga (margin 25%) | Harga/image |
|---|---|---|---|---|---|---|---|
| Starter | 10 | ×1,00 | Rp1.313.138 | Rp7.793.000 | Rp9.106.138 | Rp12.140.000 | Rp1.214.000 |
| Plus | 25 | ×1,58 | Rp2.076.253 | Rp19.482.500 | Rp21.558.753 | Rp28.750.000 | Rp1.150.000 |
| Pro | 50 | ×2,24 | Rp2.936.265 | Rp38.965.000 | Rp41.901.265 | Rp55.870.000 | Rp1.117.400 |
| Max | 100 | ×3,16 | Rp4.152.505 | Rp77.930.000 | Rp82.082.505 | Rp109.440.000 | Rp1.094.400 |

Ladder di atas **belum termasuk upscale** (semua tier diasumsikan Hires = 0). Upscale adalah add-on per image, lihat bagian Add-on.

Harga per gambar konsisten turun tiap naik tier — nggak ada cliff kayak model "full recharge tiap 10" sebelumnya (di situ Plus jadi Rp1.249.000/img, malah lebih mahal dari Starter Rp1.214.000/img, yang melanggar logika ladder).

Posisi harga ini jatuh di antara freelancer multishot (Rp600rb–1,5jt) dan agency dengan art direction (Rp1,5–5jt) — sesuai positioning yang dituju.

*(Ladder harga awal — Starter Rp5jt/Plus Rp8,5jt/Pro Rp15jt/Max Rp25jt — sudah DITOLAK karena di bawah cost produksi di semua tier dan jatuh ke harga freelancer.)*

## Per-visual vs Campaign — Perbandingan
Karena biaya kreatif sekarang di-scale pakai √ (bukan flat), selisih antara Campaign dan (N × Per-visual) **nggak lagi konstan** — mengecil makin tinggi tier:

| Tier | Campaign | N × Per-visual (Rp1.040.000/img) | Selisih | Selisih % |
|---|---|---|---|---|
| Starter | Rp12.140.000 | Rp10.400.000 | Rp1.740.000 | 16,7% |
| Plus | Rp28.750.000 | Rp26.000.000 | Rp2.750.000 | 10,6% |
| Pro | Rp55.870.000 | Rp52.000.000 | Rp3.870.000 | 7,4% |
| Max | Rp109.440.000 | Rp104.000.000 | Rp5.440.000 | 5,2% |

- **Campaign** = paket + arahan kreatif dari AIER
- **Per-visual** = gambar aja, klien bawa brief/referensi sendiri (AIER skip proses kreatif) — **Rp1.040.000/image**, gate wajib: brief/referensi visual dari klien. Tanpa gate ini, Per-visual selalu lebih murah dari Campaign di volume yang sama.
- Premium Campaign vs Per-visual paling tipis di tier Max (5,2%) — worth diawasin kalau nanti mau ngelonggarin gate brief, karena makin tipis selisihnya, makin kecil insentif klien besar buat ambil paket dengan arahan kreatif.

**Cek terhadap dua goal utama pricing AIER:**
1. *Paket mesti lebih murah tiap naik tier* ✅ — ladder Campaign konsisten turun (lihat tabel Ladder Harga di atas), nggak ada cliff.
2. *Retainer mesti lebih murah dari one-off* ✅ — otomatis terpenuhi selama diskon retainer > 0%, independen dari model scaling biaya kreatif (lihat bagian Retainer di bawah).

## Add-on
- **Photoshoot**: cost 8 jam ~Rp15.000.000 → harga jual (margin 25%) **Rp20.000.000**. Cost 4 jam **belum ada angka pasti** — perlu dicek apakah ada minimum charge yang bikin 4 jam nggak sesederhana setengah dari 8 jam. *(Tidak dimodelkan di kalkulator — angka manual.)*
- **Upscale** (khusus print jarak dekat/skala besar, ~10 jam kerja): cost **Rp3.884.000/image** → harga jual (margin 25%) **Rp5.180.000/image**. Tidak diperlukan untuk billboard/viewing jarak jauh.
  Cost-nya = machine Rp3.384.000 (200 generates × Rp16.920) + labor Rp500.000 (10 jam). *Revisi: angka Rp3.800.000 / harga Rp5.070.000 di versi sebelumnya adalah pembulatan yang keliru — kalkulator yang benar.*

## Retainer — Analisis Diskon
Formula: margin sisa = 1 − (1 − margin dasar)/(1 − diskon). Karena margin dasar 25%, kalau diskon retainer = 25% juga, margin otomatis jadi **0% (breakeven persis)** — berlaku di semua tier, bukan soal angka spesifik per tier.

| Komitmen | Diskon | Margin Sisa |
|---|---|---|
| 3 bulan | 10% | 16,7% (sehat) |
| 6 bulan | 15% (alternatif) | 11,8% |
| 6 bulan | 18% (alternatif) | 8,5% |
| 6 bulan | 25% (usulan awal) | **0% — breakeven, belum diputuskan apakah ini disengaja sebagai loss-leader atau perlu diturunkan** |

Harga retainer 3-bulan (diskon 10%, dibulatkan ke Rp10.000) per tier:
| Tier | One-off | Retainer 3-bulan (10% off) |
|---|---|---|
| Plus | Rp28.750.000 | Rp25.880.000/bln |
| Pro | Rp55.870.000 | Rp50.280.000/bln |
| Max | Rp109.440.000 | Rp98.500.000/bln |

## Parameter Kalkulator (referensi)
Nilai default di `index.html` yang menghasilkan semua angka di atas:

| Parameter | Nilai |
|---|---|
| USD → IDR | 18.000 |
| Base hourly rate | Rp50.000/jam |
| Margin | 25% (harga = cost ÷ 0,75) |
| Pembulatan harga | Rp10.000 |
| Volume acuan biaya kreatif (N basis) | 10 |
| Rate generating (max of mean/median 8 engine) | $0,0795 → Rp1.431/generate |
| Rate upscaling (max of mean/median 2 engine) | $0,94 → Rp16.920/generate |

Fase (skenario average): Creative Conception 175 gen / 7 jam / ×1,25 · Concept Revision 88 gen / 10 jam · Prompting Day 300 gen / 7 jam · Touch Up/Upscale 200 gen / 10 jam.

## Open Questions untuk Chat Berikutnya
1. Diskon retainer 6-bulan: turunkan ke 15-18%, atau tetap 25% sebagai loss-leader yang disengaja?
2. Cost real photoshoot 4 jam (belum ada angka)
3. Data rata-rata generation real per image (pending, dikumpulkan selama pilot)
4. Definisi deliverable/resolusi final: apakah AIER ikut konvensi HIRA (kirim master besar, klien crop sendiri) atau bikin skema beda karena butuh upscale ekstra ke 7000px+
5. Perilaku N < 10: √ scaling bikin biaya kreatif jatuh di volume kecil (N=1 → cuma ~Rp415.000, 32% dari riset penuh). Untuk sekarang dibiarkan; **direview setelah pilot** — apakah perlu lantai minimum biaya kreatif.
6. Eksponen √ (0,5) masih asumsi. Kalibrasi ulang pakai data jam riset riil dari pilot.
7. Pembulatan: harga paket dibulatkan Rp10.000, yang bikin per-visual jadi Rp1.040.000 (bukan Rp1.039.000 kalau dibulatkan Rp1.000). Perlu diputuskan apakah per-visual pakai aturan pembulatan sendiri.
