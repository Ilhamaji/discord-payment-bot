<div align="center">

# Discord Payment Bot

**A Discord storefront for digital products** — item catalogue, QRIS checkout, automated order tickets, an admin panel, and monthly Excel reports.

[![Status](https://img.shields.io/badge/status-active-brightgreen?style=flat-square)](#)
[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?style=flat-square&logo=node.js&logoColor=white)](https://nodejs.org)
[![discord.js](https://img.shields.io/badge/discord.js-v14-5865F2?style=flat-square&logo=discord&logoColor=white)](https://discord.js.org)

**English** · [Bahasa Indonesia](README.id.md)

</div>

---

## About

A complete storefront that lives inside Discord. Buyers browse the catalogue, open an order ticket, pay by **QRIS**, and an admin confirms the payment from a panel. Every transaction is recorded and can be exported to Excel at the end of each month.

## Features

### For buyers

- Items are grouped by category, each with a description and price.
- Every order gets a private channel (a *ticket*) that is deleted automatically once it expires.
- A static QRIS image is shown inside the ticket, so the buyer never leaves Discord.
- `/panduan` walks through the purchase flow end to end.
- A leaderboard ranks buyers by total spend.

### For admins

- The catalogue is managed through a **GUI panel** (buttons and modals) rather than manual commands.
- Add or remove admins along with their permission level.
- Full CRUD for items and categories.
- A scheduler inside the bot exports a transaction recap to **Excel** every month.
- Expired tickets are cleaned up on a background schedule.

## Tech Stack

| Layer | Technology |
| --- | --- |
| Runtime | Node.js, CommonJS |
| Bot | Discord.js v14 |
| Database | Supabase (Postgres) + local SQLite (`better-sqlite3`) |
| Reporting | ExcelJS |
| Other | `uuid`, GitHub Actions keep-alive |

## Getting Started

### 1. Clone and install

```bash
git clone https://github.com/Ilhamaji/discord-payment-bot.git
cd discord-payment-bot
npm install
```

### 2. Configure `.env`

```env
DISCORD_TOKEN=          # bot token
CLIENT_ID=              # application ID
GUILD_ID=               # server ID
SUPABASE_URL=           # Supabase project URL
SUPABASE_KEY=           # service role key
```

See `.env.example` for the full list.

### 3. Register slash commands

```bash
npm run deploy
```

### 4. Start the bot

```bash
npm start
```

### 5. Set up QRIS

Replace `assets/qris.jpg` with your own QRIS image.

## Project Layout

```
index.js                  # entrypoint + anti-crash handlers
commands/                 # slash commands (additem, panel, exportreport, ...)
handlers/                 # interaction routing (admin, order, ticket)
services/                 # panelManager, reportManager, ticketManager, adminPanelGUI
assets/qris.jpg           # payment QR image
.github/workflows/        # Supabase keep-alive (stops the project from pausing)
```

## Order Flow

```
/panduan -> pick a category -> pick an item -> ticket created
        -> QRIS shown -> buyer uploads proof of payment
        -> admin confirms in the panel -> order closed -> counted in the report
```

---

<div align="center">
Built by <a href="https://github.com/Ilhamaji">Ilham Aji</a>
</div>
