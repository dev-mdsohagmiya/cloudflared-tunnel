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


user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared


user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared  tunnel login
A browser window should have opened at the following URL:

https://dash.cloudflare.com/argotunnel?aud=&callback=https%3A%2F%2Flogin.cloudfl
areaccess.org%2Fa12zA36XNP--rLD1a5MsZJ9OpbRutzSzIzYdvdRsAwg%3D

If the browser failed to open, please visit the URL above directly in your brows
er.
2026-04-02T16:55:26Z INF You have successfully logged in.
If you wish to copy your credentials to a server, they have been saved to:
C:\Users\user\.cloudflared\cert.pem


user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ cloudflared tunnel create campustransfer-website
bash: cloudflared: command not found

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel create campustransfer-website
Tunnel credentials written to C:\Users\user\.cloudflared\36158837-5094-42cb-8f9e
-b6a07b28b0c3.json. cloudflared chose this file based on where your origin certi
ficate was found. Keep this file secret. To revoke these credentials, delete the
 tunnel.

Created tunnel campustransfer-website with id 36158837-5094-42cb-8f9e-b6a07b28b0
c3

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel route dns campustransfer-website gubdi.com
Failed to add route: code: 1003, reason: Failed to create record gubdi.com with err An A, AAAA, or CNAME record with that host already exists. For more details, refer to <https://developers.cloudflare.com/dns/manage-dns-records/troubleshooting/records-with-same-name/>.

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel route dns campustransfer-website demo.gubdi.com
2026-04-02T16:58:13Z INF Added CNAME demo.gubdi.com which will route to this tunnel tunnelID=36158837-5094-42cb-8f9e-b6a07b28b0c3

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel route dns campustransfer-website www.gubdi.com
Failed to add route: code: 1003, reason: Failed to create record www.gubdi.com with err An A, AAAA, or CNAME record with that host already exists. For more details, refer to <https://developers.cloudflare.com/dns/manage-dns-records/troubleshooting/records-with-same-name/
>.

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel route dns campustransfer-website www.gubdi.com
2026-04-02T17:03:43Z INF www.gubdi.com is already configured to route to your tunnel tunnelID=36158837-5094-42cb-8f9e-b6a07b28b0c3

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ls -a
./  ../  cloudflared.exe*  config.yml

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel list
You can obtain more detailed information for each tunnel with `cloudflared tunnel info <name/uuid>`
ID                                   NAME                   CREATED              CONNECTIONS
36158837-5094-42cb-8f9e-b6a07b28b0c3 campustransfer-website 2026-04-02T16:56:38Z

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel run campustransfer-website live
"cloudflared tunnel run" accepts only one argument, the ID or name of the tunnel to run.
See 'cloudflared tunnel run --help'.

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel run campustransfer-website
2026-04-02T17:12:18Z INF Starting tunnel tunnelID=36158837-5094-42cb-8f9e-b6a07b28b0c3
2026-04-02T17:12:18Z INF Version 2026.3.0 (Checksum 59b12880b24af581cf5b1013db601c7d843b9b097e9c78aa5957c7f39f741885)
2026-04-02T17:12:18Z INF GOOS: windows, GOVersion: go1.24.13, GoArch: amd64
2026-04-02T17:12:18Z INF cloudflared will not automatically update on Windows systems.
2026-04-02T17:12:18Z INF Generated Connector ID: 034ddd07-d42e-4895-b45f-328ca52bb281
2026-04-02T17:12:18Z INF Initial protocol quic
2026-04-02T17:12:18Z INF ICMP proxy will use 192.168.0.100 as source for IPv4
2026-04-02T17:12:18Z INF ICMP proxy will use fe80::cfef:f8c2:e522:f129 in zone Ethernet as source for IPv6
2026-04-02T17:12:18Z INF cloudflared does not support loading the system root certificate pool on Windows. Please use --origin-ca-pool <PATH> to specify the path to the certificate pool
2026-04-02T17:12:18Z INF ICMP proxy will use 192.168.0.100 as source for IPv4
2026-04-02T17:12:18Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=0 event=0 ip=198.41.200.43
2026-04-02T17:12:18Z INF ICMP proxy will use fe80::cfef:f8c2:e522:f129 in zone Ethernet as source for IPv6
2026-04-02T17:12:18Z INF Starting metrics server on 127.0.0.1:20241/metrics
2026-04-02T17:12:19Z INF Registered tunnel connection connIndex=0 connection=5a0464d9-3293-4997-9421-45cdaa670b6d event=0 ip=198.41.200.43 location=bom10 protocol=quic
2026-04-02T17:12:19Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=1 event=0 ip=198.41.192.107
2026-04-02T17:12:20Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=2 event=0 ip=198.41.200.113
2026-04-02T17:12:20Z INF Registered tunnel connection connIndex=1 connection=20f076ab-fffa-47fb-b081-1eaa932c0944 event=0 ip=198.41.192.107 location=dac02 protocol=quic
2026-04-02T17:12:21Z INF Registered tunnel connection connIndex=2 connection=73edb145-5678-4821-8999-b4303fff1147 event=0 ip=198.41.200.113 location=bom11 protocol=quic
2026-04-02T17:12:21Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=3 event=0 ip=198.41.192.227
2026-04-02T17:12:22Z INF Registered tunnel connection connIndex=3 connection=1ad48f34-e789-48e2-8ed1-7e4f71bb02f8 event=0 ip=198.41.192.227 location=dac02 protocol=quic
2026-04-02T17:33:48Z INF Initiating graceful shutdown due to signal interrupt ...
2026-04-02T17:33:48Z ERR failed to run the datagram handler error="context canceled" connIndex=1 event=0 ip=198.41.192.107
2026-04-02T17:33:48Z ERR failed to serve tunnel connection error="accept stream listener encountered a failure while serving" connIndex=1 event=0 ip=198.41.192.107
2026-04-02T17:33:48Z ERR Serve tunnel error error="accept stream listener encountered a failure while serving" connIndex=1 event=0 ip=198.41.192.107
2026-04-02T17:33:48Z INF Retrying connection in up to 1s connIndex=1 event=0 ip=198.41.192.107
2026-04-02T17:33:48Z ERR Connection terminated connIndex=1
2026-04-02T17:33:48Z ERR failed to run the datagram handler error="context canceled" connIndex=2 event=0 ip=198.41.200.113
2026-04-02T17:33:48Z ERR failed to serve tunnel connection error="accept stream listener encountered a failure while serving" connIndex=2 event=0 ip=198.41.200.113
2026-04-02T17:33:48Z ERR Serve tunnel error error="accept stream listener encountered a failure while serving" connIndex=2 event=0 ip=198.41.200.113
2026-04-02T17:33:48Z INF Retrying connection in up to 1s connIndex=2 event=0 ip=198.41.200.113
2026-04-02T17:33:48Z ERR Connection terminated connIndex=2
2026-04-02T17:33:48Z ERR failed to run the datagram handler error="Application error 0x0 (remote)" connIndex=0 event=0 ip=198.41.200.43
2026-04-02T17:33:48Z ERR failed to serve tunnel connection error="accept stream listener encountered a failure while serving" connIndex=0 event=0 ip=198.41.200.43
2026-04-02T17:33:48Z ERR Serve tunnel error error="accept stream listener encountered a failure while serving" connIndex=0 event=0 ip=198.41.200.43
2026-04-02T17:33:48Z INF Retrying connection in up to 1s connIndex=0 event=0 ip=198.41.200.43
2026-04-02T17:33:48Z ERR Connection terminated connIndex=0
2026-04-02T17:33:49Z INF Unregistered tunnel connection connIndex=3 event=0 ip=198.41.192.227


