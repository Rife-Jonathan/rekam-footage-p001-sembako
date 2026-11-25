# SHOTLIST P001 — "aplikasi kasir toko sembako" (Sembako Pintar POS)

Naskah: `naskah.json` (14 bagian). VO Fola satu jalan 162,8 dtk; durasi per bagian dari `vo/bagian.json` (25 Nov 2026). VO per bagian: `bahan/vo/<id>.wav`.
Rekam dengan Recordly preset "Nusawebsite Demo": rekam JENDELA aplikasi saja, kursor maks 1.0, zoom Manual di titik klik.
Demo: https://sembako-pintar.nusawebsite.com · login `owner` / `password` (field Username, Password, tombol MASUK).
Viewport 1920x1040, DSF 1. **Durasi target = durasi VO + 1 dtk** (boleh lebih 1-2 dtk, jangan kurang).
Aturan aman: TIDAK ada hapus/void/batal. Transaksi baru (S1-S4) hanya di TAKE FINAL, satu kali, urut S1 → S2 → S4.
Pemilih cabang di kasir: pilih "Cabang Utama". Halaman tabel kadang lambat: tunggu baris terisi (skeleton hilang) sebelum mulai rekam.
Gaya gerak: kursor meluncur ±0,9 dtk ke target, klik, diam ±1,6 dtk selama zoom; scroll hanya setelah zoom keluar.

## Bagian non-demo (b-roll / kartu, dirakit otomatis)
| Bagian VO | Perkiraan | Visual |
|---|---|---|
| 01 Opening | 13,4 dtk | kartu pembuka 2 dtk "Aplikasi Kasir Toko Sembako" → B1 dashboard |
| 02 Empathy | 11,2 dtk | B1 lanjutan + B2 kasir |
| 03 Problem | 11,0 dtk | KARTU k1 "Hitung kiloan di kalkulator · Stok dicek di rak · Nota supplier tercecer" |
| 04 Promise | 8,6 dtk | KARTU k2 "Kasir, stok, pembelian, laporan dalam satu sistem" → B1 |
| 12 Recap | 13,5 dtk | KARTU k3 7 chip fitur |
| 13 Positioning | 10,7 dtk | KARTU k4 kutipan |
| 14 CTA | 9,0 dtk | banner WA + demo |

### B1 — Dashboard (b-roll) · target 30 dtk
- Rute `/dashboard` (Semua cabang). Tunggu kartu "Hari ini per cabang" terisi.
- [hover "Total semua cabang", 2] → [hover kartu "Cabang Utama", 2] → [hover "Omzet Hari Ini", 2] → [hover grafik "Penjualan 7 Hari Terakhir" batang tengah, 3]
  → [klik tab "30 hari", 2] → [klik "7 hari", 2] → [scroll pelan ke "Penjualan per Kategori" setelah zoom keluar, 3] → [diam]
### B2 — Kasir (b-roll) · target 12 dtk
- Rute `/pos`, pilih "Cabang Utama" bila diminta. [hover kartu produk "Beras Premium", 2] → [hover "Minyak Kita 1 L", 2] → [klik kategori "Sembako", 2] → [diam]

## Bagian demo (footage cocok kalimat VO)
### S1 — Kasir cepat (VO 05, 11,7 dtk) · target 12,7 dtk
- Rute `/pos`. 1. [klik kotak "Cari produk", ketik "telur" pelan] — "mencari nama barang" 2. [klik "Telur Ayam", dialog jumlah, isi 1, klik "Tambah ke Keranjang"] — "barang masuk ke keranjang"
  3. [hover total di panel kanan "Daftar belanja", 2] — "total belanja langsung terlihat"
### S2 — Jual kiloan (VO 06, 12,8 dtk) · target 13,8 dtk
- Lanjut di `/pos`. 1. [cari "beras", klik "Beras Premium"] → dialog "Input Jumlah — Timbang" 2. [klik pilihan satuan Kilogram, lalu Ons, lalu kembali Kilogram, 1 dtk tiap] — "kilogram, ons, atau gram"
  3. [isi Jumlah 2, total di dialog berubah, 1,5] — "totalnya dihitung otomatis" 4. [klik "Tambah ke Keranjang"]
### S3 — Satuan & paket grosir (VO 07, 14,7 dtk) · target 15,7 dtk
- Rute `/units`. 1. [hover grup BERAT: Gram, Ons, Kilogram, 3] 2. [hover grup VOLUME & JUMLAH (Liter, Pcs, Dus), 2]
  3. Buka `/products`, klik ikon ubah "Gula Pasir" (atau produk berbasis gram) → scroll ke tabel "Satuan produk" (gram, kg, paket), hover baris, 4 dtk. JANGAN simpan.
### S4 — Bayar & struk (VO 08, 11,7 dtk) · target 12,7 dtk
- Kembali `/pos` (keranjang S1-S2 masih ada). 1. [klik tombol uang pas/"100.000" di panel bayar] 2. [klik "PROSES PEMBAYARAN"] → halaman Struk
  3. [hover "Kembalian" di kartu kanan, 1,5] 4. [hover isi struk (barang, jumlah, satuan), 3] 5. [hover "Sambungkan printer & cetak", 1,5] — JANGAN klik.
### S5 — Stok otomatis (VO 09, 11,3 dtk) · target 12,3 dtk
- Rute `/inventory`. 1. [hover kartu "Produk menipis", 2] 2. [pilih filter Status stok "Menipis", 2] 3. [kembalikan filter, klik ikon riwayat "Bawang Merah"] → `/inventory/<id>` Riwayat Stok
  4. [hover baris Pembelian (+) lalu Penjualan (−), 3]
### S6 — Pembelian supplier (VO 10, 10,7 dtk) · target 11,7 dtk
- Rute `/purchases`. 1. [hover kolom NO. NOTA & SUPPLIER baris 1, 2] 2. [klik baris 1] → Detail Pembelian 3. [hover "Rincian barang", 2] 4. [scroll ke "Pergerakan stok" (stok bertambah), 3]
### S7 — Laporan & cabang (VO 11, 12,5 dtk) · target 13,5 dtk
- Rute `/reports/sales`. 1. [hover "Total Penjualan" & "Laba Kotor (Estimasi)", 2] 2. [hover grafik "Penjualan per Hari", 2] 3. [klik tab "Produk", hover baris 1-3 terlaris, 3]
  4. Buka `/dashboard`, [hover kartu "Cabang Utama" lalu "Cabang Dago", 3]

## Unggah
Directus `Nusawebsite/Video/Sembako Pintar/Footage Recordly/P001/`, nama `p001-b1-dashboard`, `p001-b2-kasir`, `p001-s1-kasir`, `p001-s2-kiloan`,
`p001-s3-satuan`, `p001-s4-struk`, `p001-s5-stok`, `p001-s6-pembelian`, `p001-s7-laporan`.
Urutan kerja: 1 rekaman UJI (S2 jual kiloan) → owner setuju → semua shot.
