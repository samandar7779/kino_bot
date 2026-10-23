# 🎬 Kino Bot

Telegram kino boti: obuna tekshiruvi, kino kod bo'yicha yuborish, admin panel
(kino qo'shish/o'chirish, statistika, broadcast).

## Talablar

- Python 3.13+
- `pyTelegramBotAPI`

## Lokal ishga tushirish

```bash
pip install -r requirements.txt
```

`.env.example` faylidan `.env` yaratib, qiymatlarni to'ldiring:

```bash
copy .env.example .env      # Windows
cp .env.example .env        # Linux/macOS
```

So'ng:

```bash
python main.py
```

(yoki Windows'da `start_bot.bat`)

## Environment variables

| Nomi          | Majburiy | Tavsif                                         |
|---------------|----------|------------------------------------------------|
| `BOT_TOKEN`   | ✅       | BotFather'dan olingan token                   |
| `ADMINS`      | ❌       | Admin ID'lari, vergul bilan (`1,2,3`)          |
| `CHANNEL_ID`  | ❌       | Majburiy obuna kanali ID si                    |
| `CHANNEL_URL` | ❌       | Obuna kanali havolasi                          |
| `DB_PATH`     | ❌       | SQLite fayl yo'li (doimiy disk uchun)          |
| `PORT`        | ❌       | Berilsa, health-check HTTP server ochiladi     |

## Serverga joylash (Render)

1. Repo'ni GitHub'ga push qiling.
2. Render'da **New → Web Service** → reponi ulang.
3. Sozlamalar:
   - **Root Directory:** bo'sh
   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `python main.py`
4. **Environment** bo'limiga `BOT_TOKEN`, `ADMINS`, `CHANNEL_ID`, `CHANNEL_URL`
   qiymatlarini kiriting.
5. **Deploy** qiling.

### Muhim eslatmalar

- **Bepul Web Service 15 daqiqa harakatsizlikdan keyin uxlaydi.** Bot uzluksiz
  ishlashi uchun cron-job.org / UptimeRobot orqali har 5–10 daqiqada servis
  URL'iga ping yuboring yoki pullik instansdan foydalaning.
- **SQLite ma'lumotlari vaqtinchalik diskda saqlanadi** va har deploy'da
  o'chadi. Render Disk (pullik) ulab, uning mount yo'lini `DB_PATH` ga bering
  (masalan `/var/data/kino_bot.db`), aks holda PostgreSQL'ga o'tish tavsiya
  etiladi.
- Bot long-polling rejimida ishlaydi, shuning uchun alohida domen/SSL kerak
  emas. Health-check server faqat platformaning port talabini qondirish uchun.

## Xavfsizlik

- Tokenni hech qachon kodga yozmang yoki public repo'ga qo'ymang.
- Token oshkor bo'lgan bo'lsa: BotFather → `/revoke` orqali yangilang.
