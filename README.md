# DP-Week2-Task2-5224600054-Kindi-Asyari

## Step 1 — Write the Core Loop

Game: **Card Run** — a poker-hand scoring card game with rounds, blinds, modifiers, and a shop system.

### Core Loop

1. Player draws 8 cards from the shuffled deck
2. Player selects up to 5 cards from hand
3. Player chooses action: Play Hand or Discard
4. If Play Hand → System evaluates poker combination (e.g. Flush, Full House, Pair)
5. Base chips and multiplier are determined from the combination
6. Card chips from scoring cards are added to base chips
7. Modifiers (from shop inventory) are applied to chips and mult
8. Final score is calculated: (chips × mult) and added to accumulated score
9. If Discard → selected cards are removed, remaining returned; discard chance decremented
10. Check if accumulated score ≥ target blind score → session cleared
11. Check if plays remaining = 0 or deck empty → Game Over
12. After clearing all 3 blinds (Small, High, Boss) → earn currency bonus, open Shop
13. Player buys/sells modifiers in Shop using currency
14. Advance to next round with higher blind targets
15. Repeat from step 1 until all 5 rounds cleared (Win) or Game Over

## Step 2 — Identify the Invariants

Bagian-bagian berikut merupakan **core loop** yang **tidak boleh berubah** karena merupakan kerangka struktural permainan:

- **Urutan draw → select → action → evaluate → score → check** — Ini adalah alur utama setiap giliran. Mengubah urutan ini akan merusak logika dasar permainan.
- **Siklus Blind per Ronde (Small → High → Boss)** — Setiap ronde selalu terdiri dari 3 sesi blind berurutan. Struktur ini menjamin eskalasi tantangan yang konsisten.
- **Pengecekan kondisi menang/kalah** — Sistem harus selalu mengecek apakah skor target tercapai atau kesempatan habis. Tanpa ini, game tidak memiliki akhir.
- **Shop dibuka setelah menyelesaikan blind** — Shop hanya muncul di setelah blind selesai. Ini menjaga ritme gameplay.
- **Scoring = (chips × mult)** — Formula dasar ini adalah inti dari sistem skor. Modifier boleh mengubah nilai chips dan mult, tapi formula akhirnya tetap perkalian.

## Step 3 — Identify Mutable Elements

Bagian-bagian berikut adalah **mekanik, parameter, dan konten** yang bisa diubah tanpa merusak core loop:

- **Jumlah kartu yang di-draw** (saat ini 8) — bisa diubah untuk menyesuaikan tingkat kesulitan.
- **Target skor tiap blind** (25, 50, 85 + increment per ronde) — angka-angka ini bisa di-tuning untuk balancing.
- **Jenis kombinasi poker dan base chips/mult-nya** — bisa ditambah kombinasi baru atau diubah nilainya.
- **Daftar modifier di shop** (Double, Flat, Triple, dll.) — modifier baru bisa ditambahkan via Factory Pattern tanpa mengubah core loop.
- **Harga beli/jual modifier** — parameter ekonomi yang bisa disesuaikan.
- **Jumlah kesempatan main (4) dan discard (3)** — bisa diubah per difficulty level.
- **Jumlah ronde (5)** — bisa ditambah atau dikurangi.
- **Formula bonus currency** — cara menghitung reward di akhir sesi bisa dimodifikasi.