# Tasks — TEBAK PLAT!

1. [ ] Siapkan struktur feature `tebak-plat/` + data 44+2 entri plat (terverifikasi).
2. [ ] Layar start: judul, cara main, high score, tombol MULAI (keyboard Enter).
3. [ ] HUD: skor, kombo, nyawa (3), stage, timer bar 12s.
4. [ ] Komponen PlateCard (KODE→DAERAH & DAERAH→KODE) + 4 OptionButton (tap + keyboard 1–4).
5. [ ] Logika soal: acak arah, pengecoh se-pulau, stage pool bertingkat, soal bonus CD/RI tiap ~8 soal.
6. [ ] Scoring: 100 + sisa_detik×10, multiplier kombo, 2× untuk plat khusus; streak reset saat salah.
7. [ ] Nyawa & game over: −1 saat salah/timeout, shake+buzz, game over di 0; layar hasil + statistik + MAIN LAGI.
8. [ ] High score localStorage + banner REKOR BARU.
9. [ ] Game feel: partikel, shake, WebAudio (ding/buzz/tick), efek plat melesat, banner stage; hormati prefers-reduced-motion.
10. [ ] Mobile 360px: layout portrait, tombol besar, tidak ada overflow.
11. [ ] Verify: mainkan simulasi penuh (start→5 soal→salah→timeout→game over→restart), tidak ada error console, skor tersimpan, tidak ada softlock.
12. [ ] Export artifact → salin ke `src/` project; README lengkap; commit; repo GitHub; push; verifikasi API.