user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ^C

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ^C

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ^C

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$  cloudflared tunnel create student.campustransfer.com
bash: cloudflared: command not found

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel create student.campustransfer.com
Tunnel credentials written to C:\Users\user\.cloudflared\fcfafd65-4315-43c0-8af1-59cc36725799.json. cloudflared chose this file based on where your origin certificate was found. Keep this file secret. To revoke these credentials, delete the tunnel.

Created tunnel student.campustransfer.com with id fcfafd65-4315-43c0-8af1-59cc36725799

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel route dns campustransfer-website student.gubdi.com
2026-04-02T17:40:15Z INF Added CNAME student.gubdi.com which will route to this tunnel tunnelID=36158837-5094-42cb-8f9e-b6a07b28b0c3

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel run campustransfer-website
2026-04-02T17:40:32Z INF Starting tunnel tunnelID=36158837-5094-42cb-8f9e-b6a07b28b0c3
2026-04-02T17:40:32Z INF Version 2026.3.0 (Checksum 59b12880b24af581cf5b1013db601c7d843b9b097e9c78aa5957c7f39f741885)
2026-04-02T17:40:32Z INF GOOS: windows, GOVersion: go1.24.13, GoArch: amd64
2026-04-02T17:40:32Z INF cloudflared will not automatically update on Windows systems.
2026-04-02T17:40:32Z INF Generated Connector ID: a94a57e0-328a-49e2-85ae-e59388f46d93
2026-04-02T17:40:32Z INF Initial protocol quic
2026-04-02T17:40:32Z INF ICMP proxy will use 192.168.0.100 as source for IPv4
2026-04-02T17:40:32Z INF ICMP proxy will use fe80::cfef:f8c2:e522:f129 in zone Ethernet as source for IPv6
2026-04-02T17:40:33Z INF cloudflared does not support loading the system root certificate pool on Windows. Please use --origin-ca-pool <PATH> to specify the path to the certificate pool
2026-04-02T17:40:33Z INF cloudflared does not support loading the system root certificate pool on Windows. Please use --origin-ca-pool <PATH> to specify the path to the certificate pool
2026-04-02T17:40:33Z INF ICMP proxy will use 192.168.0.100 as source for IPv4
2026-04-02T17:40:33Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=0 event=0 ip=198.41.192.107
2026-04-02T17:40:33Z INF ICMP proxy will use fe80::cfef:f8c2:e522:f129 in zone Ethernet as source for IPv6
2026-04-02T17:40:33Z INF Starting metrics server on 127.0.0.1:20241/metrics
2026-04-02T17:40:33Z INF Registered tunnel connection connIndex=0 connection=f9fbdf52-2770-4503-9c9c-45e1d040e8f1 event=0 ip=198.41.192.107 location=dac02 protocol=quic
2026-04-02T17:40:33Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=1 event=0 ip=198.41.200.193
2026-04-02T17:40:34Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=2 event=0 ip=198.41.192.57
2026-04-02T17:40:34Z INF Registered tunnel connection connIndex=1 connection=bd99e558-5955-486d-be97-b53ee6a125e0 event=0 ip=198.41.200.193 location=bom12 protocol=quic
2026-04-02T17:40:35Z INF Registered tunnel connection connIndex=2 connection=eb82b775-ff36-4888-9c1c-63593a9999e8 event=0 ip=198.41.192.57 location=dac02 protocol=quic
2026-04-02T17:40:35Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=3 event=0 ip=198.41.200.53
2026-04-02T17:40:36Z INF Registered tunnel connection connIndex=3 connection=267c7d51-e63a-47df-8c13-1b6d1430abc7 event=0 ip=198.41.200.53 location=bom12 protocol=quic
2026-04-02T17:45:11Z INF Initiating graceful shutdown due to signal interrupt ...
2026-04-02T17:45:11Z ERR failed to run the datagram handler error="context canceled" connIndex=0 event=0 ip=198.41.192.107
2026-04-02T17:45:11Z ERR failed to serve tunnel connection error="accept stream listener encountered a failure while serving" connIndex=0 event=0 ip=198.41.192.107
2026-04-02T17:45:11Z ERR Serve tunnel error error="accept stream listener encountered a failure while serving" connIndex=0 event=0 ip=198.41.192.107
2026-04-02T17:45:11Z INF Retrying connection in up to 1s connIndex=0 event=0 ip=198.41.192.107
2026-04-02T17:45:11Z ERR Connection terminated connIndex=0
2026-04-02T17:45:12Z ERR failed to run the datagram handler error="Application error 0x0 (remote)" connIndex=3 event=0 ip=198.41.200.53
2026-04-02T17:45:12Z ERR failed to serve tunnel connection error="accept stream listener encountered a failure while serving" connIndex=3 event=0 ip=198.41.200.53
2026-04-02T17:45:12Z ERR Serve tunnel error error="accept stream listener encountered a failure while serving" connIndex=3 event=0 ip=198.41.200.53
2026-04-02T17:45:12Z INF Retrying connection in up to 1s connIndex=3 event=0 ip=198.41.200.53
2026-04-02T17:45:12Z ERR Connection terminated connIndex=3


