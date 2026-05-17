# Dachi Trader v13.9.9 — Panduan Fitur Ringkas

---

## Inti

### Core Engine (selalu aktif)
1. Hitung EMA fast (default 8) dan slow MA (default LWMA20) tiap bar.
2. Deteksi crossing di bar yang baru tutup → trigger BUY (fast cross UP) atau SELL (fast cross DOWN).
3. Hitung ATR (default period 14) sebagai unit ukur SL/TP/threshold filter.

**Setting**: `InpEMA_Fast=8`, `InpSMA_Slow=20`, `InpSlowMA_Method=MODE_LWMA`, `InpATR_Period=14`.

---

## Filter Mode (v13.9.8 NEW)

### Filter Mode
1. **STANDALONE** (default) — setiap filter `F_HARD` yang trigger memblokir signal secara independen. Identik dengan v13.9.7.
2. **SCORING** — filter dengan `Action != F_OFF` ikut voting dengan bobotnya, signal lolos kalau approval ≥ `InpScoring_MinScore` (%).
3. Judge override otomatis disabled saat SCORING aktif (OnInit print warning kalau Judge=ACTIVE).

**Setting**:
```
InpFilterMode       = FM_STANDALONE        // atau FM_SCORING
InpScoring_MinScore = 50.0                 // 0..100 min approval %
InpF0_ScoringWeight  = 10.0
InpF1_ScoringWeight  = 10.0
InpF7_ScoringWeight  = 10.0
InpF9_ScoringWeight  = 10.0
InpF10_ScoringWeight = 10.0
InpF12_ScoringWeight = 10.0
InpF13_ScoringWeight = 20.0                // F13 bobot tertinggi default
InpF14_ScoringWeight = 10.0
InpVR_ScoringWeight  = 0.0                 // operasional, default tidak voting
InpSP_ScoringWeight  = 0.0
InpTDD_ScoringWeight = 0.0
```

---

## Filter Inti (F0–F14)

### F0 — EMA Gap
1. Cek lebar gap EMA fast & slow di SIGNAL bar (bar 1, sudah tutup).
2. Block signal kalau gap < threshold (cross terlalu lemah/dekat).
3. Threshold bisa absolute pts atau persentase ATR.

**Setting**:
```
InpGap_Action     = F_HARD           // F_OFF / F_SOFT / F_HARD
InpGapPoints      = 100              // min gap dalam pts
InpGap_UseATRPct  = false            // true = pakai %ATR ganti pts
InpGap_ATRPct     = 50.0             // % ATR jika UseATRPct=true
```

### F1 — HTF EMA100 Stair-Step
1. Cek apakah HTF EMA100 sudah "melangkah" cukup sejak signal terakhir.
2. Hindari counter-trend di HTF yang masih flat (sideway HTF).
3. Opsional: butuh arah HTF cocok dengan signal (BUY hanya saat HTF EMA100 rising).

**Setting**:
```
InpF1_Action           = F_HARD
InpF1_TF               = PERIOD_H2
InpF1_Period           = 100
InpF1_LookbackBars     = 100
InpF1_StepMinPts       = 5
InpF1_ThresholdPct     = 40           // % avg step needed since last signal
InpF1_RequireDirection = false        // true = BUY butuh HTF naik
```

### F7 — DI+/DI- Validation
1. Konfirmasi arah signal lewat indikator DI+ vs DI- (komponen ADX).
2. BUY butuh `DI+ > DI- + margin`, SELL butuh `DI- > DI+ + margin`.
3. Margin (default 4.0) mencegah signal di kondisi borderline DI.

**Setting**:
```
InpF7_Action = F_HARD
InpF7_Margin = 4.0          // margin DI dalam unit ADX
```

### F9 — Crossing-to-Entry Distance
1. Block signal kalau crossing point sudah terlalu jauh dari current price.
2. Hindari "late entry" setelah trend sudah lari jauh dari MA cross.
3. Distance diukur sebagai kelipatan ATR.

**Setting**:
```
InpF9_Action      = F_HARD
InpF9_MaxDistATR  = 1.5     // max |entry - cross_price| dalam ATR
```

### F10 — MA Slope / Parallel-Drift (Structure)
1. Cek slope fast & slow MA cukup miring (bukan flat-drift).
2. Cek struktur MA bagus (no hook-back, no weave/repeated crosses, no compression).
3. Auto-tune via preset: LOOSE / NORMAL (default) / STRICT / CUSTOM.

