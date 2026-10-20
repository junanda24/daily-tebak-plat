# Proposal — TEBAK PLAT! (2026-10-20)

## Apa
Game kuis arcade pixel-art: pemain menebak kode plat nomor kendaraan Indonesia (DK → Bali? AB → Jogja?) atau sebaliknya (Bali → plat apa?), lawan timer, dengan nyawa, streak/kombo, dan skor. Jalan di browser HP, bisa langsung dimainkan.

## Kenapa ide ini mengejutkan
Setiap orang Indonesia melihat plat nomor setiap hari di jalan — tapi hampir tidak ada yang hafal semuanya. "Tebak Plat" mengubah pengetahuan jalanan sehari-hari jadi game yang nagih, gaya pixel arcade. Sudut pandang tidak biasa: bukan trivia umum, tapi trivia *jalanan*. Efek "kok kepikiran sih": orang bakal main sambil ingat-ingat plat mobil di parkiran.

## Kenapa bentuk output: game (web artifact)
- Rotasi harian: 4 hari terakhir = web app → game → npm → Dart package. Hari ini slot game.
- Game = format paling cocok: butuh interaktivitas real-time (timer, feedback, touch), sesi 2–5 menit, dan nilai ulangnya tinggi (high score).
- Tidak butuh backend: semua data (44 kode plat, terverifikasi dari 3+ sumber 2026) statis; skor disimpan di localStorage.

## Kenapa tidak pakai backend
Tidak ada state lintas-perangkat yang dibutuhkan; leaderboard global sengaja tidak dibuat (tanpa login = tanpa identitas). Semua bisa 100% client-side.

## Tambahan wajib
- Aset visual 100% original (pixel art digambar via kode/CSS, font Press Start 2P — OFL). Tidak ada karakter/sprite berlisensi.
- Copy Bahasa Indonesia natural, anti-AI-slop.
- Kode ikut `CODE_STANDARDS.md` + `ARCHITECTURE.md` (frontend: satu feature `src/features/tebak-plat/`, state masuk lima keranjang, tidak ada import antar-fitur, tidak ada god component).
