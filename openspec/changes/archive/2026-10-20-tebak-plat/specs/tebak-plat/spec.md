# Spec — TEBAK PLAT!

## Data
SHALL ada minimal 40 entri kode plat yang akurat, terverifikasi dari ≥2 sumber publik (samsatkeliling.info, mototren.com, transportasimedia.com, diakses 2026-10-20):
- Sumatera: BL Aceh · BB Sumut Barat (Tapanuli) · BK Sumut (Medan) · BA Sumbar · BM Riau · BP Kepri (Batam/Tanjung Pinang) · BG Sumsel (Palembang) · BN Babel · BE Lampung · BD Bengkulu · BH Jambi
- Jawa: A Banten · B Jakarta/Bodetabek · D Bandung · E Cirebon · F Bogor · T Karawang/Purwakarta · Z Garut/Tasikmalaya · G Pekalongan/Tegal · H Semarang · K Pati/Kudus · R Banyumas · AA Magelang · AB Yogyakarta · AD Solo
- Jatim: L Surabaya · M Madura · N Malang · P Besuki/Jember/Banyuwangi · S Bojonegoro/Mojokerto · W Sidoarjo/Gresik · AE Madiun · AG Kediri
- Bali & Nusa Tenggara: DK Bali · DR Lombok/Mataram (NTB) · EA Sumbawa (NTB) · DH Kupang/Timor (NTT) · EB Flores (NTT) · ED Sumba (NTT)
- Kalimantan: DA Kalsel · KB Kalbar · KH Kalteng · KT Kaltim · KU Kaltara
- Sulawesi: DB Manado/Sulut daratan · DL Sangihe Talaud · DM Gorontalo · DN Sulteng · DD Sulsel selatan (Makassar) · DP Sulsel utara (Palopo/Luwu) · DC Sulbar · DT Sultra
- Maluku & Papua: DE Maluku · DG Maluku Utara · PA Papua · PB Papua Barat
- Khusus: CD Korps Diplomatik · RI Kendaraan Pemerintah RI
Setiap entri: `{ kode, daerah, pulau }`. Daerah ditampilkan dengan nama kota/wilayah utama + provinsi.

## Mekanik
1. **Dua arah soal** (acak per soal):
   - KODE→DAERAH: tampil plat besar "DK", pilih 1 dari 4 nama daerah.
   - DAERAH→KODE: tampil "Bali", pilih 1 dari 4 kode plat.
   WHEN soal muncul THEN 4 opsi unik, jawaban benar acak posisinya, pengecoh (distractor) diambil dari pulau yang sama bila tersedia.
2. **Stage bertingkat** (SHALL):
   - Stage 1 "Pulau Jawa": pool Jawa (Bali bonus tidak ada).
   - Stage 2 "Sumatera": pool Jawa + Sumatera.
   - Stage 3 "Nusantara": seluruh 44 entri.
   WHEN pemain benar 5x berturut-turut THEN naik stage, tampil banner "STAGE NAIK!".
3. **Timer**: SHALL 12 detik per soal, bar menyusut; WHEN waktu habis THEN dihitung salah.
4. **Nyawa**: SHALL 3 nyawa (ikon ban/hati pixel). WHEN salah/timeout THEN nyawa −1 + screen shake + suara buzz. WHEN nyawa 0 THEN game over.
5. **Skor & kombo**: WHEN benar THEN skor += (100 + sisa_detik × 10) × (1 + min(streak,10) × 0.1); streak +1, tampil "KOMBO xN". WHEN salah THEN streak reset 0.
6. **Plat khusus**: setiap ~8 soal ada soal bonus bertanda "PLAT KHUSUS" (CD/RI), nilai 2×.
7. **High score**: SHALL tersimpan di localStorage (`tebakplat_high`); WHEN skor baru > high THEN tampil "REKOR BARU!".

## Layar & kontrol
- Layar: start (judul, cara main, high score, tombol MULAI) → main → game over (skor, best, statistik: benar/salah, stage tertinggi; tombol MAIN LAGI).
- Kontrol: tap/click opsi; keyboard 1–4 pilih opsi, Enter mulai/restart. SHALL responsif di layar 360px.
- Game feel: partikel pixel saat benar, screen shake saat salah, suara prosedural WebAudio (ding/buzz/tick detik terakhir), tanpa aset audio eksternal.

## Non-fungsional
- Tanpa login/database/backend; tanpa lorem ipsum/placeholder; tidak ada tombol mati.
- Prefers-reduced-motion dihormati (matikan shake & partikel).