**Setting**:
```
InpF10_Action  = F_HARD
InpF10_Preset  = F10_PRESET_NORMAL    // LOOSE / NORMAL / STRICT / CUSTOM

// Saat CUSTOM, knob-knob ini aktif:
InpF10_SlopeBars               = 5
InpF10_MinSlopePts             = 3.0
InpF10_MaxParallelPts          = 1.5
InpF10_UseStructure            = true
InpF10_RequireSlowSlope        = false
InpF10_MinSlowSlopePts         = 1.0
InpF10_MinExpandATR            = 0.03
InpF10_HookBars                = 3
InpF10_HookMaxGapATR           = 0.35
InpF10_WeaveLookbackBars       = 10
InpF10_MaxCrossesInLookback    = 2
InpF10_BlockCompressedDrift    = true
InpF10_CompressLookbackBars    = 6
InpF10_CompressMaxGapATR       = 0.18
InpF10_CompressMaxDeltaPts     = 1.0
```

### F11 — False-Block Recovery Entry
1. Setelah signal di-block, scan N bar berikutnya untuk breakout retest yang mengkonfirmasi arah.
2. Banyak gate keselamatan: F12 pressure, Wick sweep, choppy guard, cross density, Judge score, cooldown.
3. Fire entry sebagai SOFT (TP/SL kecil) supaya recovery tidak over-commit.

**Setting**:
```
InpF11_UseRecovery          = false
InpF11_OnlyF0Blocks         = true     // arm hanya saat F0 yang block
InpF11_RecoveryBars         = 8        // window scan setelah block
InpF11_BreakBufferATR       = 0.10
InpF11_Trigger              = EXIT_ON_CANDLE_CLOSE
InpF11_RequireMAAligned     = true
InpF11_RequireDIDirection   = true
InpF11_EnterAsSoft          = true
InpF11_BlockChoppyRange     = true
InpF11_MaxChoppyAND         = 0.65
InpF11_RequireF12Pressure   = false
InpF11_RequireJudge         = true     // butuh Judge score >= MinJudgeScore
InpF11_MinJudgeScore        = 55.0
InpF11_CooldownBars         = 20       // pause F11 N bar setelah F11 rugi
InpF11_BlockWickSweep       = true
InpF11_CrossDensityLookback = 30
InpF11_MaxCrossDensity      = 5        // > N cross dalam lookback → F11 OFF
```

### F12 — Bulls/Bears Power Confirmation
1. Cek Bulls Power / Bears Power lebih besar dari threshold ATR (ada tekanan searah).
2. Cek pressure lawan tidak terlalu besar (max threshold).
3. Opsional: butuh pressure improving N bar terakhir.

**Setting**:
```
InpF12_Action          = F_HARD
InpF12_Period          = 13
InpF12_MinPowerATR     = 0.05     // pressure searah min (fraction ATR)
InpF12_MaxOppPowerATR  = 0.20     // pressure lawan max
InpF12_RequireImproving= true
InpF12_ImproveBars     = 2
```

### F13 — HTF Running Signal & Exhaustion
1. Cek arah HTF (default H1) cocok dengan signal saat ini.
2. Block kalau gap fast/slow di HTF sudah terlalu lebar (exhaustion) — > `MaxGapATR` × ATR HTF.
3. Cek momentum HTF cukup (slope minimum N bar terakhir).

**Setting**:
```
InpF13_Action          = F_HARD
InpF13_TF              = PERIOD_H1
InpF13_UseClosedHTFBar = true
InpF13_ATRPeriod       = 14
InpF13_CheckExhaustion = true
InpF13_MaxGapATR       = 2.20     // exhaustion threshold
InpF13_MomentumBars    = 2
InpF13_MinSlopePts     = 1.0
InpF13_ReportOnly      = false    // true = log saja, tidak block
```

### F14 — Slow MA Direction (v13.9.7+, v13.9.8 min slope)
1. Cek slow MA bergerak searah signal selama `LookbackBars` (default 3) bar terakhir.
2. **v13.9.8**: opsional minimum |slope| (pts/bar) — block slope tipis di market flat.
3. Filter ringan tanpa banyak sub-condition (komplemen F10).

**Setting**:
```
InpF14_Action       = F_HARD
InpF14_LookbackBars = 3
InpF14_MinSlopePts  = 0.0     // 0 = any direction (v13.9.7 mode)
                              // > 0 = minimum slope pts/bar yang dibutuhkan
```

