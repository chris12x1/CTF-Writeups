## 📸 Screenshots — Flare × SANS × WiCyS CTF 2026

Supporting images for the [Flare × WiCyS CTF write-up](../README.md) — Solo solve, flag captured: `flare{pantal0n3s_g0t_pantsed_2026}`

| File | Description |
|---|---|
| `01-recon.png` | Leak site homepage — victim list with leak countdown timers |
| `02-encoded_message.png` | Base64-encoded HTML comment found in the homepage's page source |
| `03-robots_txt.png` | `robots.txt` disallowing `/api.php` and `/admin.php` |
| `04-api_php.png` | `api.php` error response leaking the full list of valid API actions |
| `05-action_status.png` | `api.php?action=status` — panel telemetry and online operators |
| `06-action_payloads.png` | `api.php?action=payloads` — staged malware builds per target |
| `07-action_exfil.png` | `api.php?action=exfil` — completed exfiltration job history |
| `08-exfil_sh.png` | Contents of the leaked `.exfil.sh` script (panel URL + API key) |
| `09-hidden_file.png` | Directory listing showing `.exfil.sh` inside the published leak archive |
| `10-admin_panel.png` | `admin.php` login form |
| `11-conversation.png` | `api.php?action=messages&conversation_id=1` — internal crew chat log |
| `12-leaked_password.png` | Crew member sharing a base64-"encoded" password in chat |
| `13-decoded_password.png` | CyberChef decoding the password from Base64 |
| `14-admin_dashboard_flag.png` | Authenticated admin dashboard showing the recovered flag |

> ⚠️ **Redaction note:** This CTF was a single-run public event, officially closed by WiCyS with the flag publicly disclosed in their announcement. Images are shown redacted 