user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ^C

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel route dns campustransfer-website admin.gubdi.com
Failed to add route: code: 1003, reason: Failed to create record admin.gubdi.com with err An A, AAAA, or CNAME record with that host already exists. For more details, refer to <https://developers.cloudflare.com/dns/manage-dns-records/troubleshooting/records-with-same-nam
e/>.

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel route dns campustransfer-website admin.gubdi.com
2026-04-02T17:46:16Z INF Added CNAME admin.gubdi.com which will route to this tunnel tunnelID=36158837-5094-42cb-8f9e-b6a07b28b0c3

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel route dns campustransfer-website partner.gubdi.com
2026-04-02T17:49:22Z INF Added CNAME partner.gubdi.com which will route to this tunnel tunnelID=36158837-5094-42cb-8f9e-b6a07b28b0c3

user@DESKTOP-3O8KICQ MINGW64 /c/cloudflared
$ ./cloudflared tunnel run campustransfer-website
2026-04-02T17:49:34Z INF Starting tunnel tunnelID=36158837-5094-42cb-8f9e-b6a07b28b0c3
2026-04-02T17:49:34Z INF Version 2026.3.0 (Checksum 59b12880b24af581cf5b1013db601c7d843b9b097e9c78aa5957c7f39f741885)
2026-04-02T17:49:34Z INF GOOS: windows, GOVersion: go1.24.13, GoArch: amd64
2026-04-02T17:49:34Z INF cloudflared will not automatically update on Windows systems.
2026-04-02T17:49:34Z INF Generated Connector ID: e9993b5b-40e4-4a85-83c1-7e8e26acd3c0
2026-04-02T17:49:34Z INF Initial protocol quic
2026-04-02T17:49:34Z INF ICMP proxy will use 192.168.0.100 as source for IPv4
2026-04-02T17:49:34Z INF ICMP proxy will use fe80::cfef:f8c2:e522:f129 in zone Ethernet as source for IPv6
2026-04-02T17:49:34Z INF cloudflared does not support loading the system root certificate pool on Windows. Please use --origin-ca-pool <PATH> to specify the path to the certificate pool
2026-04-02T17:49:34Z INF cloudflared does not support loading the system root certificate pool on Windows. Please use --origin-ca-pool <PATH> to specify the path to the certificate pool
2026-04-02T17:49:34Z INF cloudflared does not support loading the system root certificate pool on Windows. Please use --origin-ca-pool <PATH> to specify the path to the certificate pool
2026-04-02T17:49:34Z INF cloudflared does not support loading the system root certificate pool on Windows. Please use --origin-ca-pool <PATH> to specify the path to the certificate pool
2026-04-02T17:49:34Z INF ICMP proxy will use 192.168.0.100 as source for IPv4
2026-04-02T17:49:34Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=0 event=0 ip=198.41.200.53
2026-04-02T17:49:34Z INF ICMP proxy will use fe80::cfef:f8c2:e522:f129 in zone Ethernet as source for IPv6
2026-04-02T17:49:34Z INF Starting metrics server on 127.0.0.1:20241/metrics
2026-04-02T17:49:35Z INF Registered tunnel connection connIndex=0 connection=f7977816-fae9-4b05-8d81-270b980111e2 event=0 ip=198.41.200.53 location=bom08 protocol=quic
2026-04-02T17:49:35Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=1 event=0 ip=198.41.192.7
2026-04-02T17:49:35Z INF Registered tunnel connection connIndex=1 connection=781f9681-a7f5-4945-92cf-932d71578abc event=0 ip=198.41.192.7 location=dac02 protocol=quic
2026-04-02T17:49:36Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=2 event=0 ip=198.41.192.47
2026-04-02T17:49:37Z INF Registered tunnel connection connIndex=2 connection=9f880216-cc24-48cf-b107-55d2d5bbb27a event=0 ip=198.41.192.47 location=dac02 protocol=quic
2026-04-02T17:49:37Z INF Tunnel connection curve preferences: [X25519MLKEM768 CurveP256] connIndex=3 event=0 ip=198.41.200.23
2026-04-02T17:49:38Z INF Registered tunnel connection connIndex=3 connection=4cc9d42b-dc7f-4ab6-8103-bda736115cac event=0 ip=198.41.200.23 location=bom08 protocol=quic
2026/04/02 23:50:54 Unsolicited response received on idle HTTP channel starting with "HTTP/1.1 400 Bad Request\r\n\r\n"; err=<nil>
2026/04/02 23:50:54 Unsolicited response received on idle HTTP channel starting with "HTTP/1.1 400 Bad Request\r\n\r\n"; err=<nil>
2026/04/02 23:53:32 Unsolicited response received on idle HTTP channel starting with "HTTP/1.1 400 Bad Request\r\n\r\n"; err=<nil>
2026/04/02 23:53:32 Unsolicited response received on idle HTTP channel starting with "HTTP/1.1 400 Bad Request\r\n\r\n"; err=<nil>
2026/04/02 23:53:32 Unsolicited response received on idle HTTP channel starting with "HTTP/1.1 400 Bad Request\r\n\r\n"; err=<nil>
2026/04/02 23:53:32 Unsolicited response received on idle HTTP channel starting with "HTTP/1.1 400 Bad Request\r\n\r\n"; err=<nil>
2026/04/02 23:54:24 Unsolicited response received on idle HTTP channel starting with "HTTP/1.1 400 Bad Request\r\n\r\n"; err=<nil>
2026/04/02 23:54:24 Unsolicited response received on idle HTTP channel starting with "HTTP/1.1 400 Bad Request\r\n\r\n"; err=<nil>
2026/04/02 23:54:24 Unsolicited response received on idle HTTP channel starting with "HTTP/1.1 400 Bad Request\r\n\r\n"; err=<nil>
2026/04/02 23:54:24 Unsolicited response received on idle HTTP channel starting with "HTTP/1.1 400 Bad Request\r\n\r\n"; err=<nil>
2026/04/02 23:54:24 Unsolicited response received on idle HTTP channel starting with "HTTP/1.1 400 Bad Request\r\n\r\n"; err=<nil>
2026-04-02T18:11:50Z ERR  error="Unable to reach the origin service. The service may be down or it may not be responding to traffic from cloudflared: dial tcp [::1]:3000: connectex: No connection could be made because the target machine actively refused it." connIndex=3
event=1 ingressRule=0 originService=http://localhost:3000
2026-04-02T18:11:50Z ERR Request failed error="Unable to reach the origin service. The service may be down or it may not be responding to traffic from cloudflared: dial tcp [::1]:3000: connectex: No connection could be made because the target machine actively refused it.
" connIndex=3 dest=https://www.gubdi.com/ event=0 ip=198.41.200.23 type=http
2026-04-02T18:15:17Z ERR  error="Unable to reach the origin service. The service may be down or it may not be responding to traffic from cloudflared: dial tcp [::1]:3000: connectex: No connection could be made because the target machine actively refused it." connIndex=1
event=1 ingressRule=0 originService=http://localhost:3000
2026-04-02T18:15:17Z ERR Request failed error="Unable to reach the origin service. The service may be down or it may not be responding to traffic from cloudflared: dial tcp [::1]:3000: connectex: No connection could be made because the target machine actively refused it.
" connIndex=1 dest=https://www.gubdi.com/meta.json event=0 ip=198.41.192.7 type=http
2026-04-02T18:15:41Z ERR  error="Unable to reach the origin service. The service may be down or it may not be responding to traffic from cloudflared: dial tcp [::1]:3000: connectex: No connection could be made because the target machine actively refused it." connIndex=1
event=1 ingressRule=0 originService=http://localhost:3000
2026-04-02T18:15:41Z ERR Request failed error="Unable to reach the origin service. The service may be down or it may not be responding to traffic from cloudflared: dial tcp [::1]:3000: connectex: No connection could be made because the target machine actively refused it.
" connIndex=1 dest=https://www.gubdi.com/ event=0 ip=198.41.192.7 type=http
2026-04-02T18:15:46Z INF Initiating graceful shutdown due to signal interrupt ...
2026-04-02T18:15:46Z ERR failed to run the datagram handler error="context canceled" connIndex=2 event=0 ip=198.41.192.47
2026-04-02T18:15:46Z ERR failed to serve tunnel connection error="accept stream listener encountered a failure while serving" connIndex=2 event=0 ip=198.41.192.47
2026-04-02T18:15:46Z ERR Serve tunnel error error="accept stream listener encountered a failure while serving" connIndex=2 event=0 ip=198.41.192.47
2026-04-02T18:15:46Z INF Retrying connection in up to 1s connIndex=2 event=0 ip=198.41.192.47
2026-04-02T18:15:46Z ERR failed to run the datagram handler error="context canceled" connIndex=1 event=0 ip=198.41.192.7
2026-04-02T18:15:46Z ERR Connection terminated connIndex=2
2026-04-02T18:15:46Z ERR failed to serve tunnel connection error="accept stream listener encountered a failure while serving" connIndex=1 event=0 ip=198.41.192.7
2026-04-02T18:15:46Z ERR Serve tunnel error error="accept stream listener encountered a failure while serving" connIndex=1 event=0 ip=198.41.192.7
2026-04-02T18:15:46Z INF Retrying connection in up to 1s connIndex=1 event=0 ip=198.41.192.7
2026-04-02T18:15:46Z ERR Connection terminated connIndex=1
2026-04-02T18:15:46Z ERR failed to run the datagram handler error="Application error 0x0 (remote)" connIndex=3 event=0 ip=198.41.200.23
2026-04-02T18:15:46Z ERR failed to serve tunnel connection error="accept stream listener encountered a failure while serving" connIndex=3 event=0 ip=198.41.200.23
2026-04-02T18:15:46Z ERR failed to run the datagram handler error="Application error 0x0 (remote)" connIndex=0 event=0 ip=198.41.200.53
2026-04-02T18:15:46Z ERR Serve tunnel error error="accept stream listener encountered a failure while serving" connIndex=3 event=0 ip=198.41.200.23
2026-04-02T18:15:46Z ERR failed to serve tunnel connection error="accept stream listener encountered a failure while serving" connIndex=0 event=0 ip=198.41.200.53
2026-04-02T18:15:46Z INF Retrying connection in up to 1s connIndex=3 event=0 ip=198.41.200.23
2026-04-02T18:15:46Z ERR Serve tunnel error error="accept stream listener encountered a failure while serving" connIndex=0 event=0 ip=198.41.200.53
2026-04-02T18:15:46Z ERR Connection terminated connIndex=3
2026-04-02T18:15:46Z INF Retrying connection in up to 1s connIndex=0 event=0 ip=198.41.200.53
2026-04-02T18:15:46Z ERR Connection terminated connIndex=0
2026-04-02T18:15:46Z ERR no more connections active and exiting
2026-04-02T18:15:46Z INF Tunnel server stopped
2026-04-02T18:15:46Z ERR icmp router terminated error="context canceled"
2026-04-02T18:15:46Z INF Metrics server stopped

