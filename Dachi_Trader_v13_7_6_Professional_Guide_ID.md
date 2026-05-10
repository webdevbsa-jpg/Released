# Dachi Trader v13.7.6 — Professional Guide, Recommended Settings & XAUUSD Development Roadmap

---

## Executive Summary

Dachi Trader v13.6.1 sampai v13.7.6 bergerak dari EA crossing MA biasa menjadi sistem semi-adaptif yang memiliki:
- filter struktur MA untuk menghindari false cross,
- recovery untuk sinyal yang awalnya terblokir tetapi kemudian terbukti benar,
- konfirmasi Bulls/Bears power,
- pilihan Manual TP target,
- broker/server SL untuk mode touch,
- pengamanan partial close agar tidak salah menghitung lot,
- dokumentasi dan rekomendasi setting per timeframe.

Untuk **XAUUSD M5 dan M15**, EA ini paling cocok dipakai sebagai **trend-pullback scalper / intraday follower**, bukan sebagai grid, martingale, atau counter-news robot. Kekuatan utamanya adalah membaca crossing + struktur MA. Kelemahannya adalah EA masih perlu filter market regime, news/session, dan adaptasi parameter agar lebih stabil pada kondisi emas yang sangat berubah-ubah.

---

## 1. Penjelasan dan Penilaian Simpel Setiap Fitur

### Core Engine

| Fitur | Fungsi Awam | Penilaian Profesional | Status |
|---|---|---|---|
| Fast EMA | Garis cepat untuk menangkap perubahan arah. | Baik untuk scalping, tetapi rawan noise jika berdiri sendiri. | Pakai |
| Slow MA Method | Garis lambat sebagai pembanding trend. | LWMA 20 cepat untuk M1/M5; SMA/EMA lebih halus untuk M15+. | Pakai |
| ATR | Ukuran volatilitas untuk TP, SL, filter jarak. | Wajib untuk XAUUSD karena volatilitas berubah cepat. | Pakai |

### Filter Entry

| Filter | Fungsi Awam | Kelebihan | Kekurangan | Status |
|---|---|---|---|---|
| F0 EMA Gap | Memastikan jarak MA tidak terlalu rapat. | Mengurangi entry saat crossing lemah. | Bisa blok awal trend yang baru lahir. | Pakai |
| F1 HTF EMA100 | Melihat arah besar timeframe lebih tinggi. | Bagus untuk M15/H1 dan market ranging. | Bisa terlambat saat reversal awal. | Optional |
| F7 DI+/DI- | Cek tenaga buyer/seller. | Lebih directional daripada ADX murni. | Bisa lag saat spike cepat. | Optional/Pakai ringan |
| F9 Crossing Distance | Menolak entry yang terlalu jauh dari titik crossing. | Menghindari kejar harga. | Bisa melewatkan breakout kuat. | Pakai |
| F10 MA Structure | Membaca slope, gap, hook-back, weave, compression. | Filter paling penting untuk false cross XAUUSD. | Perlu tuning berbeda per timeframe. | Pakai wajib M5/M15 |
| F11 Recovery | Entry recovery setelah false block. | Menangkap signal yang awalnya terlalu dini diblok. | Jika terlalu agresif bisa entry telat. | Optional |
| F12 Bulls/Bears | Konfirmasi tekanan buyer/seller. | Bagus untuk validasi arah. | Bisa terlalu ketat pada market lambat. | Pakai M5/M15 |
| VR Volatility Regime | Membaca volatilitas tinggi. | Melindungi saat market abnormal. | Bisa mengurangi jumlah trade. | Pakai |
| Switch Proxy | Deteksi choppy via deviasi/ATR. | Membantu M15+. | Kurang cocok dipaksa di M1. | Optional |
| Spread Filter | Blok entry saat spread mahal. | Wajib untuk XAUUSD. | Bisa menolak trade saat news. | Wajib |
| Session Filter | Batasi jam trading. | Mencegah trade di jam sepi. | Perlu cocokkan server time broker. | Pakai |
| Daily Loss / Trail DD | Risk stop harian/sesi. | Melindungi akun dari hari buruk. | Jika terlalu kecil bisa stop terlalu cepat. | Wajib live |

### Exit, TP, SL, dan Partial

