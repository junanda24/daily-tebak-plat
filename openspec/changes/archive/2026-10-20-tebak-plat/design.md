# Design — TEBAK PLAT!

## Stack
Single-page web artifact statis (HTML5 + CSS + vanilla JS atau React+Vite sesuai builder). Gaya visual: pixel arcade 16-bit — palet malam jalanan (aspal gelap + kuning marka jalan + merah/putih plat), font "Press Start 2P" (OFL) untuk judul/kode plat, font baca untuk opsi.

## Arsitektur (ikut ARCHITECTURE.md)
- Frontend feature-based: seluruh game dalam satu feature `tebak-plat/` (components: `PlateCard`, `OptionButton`, `HudBar`, `StartScreen`, `GameOverScreen`; `data/plates.js`; `lib/scoring.js`, `lib/sound.js`, `lib/storage.js`).
- Lima keranjang state: server state — tidak ada; client UI state (layar, opsi terpilih); form state — tidak ada; URL state — tidak ada; ephemeral/local (timer, animasi) via rAF.
- Tidak ada import antar-fitur (ini satu-satunya feature); tidak ada god component (>300 baris dipecah); tidak ada secret; tidak ada backend → tidak ada RFC 9457 yang perlu diimplementasi.

## Interaksi & animasi (momen delight)
- Plat nomor "tercetak" dengan efek typewriter pixel + bunyi tik mesin tik.
- Opsi jawaban: hover/tap → tombol arcade menekan (translate + shadow).
- Benar: ledakan partikel pixel + plat melesat ke kanan seperti mobil ngebut + ding naik nada per kombo.
- Salah: screen shake + plat retak (crack overlay pixel) + buzz.
- Stage naik: banner marquee "STAGE 2 — SUMATERA!" bergulir.
- Detik 3 terakhir: tick + bar timer berkedip merah.

## Game loop
`start → nextQuestion() → rAF timer 12s → answer/timeout → feedback 900ms → nyawa>0 ? nextQuestion() : gameOver()`. Tidak ada softlock: setiap cabang berakhir di nextQuestion/gameOver/restart.

## Aset
100% prosedural: plat digambar dengan CSS (border pixel, teks), partikel via canvas, suara via WebAudio oscillator. Tidak ada gambar/sprite pihak ketiga.
