# PROMPT untuk agent di LAPTOP — rekam footage P001 Sembako Pintar lalu unggah ke Directus

Clone repo ini di laptop, buka agent di dalam foldernya, lalu kirim: **"Baca PROMPT.md dan kerjakan."**
Token Directus TIDAK ada di repo (repo publik). Owner memberikannya terpisah → simpan sebagai `rahasia/directus-token.txt` (folder ini di-.gitignore). Belum ada → minta ke owner.

---

## Tugas
Rekam 9 footage demo aplikasi **Sembako Pintar POS** (aplikasi kasir toko sembako, https://sembako-pintar.nusawebsite.com) dengan **Recordly**,
olah dengan gaya standar owner, lalu unggah tiap MP4 ke Directus. Footage dipakai merakit video YouTube review **P001 "aplikasi kasir toko sembako"**
(perakitan dikerjakan di PC lain, bukan tugasmu). Standar sama persis dengan video DentalCare YT002.

Daftar shot, rute, langkah klik, dan durasi target: **`bahan/SHOTLIST-P001.md`** (sumber kebenaran). Naskah + VO per bagian ada di `bahan/`
(putar `bahan/vo/06-satuan.wav` sambil latihan S2, dst. untuk mencocokkan tempo).

| Shot | Nama file | Target |
|---|---|---|
| B1 Dashboard | b1-dashboard.mp4 | 30 dtk |
| B2 Kasir | b2-kasir.mp4 | 12 dtk |
| S1 Kasir cepat | s1-kasir.mp4 | 12,7 dtk |
| S2 Jual kiloan | s2-kiloan.mp4 | 13,8 dtk |
| S3 Satuan & paket grosir | s3-satuan.mp4 | 15,7 dtk |
| S4 Bayar & struk | s4-struk.mp4 | 12,7 dtk |
| S5 Stok otomatis | s5-stok.mp4 | 12,3 dtk |
| S6 Pembelian supplier | s6-pembelian.mp4 | 11,7 dtk |
| S7 Laporan & cabang | s7-laporan.mp4 | 13,5 dtk |

## Aplikasi & data demo
- Login: Username `owner` / Password `password` (tombol MASUK). Viewport browser 1920x1040.
- Data demo sudah berisi produk sembako, 2 cabang (Cabang Utama, Cabang Dago), supplier, member, riwayat penjualan 30 hari.
- Tidak ada banner "MODE DEMO". Kalau ada banner/peringatan demo terlihat, BERHENTI dan lapor ke owner.
- Halaman tabel kadang lambat memuat (skeleton abu-abu). Mulai Record hanya setelah baris tabel terisi.
- Kasir: bila diminta memilih cabang, pilih "Cabang Utama".

## 1. Setup (kerjakan sendiri, cek dulu yang sudah terpasang)
1. Node 22+, Python 3.10+ (`pip install pyautogui`), Git Bash bila Windows.
2. Playwright: `npm i playwright` di folder ini, lalu `npx playwright install chromium`.
3. **Recordly v1.4.0**: unduh dari rilis resmi https://github.com/webadderallorg/Recordly/releases (Windows: `Recordly-windows-x64.exe`).
   Jalankan dengan `--remote-debugging-port=9556` supaya bisa dikendalikan lewat CDP (lihat `skrip-pc/kendali.js`).
4. Preset gaya: salin `recordly-setting/app-settings.json` ke folder data Recordly (Windows: `%APPDATA%\Recordly\app-settings.json`,
   tutup Recordly dulu, cadangkan file lama). Isinya preset **"Nusawebsite Demo"**. Bila tidak terbaca, buat ulang manual:
   wallpaper putih-biru muda (baris 3 kolom 1), blur 3.5px, shadow 53%, radius 2.4%, padding 14%, crop atas 9%,
   kursor 1.0, click bounce 2, sway 0.2 → simpan sebagai preset "Nusawebsite Demo".
5. `skrip-pc/` = skrip yang SUDAH TERBUKTI di PC owner untuk DentalCare. `BASE` di `rekam.js` sudah diganti ke Sembako Pintar,
   tapi alur & login di dalamnya masih DentalCare (email `admin@klinik.com`): ganti login ke field Username/Password di atas dan
   tulis alur baru dari `bahan/SHOTLIST-P001.md` dengan gaya gerak yang sama. Path PC (`E:/...`, `C:/Users/RIFE/...`, Python310) ganti ke path laptop.
   Alur utama: `sesi.sh <alur>` (rekam + olah) dan `proses.sh <rekaman.mp4> <keluaran.mp4>` (olah ulang tanpa rekam).

## 2. Aturan rekam (keputusan owner, WAJIB)
- Rekam **JENDELA browser aplikasi saja**, bukan seluruh layar. Desktop/ikon/notifikasi pribadi tidak boleh terekam.
- Sembunyikan HUD Recordly (Hide HUD) sebelum Record. Tutup browser hanya SETELAH Stop.
- Kursor = kursor OS asli (lewat `mouse_server.py`/pyautogui) supaya Recordly mencatat klik. Ukuran kursor **maks 1.0**.
- Gerak: kursor meluncur ±0,9 dtk ke target, klik, lalu diam/geser kecil ±1,6 dtk. Jeda antar aksi ≤1 dtk, kursor tidak diam lama.
  Scroll hanya setelah zoom keluar.
- **ANTI-GOYANG:** zoom mode **Manual** dengan fokus di titik klik asli (`fokus-klik.js` membaca `<rekaman>.mp4.cursor.json`).
  JANGAN mode Auto. Urutan olah: preset → kursor 1.0 → crop 9% → Suggest Zooms → fokus-klik → ekspor.
- TIDAK ada hapus/void/batal data, TIDAK menyimpan form produk. Transaksi baru (S1 → S2 → S4) hanya di TAKE FINAL, satu kali.
- Durasi tiap footage = target (boleh lebih 1-2 dtk, jangan kurang).

## 3. Cara kerja
1. Setup, lalu buat **1 rekaman uji: S2 jual kiloan** (`s2-kiloan`). Unggah ke Directus (lihat §4) dan tunjukkan ke owner; tunggu "oke" sebelum merekam semua.
2. Latihan tiap shot tanpa Record (hover sebagai ganti klik yang mengubah data), lalu take final.
3. Periksa tiap hasil sebelum diunggah: ambil frame (ffmpeg), pastikan tidak ada HUD, desktop, skeleton loading, zoom goyang, dan durasinya cukup. Ulang shot yang gagal.

## 4. Unggah ke Directus
Pakai `skill/directus-pustaka/simpan.mjs` (baca `SKILL.md`-nya). Token: `rahasia/directus-token.txt` → env `DIRECTUS_TOKEN` (JANGAN cetak isinya).
Butuh ffmpeg + ffprobe di PATH.

```bash
export DIRECTUS_TOKEN="$(cat rahasia/directus-token.txt)"
node skill/directus-pustaka/simpan.mjs --brand Nusawebsite --jenis Video --sub "Sembako Pintar/Footage Recordly/P001" \
  --file out/s2-kiloan.mp4 --varian "p001 s2 kiloan" --produk "Sembako Pintar" --kategori screen-recording \
  --deskripsi "Footage Recordly P001 S2: jual kiloan beras, pilih satuan kg/ons/gram" --tags "p001,recordly,sembako-pintar"
```
Coba dulu dengan `--dry`. Nama sama ditolak; pakai `--ganti` hanya untuk mengganti take yang jelek.

## 5. Lapor ke owner
Daftar shot + id/nama file Directus + durasi tiap file + catatan shot yang diulang.