| Fitur | Fungsi Awam | Penilaian | Status |
|---|---|---|---|
| Manual TP Target | User memilih TP final, misalnya TP2. | Sangat berguna untuk user yang ingin target jelas. | Pakai |
| Smart TP1 2 Zone | Partial profit antara entry dan TP1. | Lebih realistis daripada 5 zona mikro. | Pakai jika broker lot step mendukung. | Optional |
| Smart TP2 | Partial dari TP1 ke TP2. | Bagus untuk mengunci profit. | Jangan terlalu besar agar sisa posisi tetap meaningful. | Optional |
| Broker SL TOUCH | SL dikirim ke server broker. | Wajib jika ingin S/L muncul dan proteksi lebih cepat. | Pakai untuk TOUCH |
| SL Candle Close | Close hanya jika candle close melewati SL. | Mengurangi wick stop-out. | Tidak ada broker SL; EA harus aktif. | Optional |
| Fast MA Protective Exit | Exit protektif saat harga balik ke fast MA. | Bagus setelah trend sudah melebar. | Bisa exit terlalu cepat jika gap threshold kecil. | Optional |
| Spike SL | Exit saat adverse move ekstrem. | Berguna saat news. | Bisa stop karena wick. | OFF default |
| Circuit Breaker | Emergency exit dan proteksi loss streak. | Wajib untuk live. | Jangan terlalu sensitif. | Pakai |

### Fitur yang Dipensiunkan

| Fitur | Alasan Dipensiunkan |
|---|---|
| F2/F3/F4/F5/F6/F8 | Banyak overlap, lambat, atau membuat keputusan sulit dibaca. |
| Smart SL | Berisiko partial loss saat state tidak sinkron. |
| Late Entry | Berisiko auto-entry dari sinyal lama. |
| Classic Reentry / Retest | Menambah kompleksitas dan potensi overtrade. |

---

## 2. Rekomendasi Filter dan Setting Berdasarkan Timeframe

> Catatan: angka spread/point perlu disesuaikan digit broker. Untuk XAUUSD, forward test broker masing-masing wajib.

### M1 — Scalping Agresif

| Komponen | Rekomendasi |
|---|---|
| Fast/Slow MA | EMA 8 + LWMA 20 |
| F0 | SOFT, ATR-pct 35–45% |
| F1 | OFF |
| F7 | SOFT, margin 4–5 |
| F9 | HARD, max 0.9–1.1 ATR |
| F10 | HARD, slope bars 4–5, min slope 2–3 pt, compression ON |
| F11 | OFF dulu; ON hanya setelah forward-test |
| F12 | SOFT/HARD, min power 0.04–0.05 ATR, max opposite 0.18–0.22 ATR |
| VR | ON, threshold 1.4–1.5, action TIGHTEN |
| Switch Proxy | OFF kecuali sudah diuji |
| Spread | Max 35–45 points atau normal broker |
| Session | London/NY liquid session |
| Daily Loss | ON, ketat |
| Trail DD | ON |
| Manual TP | TP1–TP2, full atau partial kecil |
| SL | TOUCH broker SL untuk proteksi cepat |

### M5 — Scalping Seimbang XAUUSD

| Komponen | Rekomendasi |
|---|---|
| Fast/Slow MA | EMA 8 + LWMA 20 atau SMA 20 |
| F0 | HARD, ATR-pct 45–55% |
| F1 | SOFT/HARD, RequireDirection ON, TF H2/H4 |
| F7 | SOFT, margin 4 |
| F9 | HARD, max 1.1–1.3 ATR |
| F10 | HARD, slope bars 5, min slope 3 pt, slow slope ON, compression ON |
| F11 | ON optional, Only F0 Blocks, recovery 6–8 bars |
| F12 | HARD, period 13, min power 0.05 ATR, max opposite 0.20 ATR |
| VR | ON, threshold 1.5, TIGHTEN |
| Switch Proxy | Optional, AnyTimeframe OFF dulu |
| Spread | Max 45 points atau normal broker |
| Session | London, NY, London/NY overlap |
| Daily Loss | ON |
| Trail DD | ON |
| Manual TP | TP2 full untuk simple mode; TP2 + partial untuk konservatif |
| SL | TOUCH untuk scalping cepat; Candle Close jika ingin tahan wick |

### M15 — Intraday Trend Follower

