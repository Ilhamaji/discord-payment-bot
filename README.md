<div align="center">

# Discord Payment Bot

**Bot Discord untuk toko produk digital** — katalog item, checkout QRIS, tiket order otomatis, panel admin, dan laporan Excel bulanan.

[![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)](#)
[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?style=flat-square&logo=node.js&logoColor=white)](https://nodejs.org)
[![discord.js](https://img.shields.io/badge/discord.js-v14-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.js.org)

</div>

---

## Tentang

Sistem toko lengkap di dalam Discord: pembeli melihat katalog, membuat tiket order, membayar via **QRIS**, lalu admin memverifikasi lewat panel. Semua transaksi tercatat dan bisa diekspor ke Excel setiap bulan.

## Fitur

### Untuk pembeli

- Item dikelompokkan per kategori, lengkap dengan deskripsi dan harga.
- Setiap transaksi dapat satu channel privat (*tiket*) yang otomatis dihapus saat kedaluwarsa.
- Gambar QRIS statis ditampilkan langsung di dalam tiket, tanpa perlu keluar dari Discord.
- `/panduan` menjelaskan alur pembelian dari awal sampai selesai.
- Leaderboard peringkat pembeli berdasarkan total transaksi.

### Untuk admin

- Katalog dikelola lewat **panel GUI** (button & modal), bukan command manual.
- Tambah/hapus admin beserta tingkat izinnya.
- CRUD item dan kategori: tambah, ubah, hapus.
- Rekap transaksi diekspor ke **Excel** setiap bulan oleh scheduler di dalam bot.
- Tiket kedaluwarsa dibersihkan terjadwal di background.

## Tech Stack

| Bagian | Teknologi |
| --- | --- |
| Runtime | Node.js, CommonJS |
| Bot | Discord.js v14 |
| Database | Supabase (Postgres) + SQLite lokal (`better-sqlite3`) |
| Laporan | ExcelJS |
| Lainnya | `uuid`, GitHub Actions keep-alive |

## Menjalankan

### 1. Clone & install

```bash
git clone https://github.com/Ilhamaji/discord-payment-bot.git
cd discord-payment-bot
npm install
```

### 2. Konfigurasi `.env`

```env
DISCORD_TOKEN=          # token bot
CLIENT_ID=              # application ID
GUILD_ID=               # server ID
SUPABASE_URL=           # URL project Supabase
SUPABASE_KEY=           # service role key
```

Lihat `.env.example` untuk daftar lengkap.

### 3. Daftarkan slash command

```bash
npm run deploy
```

### 4. Jalankan bot

```bash
npm start
```

### 5. Siapkan QRIS

Ganti `assets/qris.jpg` dengan gambar QRIS milikmu.

## Struktur

```
index.js                  # entrypoint + anti-crash handler
commands/                 # slash command (additem, panel, exportreport, ...)
handlers/                 # routing interaksi (admin, order, ticket)
services/                 # panelManager, reportManager, ticketManager, adminPanelGUI
assets/qris.jpg           # gambar QR pembayaran
.github/workflows/        # keep-alive Supabase (mencegah project paused)
```

## Alur Order

```
/panduan -> pilih kategori -> pilih item -> tiket dibuat
        -> tampilkan QRIS -> upload bukti bayar
        -> admin verifikasi di panel -> status selesai -> masuk laporan
```

---

<div align="center">
Dibuat oleh <a href="https://github.com/Ilhamaji">Ilham Aji</a>
</div>
