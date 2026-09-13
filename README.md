ZENTRIX GENERATOR BOT — Render Deployment

Deploy on Render (free) — 3 steps

1. Push to GitHub
Upload this whole folder as a GitHub repo (add your stock `.txt` files inside `stock/`).

2. Create Web Service on Render
- Render Dashboard → New + → Web Service → connect your repo
- Render auto-detects `render.yaml` — or set manually:
  - Build Command: `pip install -r requirements.txt`
  - Start Command: `python bot.py`
  - Health Check Path: `/`

3. Set Environment Variables
In Render → your service → Environment:

Key	Value	
`BOT_TOKEN`	your token from @BotFather	
`ADMIN_IDS`	your Telegram user ID (e.g. `123456789`, comma-separated for multiple)	

Click Deploy. Done — the bot runs 24/7 and the `/` health check keeps the service alive.

Commands

User

Command	Description	
/start	Menu with inline buttons	
/redeem KEY	Redeem key (required before generating)	
/generate	Pick a stock, receive TXT file	
/stock	Available stocks + lines remaining	
/me	Your tier, key, total generations	

Admin

Command	Description	
/genkey	Reply format: `Premium 5` or `Platinum 3`	
/revoke USER_ID	Remove user access permanently	
/check USER_ID	View user tier + generation count	

Stock Management
The bot reads `.txt` files from `stock/`. Two ways to add stock on Render:

1. Via GitHub — push new `.txt` files into `stock/`, Render redeploys automatically.
2. Via Render Shell — Dashboard → your service → Shell:
   
```
   cd stock && curl -L -o GARENA.txt "YOUR_FILE_URL"
   ```

⚠️ Render free tier erases the disk on every redeploy. The stock `.txt` files and offsets are safe if you commit them to GitHub — but if you add stock via Shell only, it disappears on redeploy. For permanent stock updates, use GitHub.

Key Tiers

Tier	Expiration	Lines per generate	
Premium	Never	3,000	
Platinum	Never	2,500	

Key format: `Premium-123-456-789` · 1 key = 1 user (locked on redeem)

Local test

```
pip install -r requirements.txt
set BOT_TOKEN=xxx && set ADMIN_IDS=123456789 && python bot.py
```

(Linux/Mac: `export BOT_TOKEN=xxx` instead of `set`)
