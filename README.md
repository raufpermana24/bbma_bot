# 🤖 BBMA Bot — GitHub Actions Setup

Bot BBMA OMA ALLY berjalan otomatis di GitHub Actions dengan siklus:
**✅ Nyala 1 jam → 😴 Mati 4 jam → ✅ Nyala lagi (siklus 5 jam)**

---

## 📁 Struktur File

```
repo-kamu/
├── .github/
│   └── workflows/
│       └── bbma_bot.yml      ← Workflow GitHub Actions
├── bbma_bot_top100.py        ← File bot utama
├── requirements.txt          ← Daftar library Python
├── .gitignore
└── README.md
```

---

## 🚀 Cara Setup (Langkah demi Langkah)

### 1. Buat Repository GitHub

```bash
# Buat repo baru di github.com, lalu clone
git clone https://github.com/USERNAME/bbma-bot.git
cd bbma-bot
```

### 2. Upload File Bot

Salin semua file ke dalam folder repo:
- `bbma_bot_top100.py` (file bot kamu)
- `.github/workflows/bbma_bot.yml`
- `requirements.txt`
- `.gitignore`

### 3. Set Secrets di GitHub

Di halaman repo → **Settings** → **Secrets and variables** → **Actions** → klik **New repository secret**

Tambahkan 4 secrets berikut:

| Name | Value |
|------|-------|
| `BINANCE_API_KEY` | API Key Binance kamu |
| `BINANCE_API_SECRET` | API Secret Binance kamu |
| `TELEGRAM_TOKEN` | Token bot Telegram |
| `TELEGRAM_CHAT_ID` | Chat ID Telegram grup/channel |

> ⚠️ **PENTING**: Hapus API key yang hardcode di `bbma_bot_top100.py`!
> Ganti baris ini agar hanya baca dari environment:
> ```python
> API_KEY    = os.environ.get('BINANCE_API_KEY',    '')
> API_SECRET = os.environ.get('BINANCE_API_SECRET', '')
> TELEGRAM_TOKEN   = os.environ.get('TELEGRAM_TOKEN',   '')
> TELEGRAM_CHAT_ID = os.environ.get('TELEGRAM_CHAT_ID', '')
> ```

### 4. Push ke GitHub

```bash
git add .
git commit -m "Setup BBMA bot GitHub Actions"
git push origin main
```

### 5. Aktifkan Actions

- Pergi ke tab **Actions** di repo GitHub
- Klik **"I understand my workflows, go ahead and enable them"**
- Selesai! Bot akan mulai otomatis sesuai jadwal

---

## ⏰ Jadwal Berjalan (Waktu UTC)

| Jam UTC | Jam WIB | Status |
|---------|---------|--------|
| 00:00   | 07:00   | ✅ Nyala |
| 01:00   | 08:00   | 😴 Mati  |
| 05:00   | 12:00   | ✅ Nyala |
| 06:00   | 13:00   | 😴 Mati  |
| 10:00   | 17:00   | ✅ Nyala |
| 11:00   | 18:00   | 😴 Mati  |
| 15:00   | 22:00   | ✅ Nyala |
| 16:00   | 23:00   | 😴 Mati  |
| 20:00   | 03:00   | ✅ Nyala |
| 21:00   | 04:00   | 😴 Mati  |

> 💡 GitHub Actions menggunakan **UTC**. WIB = UTC+7.

---

## 🔧 Jalankan Manual

Di tab **Actions** → pilih workflow **BBMA Bot** → klik **Run workflow** → **Run workflow** (tombol hijau).

---

## 📊 Melihat Log

1. Tab **Actions** di repo
2. Klik run yang sedang berjalan / sudah selesai
3. Klik job **"Jalankan BBMA Bot"**
4. Expand step **"Jalankan bot"** untuk lihat output lengkap

---

## ⚠️ Catatan Penting

- **Free tier GitHub Actions**: 2.000 menit/bulan (private repo) atau unlimited (public repo)
- Bot berjalan **5× sehari × 60 menit = 300 menit/hari** → ~9.000 menit/bulan
- Untuk private repo, **disarankan upgrade ke GitHub Pro** atau jadikan repo **Public**
- State sinyal tersimpan di cache antar sesi agar tidak kirim sinyal duplikat
- Chart tersimpan sebagai artifact selama 3 hari

---

## 🛑 Cara Mematikan Bot Sementara

Di tab **Actions** → klik workflow **BBMA Bot** → **...** → **Disable workflow**

Aktifkan kembali kapan saja dari menu yang sama.
