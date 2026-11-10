# CAP-AutoBank — Sistem Otomasi Analisis Rekening Koran untuk Relationship Manager (RM)

Aplikasi berbasis web modern yang dirancang khusus untuk membantu **Relationship Manager (RM)**, **Credit Analyst**, dan **Komite Kredit** di perbankan dalam menganalisis mutasi rekening koran calon debitur secara otomatis untuk penyusunan **Credit Approval Package (CAP) / Nota Analisis Kredit (NAK)**.

---

## 🌟 Fitur Utama

1. **Multi-Input Rekening Koran Fleksibel**:
   - Upload file **Excel (.xlsx, .xls)** & **CSV** (mendukung format e-Statement BCA, Bank Mandiri, BRI, BNI, CIMB Niaga, dll.).
   - Fitur **Copy-Paste** langsung dari tabel Excel atau e-Statement.
   - Dilengkapi **Template Excel Standar** yang dapat diunduh langsung untuk nasabah/RM.

2. **Perhitungan Rasio Keuangan & Perbankan Otomatis (Instant Generation)**:
   - **Debit to Credit Ratio (D/C Ratio)**: Mengukur rasio pengeluaran terhadap omset masuk & deteksi *cash burning / defisit kas*.
   - **ADB to Turnover Ratio**: Mengukur persentase Saldo Rata-rata Harian (*Average Daily Balance*) terhadap turnover bulanan guna mendeteksi rekening operasional vs rekening transit (*pass-through*).
   - **Cash Buffer / Liquidity Days**: Menghitung berapa hari operasional perusahaan dapat bertahan jika terjadi penundaan pembayaran dari debitur/buyer.
   - **Pass-Through Fund Ratio**: Mendeteksi pola dana masuk besar yang langsung ditarik keluar kembali dalam tempo < 48 jam (indikasi rekayasa omzet / rekening numpang lewat).
   - **Month-End Spike / Window Dressing Index**: Mendeteksi suntikan dana abnormal di 4 hari terakhir bulan kalender untuk memoles saldo laporan keuangan.
   - **Aktivitas & Frekuensi Transaksi**: Menguji apakah rekening tersebut merupakan rekening operasional primer (*main operating account*).

3. **Early Warning System (EWS) & Red Flags Detection**:
   - Deteksi otomatis warkat **Tolakan Kliring / Cek Bilyet Giro Kosong (SKNBI)**.
   - Deteksi **Cerukan / Overdraft** saldo minus tidak sah.
   - Deteksi saldo kritis (*near-zero balance*).
   - Panduan mitigasi risiko spesifik yang wajib dilampirkan RM ke Komite Kredit.

4. **Kalkulator Plafon Kredit Modal Kerja (KMK)**:
   - Menggunakan **Turnover Method** perbankan berdasarkan *Cash Conversion Cycle (CCC)* dan porsi *Bank Sharing (70%)*.
   - Perhitungan otomatis estimasi beban bunga bulanan & **Debt Service Ratio (DSR / IIR)**.
   - Simulasi interaktif slider plafon, siklus kas, suku bunga, dan tenor.

5. **Laporan & Export Siap Pakai**:
   - **Export Rekapitulasi Lengkap ke Excel (.xlsx)** dengan 3 sheet (Ringkasan Debitur & Rasio, Rekapitulasi Bulanan, Data Mutasi Transaksi).
   - **Cetak Memo CAP / Print PDF** resmi berformat memorandum komite kredit dengan kolom tanda tangan RM, Reviewer/TL, dan Branch Manager.
   - **Preset Contoh Nyata**:
     - *PT Sumber Pangan Lestari* (Contoh debitur sehat / Layak KMK Rp 3 Miliar)
     - *CV Mega Konstruksi Nusantara* (Contoh berisiko tinggi / Ada tolakan kliring & window dressing)

---

## 🚀 Cara Menjalankan Aplikasi

Aplikasi telah aktif di background. Anda dapat membukanya langsung di browser:
- **URL Lokal**: `http://localhost:5173/`

Untuk menjalankan secara manual di terminal:
```bash
# 1. Masuk ke direktori
cd "c:\Users\ai.department\Documents\akmal\project otomasi CAP"

# 2. Jalankan development server
npm run dev
```

---

## 📊 Matriks & Benchmark Rasio Perbankan

| No | Nama Rasio | Formula Standar Bank | Benchmark Sehat | Indikasi Bahaya |
|---|---|---|---|---|
| 1 | **Debit to Credit Ratio** | `(Total Debit / Total Kredit) × 100%` | `< 92%` | `> 100%` (Defisit Kas / Cash Bleeding) |
| 2 | **ADB to Turnover Ratio** | `(Average Daily Balance / Inflow Bulanan) × 100%` | `> 8.0%` | `< 3.0%` (Rekening Transit / Tidak Mengendap) |
| 3 | **Cash Buffer Days** | `ADB / Rata-rata Pengeluaran Debit Harian` | `≥ 7 Hari` | `< 4 Hari` (Likuiditas Kritis / Rentan Default) |
| 4 | **Pass-Through Ratio** | `(Inflow Keluar < 48 Jam / Total Inflow) × 100%` | `< 15%` | `> 30%` (Rekayasa Perputaran Omzet) |
| 5 | **Window Dressing Index** | `(Inflow Tgl 27-Akhir Bln / Total Inflow) × 100%` | `< 25%` | `> 35%` (Poles Saldo Akhir Bulan) |
| 6 | **Frekuensi Transaksi** | `Total Jumlah Mutasi / Jumlah Bulan` | `> 30 Tx/Bln` | `< 10 Tx/Bln` (Rekening Pasif / Sekunder) |
