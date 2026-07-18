# 🚀 Telegram VPS & RDP Store Bot (Premium)

Bot Telegram untuk jualan VPS, RDP, AWS, Digital Ocean & produk digital lainnya.
Modular, realtime, anti double transaksi, dan siap deploy ke Render.

## ✨ Fitur

- 🛒 Katalog produk dinamis dengan **pagination** (admin dapat add/edit/delete realtime)
- 📸 Upload gambar produk via **foto Telegram** atau URL
- 👥 **Multi-admin** via `/addadmin`, `/removeadmin`, `/listadmins` (super-admin only)
- 💳 Pembayaran QRIS (gambar dapat diganti admin via foto/URL kapan saja)
- 📤 Upload bukti transfer
- 🔔 Notifikasi admin lengkap dengan tombol Approve / Reject
- 📦 Menu "Pesanan Saya" — hanya menampilkan order aktif (waiting_payment / waiting_review / processing)
- 👑 Admin panel tersembunyi (`/admin`)
- 📊 Dashboard realtime (total user, order, revenue, dll)
- 📢 Broadcast (admin tidak menerima broadcast miliknya sendiri)
- 🔒 Anti double order / double click / double invoice / spam callback
- 🖼 Banner & caption dinamis
- ✏️ Semua menu pakai `editMessage` — chat tetap bersih

## 🛠 Tech Stack

- Node.js 18+ (LTS)
- Telegraf 4
- MongoDB + Mongoose
- Express (health endpoint + webhook)
- dotenv, axios, moment, Node.js crypto

## 📁 Struktur Folder

```
src/
├── commands/      # /start, /admin
├── handlers/      # user, order, admin flow
├── middlewares/   # auth, anti-spam
├── models/        # mongoose schemas
├── services/      # business logic
├── utils/         # format, invoice, safeEdit, locks
├── keyboards/     # inline keyboards
├── config/        # env + db
├── Bot.js         # registrasi handler
└── app.js         # entry point
```

## 🚀 Setup Lokal (VS Code)

```bash
git clone <repo-url>
cd telegram-vps-rdp-store
cp .env.example .env
# isi BOT_TOKEN, ADMIN_ID, ADMIN_USERNAME, MONGODB_URI
npm install
npm start
```

## 🔑 Cara mendapatkan credentials

| Variable | Cara Dapat |
|---|---|
| `BOT_TOKEN` | Chat [@BotFather](https://t.me/BotFather) → `/newbot` |
| `ADMIN_ID` | Chat [@userinfobot](https://t.me/userinfobot) → copy ID |
| `ADMIN_USERNAME` | Username Telegram admin (tanpa `@`) |
| `MONGODB_URI` | [MongoDB Atlas](https://cloud.mongodb.com) → Free cluster → Connect → Drivers |

## ☁️ Deploy ke Render

1. Push repo ke GitHub.
2. Di [Render](https://render.com): **New +** → **Web Service** → connect repo.
3. **Build Command**: `npm ci --omit=dev`
4. **Start Command**: `npm start`
5. **Environment Variables**: tambahkan semua dari `.env.example`.
6. (Opsional) Set `WEBHOOK_URL` ke URL Render Anda (misal `https://yourapp.onrender.com`) untuk mode webhook. Kosongkan untuk long polling.
7. Deploy. Cek `/health` endpoint untuk memastikan service hidup.

> 💡 Untuk Render Free Tier, set cron-job.org ping ke `/health` setiap 5 menit agar bot tidak sleep.

## 🧪 Verifikasi

```bash
# Validate dependencies
npm install --dry-run

# Lint
npm run lint
```

## 📜 Lisensi

MIT