Contoh `InpF14_MinSlopePts`:
- `0.0` → behavior v13.9.7 (any-direction)
- `1.0` → cukup strict untuk XAUUSD M15
- `3.0` → strict trend (signal lebih jarang, kualitas tinggi)

---

## Judge System (v13.9.0)

### Judge System
1. Gabungkan 6 komponen (momentum/pressure/volatility/candle/distance/HTF) jadi skor 0–100.
2. Mode OFF / REPORT_ONLY (dashboard saja) / ACTIVE (boleh override F0/F13).
3. Skor ≥ `UpperThr` (default 70) → demote HARD block jadi SOFT (atau VALID). Skor ≤ `LowerThr` (default 40) → confirm block, F11 tidak boleh arm.

**Setting**:
```
InpJudge_Mode          = JUDGE_OFF      // OFF / REPORT_ONLY / ACTIVE
InpJudge_UpperThr      = 70.0
InpJudge_LowerThr      = 40.0
InpJudge_OverrideF0    = true
InpJudge_OverrideF13   = false
InpJudge_OverrideAsSoft= true
InpJudge_W_Momentum    = 25.0
InpJudge_W_Pressure    = 15.0
InpJudge_W_Volatility  = 15.0
InpJudge_W_Candle      = 15.0
InpJudge_W_Distance    = 15.0
InpJudge_W_HTF         = 15.0
```

**Catatan v13.9.8**: kalau `InpFilterMode=FM_SCORING`, Judge override otomatis disabled (warning di OnInit). Set `InpJudge_Mode=OFF` atau `REPORT_ONLY` saat pakai SCORING.

---

## Wick / Liquidity Sweep Detector

### Wick Detector
1. Scan N bar terakhir untuk previous swing high/low.
2. Deteksi bar sweep — wick menembus level itu lalu close balik (liquidity grab).
3. Output: `bad_sweep` (sweep melawan arah signal → warning) / `good_sweep` (sweep searah → bonus Judge).

**Setting**:
```
InpWick_UseFilter   = false
InpWick_SweepLookback = 10
InpWick_MinWickRatio = 0.55     // wick/range ratio jadi "dominant wick"
InpWick_ConfirmBars  = 1
```

---

## Market Guard

### Volatility Regime (VR)
1. Bandingkan ATR current vs rata-rata ATR jangka panjang.
2. Saat ratio > threshold (default 1.5×) → market sedang expansion.
3. Action: TIGHTEN (SL/TP lebih ketat) atau PAUSE (block entry).

**Setting**:
```
InpUseVolRegime    = false
InpVR_ATR_Period   = 14
InpVR_ATR_AvgPeriod= 50
InpVR_HighThreshold= 1.5
InpVR_Action       = VR_TIGHTEN    // VR_TIGHTEN / VR_PAUSE
```

### Switch Proxy (SP)
1. Hitung stddev/ATR — ratio rendah = market choppy (sideway).
2. Otomatis aktif di M15+ (atau semua TF kalau `InpSwitchProxy_AnyTimeframe=true`).
3. Saat choppy → mark signal sebagai SOFT (TP/SL kecil).

**Setting**:
```
InpUseSwitchProxy          = false
InpSwitchProxy_AnyTimeframe= false
InpSP_StddevPeriod         = 20
InpSP_HighAND              = 0.7
InpSP_LowAND               = 0.4
```

### Trailing Drawdown Circuit Breaker
1. Track peak equity sejak EA jalan.
2. Block entry baru kalau equity drop > `InpTrailDD_Pct` % dari peak.
3. Reset peak setiap kali equity bikin high baru.

**Setting**:
```
InpUseTrailDD   = false
InpTrailDD_Pct  = 5.0       // % drawdown dari peak
```

### Circuit Breaker (DD + loss streak + spread)
1. Block entry kalau drawdown current trade > `InpCB_DrawdownATR` × ATR.
2. Block kalau N kali rugi berturut-turut (`InpCB_ConsecLoss`).
3. Block kalau spread > `InpCB_SpreadMax`.

**Setting**:
```
InpUseCB         = false
InpCB_DrawdownATR= 3.0
InpCB_ConsecLoss = 3
InpCB_UseVolume  = true
InpCB_UseMomentum= true
InpCB_MomBars    = 2
InpCB_UseSpread  = true
InpCB_SpreadMax  = 60
```

### Daily Loss / Daily Profit Stop
1. Track P/L harian (sejak 00:00 server time).
2. `InpUseDailyLoss=true` → block entry kalau total loss harian ≥ `InpDailyLossLimit`.
3. `InpUseDailyProfitStop=true` → block entry kalau total profit harian ≥ `InpDailyProfitTarget` (kunci profit).

