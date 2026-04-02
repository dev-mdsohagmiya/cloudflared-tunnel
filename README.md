# 🚀 Cloudflare Tunnel Setup (Simple Guide)

This guide shows how to make your localhost app live using Cloudflare Tunnel.

---

## ✅ Requirements

- Cloudflare account
- A domain added to Cloudflare
- Local app running (example: http://localhost:3000)

---

## 📥 Step 1: Download Cloudflared

Download from:
https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/install-and-setup/

For Windows:
- Download `cloudflared.exe`
- Put it in a folder (example: `C:\cloudflared`)

---

## 🔐 Step 2: Login

Run:

```bash
./cloudflared tunnel login
A browser will open
Login to Cloudflare
Select your domain
🏗️ Step 3: Create Tunnel
./cloudflared tunnel create my-tunnel

Example:

./cloudflared tunnel create campustransfer-website

This will create a tunnel and save credentials.

🌐 Step 4: Connect Domain
./cloudflared tunnel route dns my-tunnel demo.yourdomain.com

Example:

./cloudflared tunnel route dns campustransfer-website demo.gubdi.com

👉 This creates a DNS record.

⚠️ If you get error:

record already exists

Go to Cloudflare DNS
Delete old A / CNAME record
Run command again
⚙️ Step 5: Create Config File

Go to:

C:\Users\YOUR_NAME\.cloudflared

Create config.yml

Example:

tunnel: YOUR_TUNNEL_ID
credentials_file: C:\Users\YOUR_NAME\.cloudflared\YOUR_TUNNEL_ID.json

ingress:
  - hostname: www.gubdi.com
    service: http://localhost:3000
  - service: http_status:404
▶️ Step 6: Run Tunnel
./cloudflared tunnel run my-tunnel

Example:

./cloudflared tunnel run campustransfer-website
🎉 Done!

Now open:

https://www.gubdi.com

Your localhost app is live 🚀

💡 Tips
Always run your local server first (like npm run dev)
Make sure port matches (3000, 5173, etc.)
Use subdomain if main domain has conflict
🧪 Test

If working:

URL opens your local app
No error in terminal
🔒 Important
Keep .json credential file safe
Do NOT share it publicly
🧹 Stop Tunnel

Press:

CTRL + C
✅ That’s it!

You can now make any localhost project live easily 🎉


---

If you want, I can also make:
- :contentReference[oaicite:0]{index=0}
- :contentReference[oaicite:1]{index=1}
- :contentReference[oaicite:2]{index=2}

Just tell me 👍