| Komponen | Rekomendasi |
|---|---|
| Fast/Slow MA | EMA 8 + SMA 20 atau EMA 21 |
| F0 | HARD, ATR-pct 50–65% |
| F1 | HARD, RequireDirection ON, TF H4 |
| F7 | OFF/SOFT, margin 4–5 |
| F9 | HARD, max 1.2–1.5 ATR |
| F10 | HARD, slope bars 5–7, min slope 3–5 pt, compression ON |
| F11 | ON optional, recovery 8–10 bars |
| F12 | HARD, min power 0.05–0.07 ATR, max opposite 0.20 ATR |
| VR | ON, threshold 1.5–1.6, TIGHTEN/PAUSE |
| Switch Proxy | ON, default M15+ |
| Spread | Max 45–60 points |
| Session | London/NY; hindari jam rollover |
| Daily Loss | ON |
| Trail DD | ON |
| Manual TP | TP2/TP3 tergantung volatilitas |
| SL | Candle Close untuk tahan wick; TOUCH jika user ingin proteksi server |

### M30 — Intraday Filtered Mode

| Komponen | Rekomendasi |
|---|---|
| Fast/Slow MA | EMA 8 + EMA 21 atau SMA 20 |
| F0 | HARD, ATR-pct 55–70% |
| F1 | HARD, TF H4/D1, RequireDirection ON |
| F7 | OFF/SOFT |
| F9 | HARD, max 1.3–1.6 ATR |
| F10 | HARD, slope bars 6–8, slow slope ON, compression ON |
| F11 | ON optional, recovery 8–12 bars |
| F12 | HARD, min power 0.06–0.08 ATR |
| VR | ON, threshold 1.6, PAUSE saat news |
| Switch Proxy | ON |
| Spread | Max 60 points atau sesuai broker |
| Session | London/NY only |
| Daily Loss | ON, lebih longgar dari M5 |
| Trail DD | ON |
| Manual TP | TP2/TP3, partial optional |
| SL | Candle Close atau TOUCH sesuai toleransi risiko |

### H1 — Directional Bias / Low Frequency

| Komponen | Rekomendasi |
|---|---|
| Fast/Slow MA | EMA 8 + EMA 21/SMA 20 |
| F0 | HARD, ATR-pct 60–80% |
| F1 | HARD, TF H4/D1 |
| F7 | OFF/SOFT |
| F9 | HARD, max 1.5–2.0 ATR |
| F10 | HARD, slope bars 8–10, slow slope ON |
| F11 | ON optional, recovery 10–14 bars |
| F12 | SOFT/HARD, min power 0.06–0.10 ATR |
| VR | ON, threshold 1.6–1.8 |
| Switch Proxy | ON |
| Spread | Tidak terlalu sensitif, tetapi tetap pakai batas |
| Session | Entry terbaik saat sesi aktif, bukan rollover |
| Daily Loss | ON |
| Trail DD | ON |
| Manual TP | TP2–TP4, partial lebih masuk akal |
| SL | Candle Close untuk mengurangi wick stop-out |

---

## 3. Section Download File

| Item | Link |
|---|---|
| Dachi Trader v13.7.6 EX5 | https://dachi-trader.com/download/Dachi_Trader_v13_7_6.ex5 |
| Catatan | Re-attach EA setelah update karena nama file/version berubah. |
| Rekomendasi sebelum live | Jalankan Strategy Tester dan forward test minimal 1–2 minggu di broker yang sama. |

---

## 4. Fixed Bug List v13.6.1 sampai v13.7.6

| Versi | Fixed Bug / Hardening |
|---|---|
| v13.6.1 | Strategy Tester / Optimizer license bypass agar backtest tidak selalu unauthorized. |
| v13.7.0 | Reverse-close memverifikasi posisi server benar-benar hilang; Hard SL bisa touch/candle-close. |
| v13.7.1 | REV marker tetap digambar sebelum close attempt; Bulls/Bears confirmation ditambahkan. |
| v13.7.2 | TP/SL visual state dibersihkan saat runtime reset; fallback TP/SL dari server position. |
| v13.7.3 | ScanHistory menjadi visual-only; attach tidak memicu LateEntry dari sinyal historis. |
| v13.7.4 | TP1 menjadi 2 subzone; Smart TP partial butuh profit dan arah server sama; Smart SL forced OFF. |
| v13.7.5 | Manual TP target close final di TP pilihan user; Smart TP bisa disuppress saat Manual TP aktif. |
| v13.7.6 | Broker SL untuk TOUCH mode; partial close cek retcode + volume server; total partial dibatasi lot awal. |

