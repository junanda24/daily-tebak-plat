# TEBAK PLAT!

Game kuis arcade pixel-art 16-bit: tebak kode plat nomor kendaraan Indonesia — "DK itu Bali atau Lombok?" — lawan timer 12 detik, dengan 3 nyawa, kombo beruntun, dan 3 stage dari Pulau Jawa sampai Nusantara. Jalan langsung di browser HP, tanpa install, tanpa login.

**Kenapa ide ini dipilih:** setiap orang Indonesia melihat plat nomor tiap hari di jalan, tapi hampir tak ada yang hafal semuanya. Game ini mengubah pengetahuan "jalanan" sehari-hari jadi sesuatu yang nagih — efek "kok kepikiran sih" yang bikin orang main sambil ingat-ingat plat mobil di parkiran. Slot game harian (rotasi: web app → game → npm → Dart package).

## Fitur

- **58 kode plat terverifikasi** (Sumatera, Jawa, Bali & Nusa Tenggara, Kalimantan, Sulawesi, Maluku & Papua) + plat khusus **CD** (Korps Diplomatik) dan **RI** (Kendaraan Pemerintah)
- **Dua arah soal acak**: KODE→DAERAH (tampil "DK", pilih daerahnya) dan DAERAH→KODE (tampil "Bali", pilih kodenya)
- **3 stage bertingkat**: Stage 1 Pulau Jawa → Stage 2 Sumatera → Stage 3 Nusantara, naik tiap 5 benar beruntun (banner marquee "STAGE NAIK!")
- **Timer 12 detik** per soal, bar menyusut, tick + kedip merah di 3 detik terakhir
- **3 nyawa pixel** — salah/timeout = nyawa −1, screen shake, suara buzz, kombo reset
- **Skor berbasis kecepatan**: (100 + sisa_detik × 10) × pengali kombo; soal PLAT KHUSUS tiap ~8 soal bernilai 2×
- **High score persisten** di localStorage + label "REKOR BARU!"
- **Game feel arcade**: suara 100% prosedural WebAudio (ding naik nada per kombo, buzz, tick, fanfare), partikel pixel, plat melesat seperti mobil ngebut saat benar, efek retak pixel saat salah, mobil pixel melintas di layar mulai
- Kontrol tap + keyboard (1–4 pilih opsi, Enter mulai/restart), toggle suara, hormat `prefers-reduced-motion`
- Layar: mulai → main (HUD skor/kombo/nyawa/stage/timer) → game over (skor, best, statistik benar–salah, stage tertinggi) → main lagi

## Cara main

1. Buka `src/tebak-plat.html` di browser (HP atau desktop) — atau mainkan versi artifact di link di bawah.
2. Tekan **MULAI**, baca soal, jawab sebelum timer habis.
3. Keyboard: tombol **1–4** untuk pilih jawaban, **Enter** untuk mulai/restart.
4. Kehabisan 3 nyawa = game over. Pecahkan rekor tertinggimu!

## Menjalankan dari source

Tidak perlu build step — ini satu file HTML mandiri:

```bash
# cara termudah: buka langsung
xdg-open src/tebak-plat.html        # Linux
open src/tebak-plat.html            # macOS
# atau sajikan via server lokal
python3 -m http.server -d src 8080  # lalu buka http://localhost:8080/tebak-plat.html
```

## Tech stack

- HTML5 + CSS + vanilla JS (satu file, tanpa bundler, tanpa dependency runtime)
- Font pixel "Press Start 2P" / "VT323" (Google Fonts, lisensi OFL) dengan fallback monospace
- WebAudio API untuk semua efek suara (prosedural, tanpa file audio)
- localStorage untuk high score
- Semua aset visual original dari kode (CSS/canvas) — tanpa gambar atau sprite pihak ketiga

## Struktur folder

```
.
├── README.md
├── src/
│   └── tebak-plat.html      # game lengkap (export dari web artifact)
└── openspec/changes/2026-10-20-tebak-plat/
    ├── proposal.md          # apa & kenapa
    ├── design.md            # pendekatan teknis + arsitektur
    ├── tasks.md             # checklist implementasi
    ├── specs/tebak-plat/spec.md   # requirement SHALL + skenario WHEN/THEN
    └── archive/             # arsip change setelah selesai
```

## Link hasil

- Game (artifact): dibuat 2026-10-20 — link dibagikan saat delivery harian
- Repo: https://github.com/junanda24/daily-tebak-plat

## Catatan build

- Data 58 kode plat diverifikasi silang dari 3 sumber publik (samsatkeliling.info, mototren.com, transportasimedia.com) pada 2026-10-20. Ambigu lintas-sumber diselesaikan dengan versi terbanyak; nama daerah ditulis dengan kota/wilayah utama + provinsi agar tidak ambigu saat jadi pengecoh.
- Distractor (pengecoh) diprioritaskan dari pulau yang sama supaya soal stage awal tidak terlalu mudah.
- Stage 1 pool = semua entri berlabel pulau "Jawa" (termasuk Jatim) agar pemain pemula tidak langsung dihajar 58 kode.
- Verifikasi mandiri: 47/47 asersi jsdom end-to-end lolos (mulai, stage naik, soal khusus 2×, salah, timeout 12 detik real, game over, rekor tersimpan persis = skor akhir, restart, kembali ke menu) + probe browser langsung (klik jawaban benar, partikel, plat melesat, skor sesuai rumus).
- Google Fonts sempat terblokir egress saat audit build; font dimuat normal setelah artifact di-publish, dengan fallback rapi selama audit.