**Setting**:
```
InpUseDailyLoss        = false
InpDailyLossLimit      = 50.0
InpUseDailyProfitStop  = false
InpDailyProfitTarget   = 50.0
```

Tampil di chart sebagai marker `? DAILY` saat skip entry karena limit hit.

### Session Filter
1. Restrict entry ke jam tertentu (server time).
2. Restrict ke hari tertentu (Mon..Sun toggles).
3. Tampil sebagai `? SESSION` saat skip karena di luar window.

**Setting**:
```
InpUseSession   = false
InpSessionStart = 8        // jam mulai
InpSessionEnd   = 22       // jam selesai
InpSessionMon..Sun = false // tambah filter per hari kalau dibutuhkan
```

### Spread Guard
1. Block entry kalau spread current > `InpMax_Spread` pts.
2. Tampil sebagai `? SPREAD` di chart saat skip.
3. Slippage saat order: `InpEASlippage` pts (default 30).

**Setting**:
```
InpMax_Spread = 45
InpEASlippage = 30
```

---

## Exit System

### Take Profit (default 2-step)
1. TP1 = entry ± `InpTP1_Mult` × ATR (default 0.75×).
2. TP2 = TP1 ± `InpTP1_to_TP2_Mult` × ATR (default 0.75× → 1.5× total).
3. TP3+ = step `InpTP_Step_Mult` × ATR per level (sampai MAX_TP=30 level).

**Setting**:
```
InpTP1_Mult        = 0.75
InpTP1_to_TP2_Mult = 0.75
InpTP_Step_Mult    = 1.0
```

### Stop Loss
1. SL = entry ∓ `InpSL_Mult` × ATR.
2. Trigger: TOUCH (langsung saat harga sentuh) atau CANDLE_CLOSE (tunggu close bar).
3. Force-on saat signal SOFT (filter SOFT atau Judge override).

**Setting**:
```
InpUseSL              = false
InpSL_Mult            = 1.25
InpSL_HardlineTrigger = EXIT_ON_TOUCH      // atau EXIT_ON_CANDLE_CLOSE
```

### Manual TP Target Exit
1. Pilih TP level mana yang full-close (default TP2).
2. Opsional pakai Smart TP partials sebelum target.
3. Memudahkan setting "close all di TPn".

**Setting**:
```
InpManualTP_Enable           = false
InpManualTP_Target           = 2          // 1..30
InpManualTP_UsePartialSystem = false
```

### Smart TP (partial close system)
1. Close 30% (default) di TP1, 30% di TP2.
2. Sisanya runner pakai trailing.
3. TP3+ optional partial close on reversal candle.

**Setting**:
```
InpUseSmartTP        = false
InpSTP1_UseSubZones  = false
InpSTP2_UseSubZones  = false
InpSTP3_UsePartial   = false
InpSTP1_Pct          = 30
InpSTP2_Pct          = 30
```

### Progressive Exit (v13.9.4 + v13.9.5)
1. **Phase 0**: N bar pertama setelah entry (default 4), exit level = fast EMA digeser `Phase0BufferATR × ATR` (grace period).
2. **Phase 1**: setelah Phase 0 habis, exit kalau harga touch/close di fast EMA.
3. **Phase 2**: setelah TPn (default TP2) tercapai, exit di BEP (lock entry price).

**Setting**:
```
InpUsePE             = false
InpPE_Trigger        = EXIT_ON_TOUCH    // atau EXIT_ON_CANDLE_CLOSE
InpPE_BEPAfterTP     = 2                // TP level yang arm BEP lock
InpPE_Phase0Bars     = 4
InpPE_Phase0BufferATR= 0.5
```

### Fast MA Protective Exit
1. Aktif setelah expansion gap MA cukup besar (`MinGapATR`).
2. Exit kalau harga balik touch fast MA (akhir trend).
3. Pakai arm bar delay untuk hindari exit prematur.

**Setting**:
```
InpUseEarlyExit      = false
InpEarlyExit_MinGapATR= 1.0
InpEarlyExit_Trigger = EXIT_ON_TOUCH
InpEarlyExit_ArmBars = 1
```

### Adaptive Reversal Exit
1. Track peak price sejak entry.
2. Exit kalau pullback dari peak > `PullbackATR` × ATR.
3. Lookback `FastBars` (default 3) untuk konfirmasi reversal.