---

## 4. Analisa Profesional XAUUSD M5/M15 — Kekurangan EA Saat Ini

Konteks pasar terbaru: laporan World Gold Council 2026 menekankan bahwa emas masih dipengaruhi volatilitas tinggi, risiko geopolitik, demand bank sentral, dan ekspektasi suku bunga. Untuk XAUUSD, kondisi ini membuat M5/M15 sangat sensitif terhadap spike berita, perubahan USD yield, dan liquidity sweep. Artinya EA crossing MA harus punya regime filter, news/session protection, dan adaptive risk.

---

## 5. Roadmap Development Agar Lebih Adaptif dan Profitable di M5/M15

### Prioritas 1 — Market Regime Engine

| Komponen | Bobot Awal | Tujuan |
|---|---:|---|
| ATR short / ATR average | 20% | Deteksi volatilitas normal vs ekstrem. |
| MA slope + gap expansion | 25% | Deteksi trend sehat. |
| Wick/body ratio | 15% | Deteksi rejection atau stop hunt. |
| DI direction / Bulls-Bears | 15% | Konfirmasi tekanan arah. |
| Session + spread | 15% | Hindari jam buruk dan spread abnormal. |
| Distance from HTF level | 10% | Hindari entry tepat di resistance/support besar. |

Output regime:

- **TREND**: izinkan entry normal, TP lebih panjang, runner aktif.
- **RANGE**: entry lebih ketat, TP pendek, manual TP TP1/TP2.
- **SPIKE/NEWS**: pause entry, hanya manage posisi.
- **EXHAUSTION**: hindari entry lanjutan, tunggu pullback/recovery.

### Prioritas 2 — XAUUSD Liquidity & Wick Filter

Tambahkan filter:

- candle wick atas/bawah > 60% range,
- sweep previous high/low 5–20 candle,
- close kembali masuk range,
- spread melebar bersamaan dengan wick.

Jika terdeteksi sweep, entry crossing pertama jangan langsung diambil; tunggu candle konfirmasi berikutnya.

### Prioritas 3 — News Blackout Module

Minimal versi manual:

| Input | Fungsi |
|---|---|
| `InpUseNewsBlackout` | Aktifkan filter news. |
| `InpNewsBeforeMin` | Berapa menit sebelum news entry diblok. |
| `InpNewsAfterMin` | Berapa menit setelah news entry diblok. |
| `InpNewsCloseBefore` | Optional close posisi sebelum news besar. |

Versi lanjut: integrasi kalender ekonomi broker/MQL5 atau endpoint backend.

### Prioritas 4 — Adaptive Exit Profile

| Regime | TP | SL | Exit |
|---|---|---|---|
| Trend | TP2–TP4, partial kecil | SL ATR normal | Runner trail fast MA / ATR |
| Range | TP1–TP2 | SL lebih ketat | Manual TP full, no runner |
| Spike | No new entry | Broker SL wajib | Emergency only |
| Exhaustion | TP pendek | SL konservatif | Exit cepat saat reversal candle |

### Prioritas 5 — Rolling Performance Memory

EA perlu menyimpan statistik sederhana:

- winrate per timeframe,
- winrate per session,
- average MFE/MAE,
- slippage rata-rata,
- spread saat entry,
- filter mana yang paling sering block dan hasil setelah block.

Dari data ini EA bisa memilih preset:

- Conservative,
- Balanced,
- Aggressive,
- News/High Volatility Protection.

---

## 6. Kesimpulan

Untuk XAUUSD M5/M15, arah pengembangan terbaik bukan menambah indikator sebanyak mungkin, tetapi membuat EA **lebih pintar memilih mode**. F10/F11/F12 sudah pondasi bagus untuk false-cross protection. Manual TP dan broker SL membuat eksekusi lebih praktis dan aman. Tahap berikutnya sebaiknya fokus pada:

1. market regime engine,
2. news blackout,
3. liquidity sweep filter,
4. adaptive TP/SL profile,
5. rolling performance memory.