**Setting**:
```
InpUseAdaptiveReversal= false
InpAdapt_PullbackATR  = 1.5
InpAdapt_FastBars     = 3
```

### Spike SL
1. Detect adverse spike di forming bar (bar yang belum tutup).
2. Exit kalau adverse move ≥ `Spike_ATR_Mult` × entry-ATR.
3. Lindungi dari news spike / volatility burst.

**Setting**:
```
InpUseSpikeSL    = false
InpSpike_ATR_Mult= 2.0
```

### Soft Mode TP/SL
1. Aktif saat signal classification SOFT (filter F_SOFT trigger atau Judge override-as-soft).
2. TP1 lebih kecil, TP2 lebih dekat — quick-grab profit.
3. SL forced ON walau `InpUseSL=false` (proteksi wajib saat signal lemah).

**Setting**:
```
InpSoft_TP1_Mult = 0.4
InpSoft_TP2_Mult = 0.4
InpSoft_SL_Mult  = 0.75
```

---

## Order & Akun

### EA Trading
1. `InpIndicatorOnly=true` → EA hanya gambar signal di chart, tidak buka order.
2. `InpAutoLot=true` → lot dihitung otomatis dari balance / `InpAutoLotDivider`.
3. `InpManualLot` jadi fallback lot saat AutoLot=false.

**Setting**:
```
InpIndicatorOnly = false
InpAutoLot       = false
InpManualLot     = 0.01
InpAutoLotDivider= 20000      // contoh: balance $2000 → lot 0.10
InpEAMagic       = 202603     // magic number untuk EA ini
```

### Display
1. Dashboard di pojok kiri bawah (toggle dengan button PANEL).
2. Warna candle BUY/SELL signal customizable.
3. Background chart hitam default (override warna built-in MT5).

**Setting**:
```
InpBuyColor   = clrLime
InpSellColor  = clrRed
InpEntryColor = clrDodgerBlue
```

### Alerts
1. Sound alert tiap signal valid.
2. Push notification ke mobile MT5 (butuh setup di Tools → Options → Notifications).
3. Popup alert window.

**Setting**:
```
InpAlertSound = true
InpAlertPush  = false
InpAlertPopup = true
```

---

## Quick Start Preset

Untuk yang ingin coba cepat tanpa baca semua di atas:

### Preset A: Konservatif (sedikit signal, kualitas tinggi)
```
InpFilterMode  = FM_STANDALONE
InpGap_Action  = F_HARD;  InpGapPoints       = 150
InpF10_Action  = F_HARD;  InpF10_Preset      = F10_PRESET_STRICT
InpF13_Action  = F_HARD;  InpF13_MaxGapATR   = 2.0
InpF14_Action  = F_HARD;  InpF14_MinSlopePts = 2.0
InpUseSL       = true;    InpSL_Mult         = 1.25
InpUsePE       = true     // Progressive Exit
```

### Preset B: Balanced (default-ish)
```
InpFilterMode  = FM_STANDALONE
InpGap_Action  = F_HARD;  InpGapPoints       = 100
InpF10_Action  = F_HARD;  InpF10_Preset      = F10_PRESET_NORMAL
InpF13_Action  = F_HARD;  InpF13_ReportOnly  = false
InpF14_Action  = F_SOFT;  InpF14_MinSlopePts = 0.5
InpJudge_Mode  = JUDGE_REPORT_ONLY     // observasi dulu
```

### Preset C: Ensemble Voting (v13.9.8 SCORING)
```
InpFilterMode       = FM_SCORING
InpScoring_MinScore = 60          // butuh majority voting
InpGap_Action  = F_HARD            // Action tetap diset; di SCORING semua jadi voter
InpF10_Action  = F_HARD;  InpF10_Preset = F10_PRESET_NORMAL
InpF13_Action  = F_HARD;
InpF14_Action  = F_HARD;  InpF14_MinSlopePts = 1.0
InpJudge_Mode  = JUDGE_OFF         // wajib OFF/REPORT_ONLY di SCORING
```

---

## Section Download File

| Item | Link |
|---|---|
| Dachi Trader v13.9.9 EA | https://dachi-trader.com/download/Dachi_Trader_v13_9_9.ex5 |
| Dachi Trader v13.9.9 Preset | https://dachi-trader.com/download/dachi_13_9_9_preset.set |
| Catatan | Re-attach EA setelah update karena nama file/version berubah. |
| Rekomendasi sebelum live | Jalankan Strategy Tester dan forward test minimal 1–2 minggu di broker yang sama. |

---
