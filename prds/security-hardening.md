# PRD: OpenClaw Security Hardening

> Drop this file into your agent's chat and say: "Execute this security PRD"
> It will harden your server following each step.
> **Updated for OpenClaw v2026.3.13**

---

## ⚠️ Why This Is Urgent

In February 2026, a critical vulnerability (**CVE with CVSS 8.8**) was discovered in OpenClaw instances exposed on the internet. Over **30,000 instances** were identified as vulnerable before the patch in version 2026.2.12. Servers without basic protection were compromised — data exfiltrated, API keys stolen, agents used for spam.

Additionally: OpenClaw servers exposed on the internet receive 1,000+ brute force attempts per day. Without protection, anyone can access your agent and your data.

This guide protects you against all known attack vectors.

## Context for v2026.3.2+

**WebSocket is now loopback-only by default.** The OpenClaw web panel (`http://IP:18789`) only accepts connections from `127.0.0.1` — meaning only from within the server itself. For remote access, you need Cloudflare Tunnel (covered below).

### Security improvements in v2026.3.13

Version 2026.3.13 brought a significant package of security fixes:

- **Device pairing single-use:** Setup codes are now single-use — they cannot be reused to gain access. Each `openclaw qr` or `/pair` generates a code that expires on first scan (or in a few minutes if unused). Trying to use the same QR twice → "code expired" error. Generate a new one for each pairing. ⚠️ Never share QR via screenshot — whoever scans first gets access.
- **Exec approvals hardened:** Several ways to bypass command analysis were fixed (Unicode zero-width, backslash-newline, pnpm wrappers, Perl/Ruby -r/-I flags)
- **WebSocket preauth:** Unauthenticated handshake window reduced; oversized frames rejected before parsing
- **Proxy attachments:** 5MB limit restored for files persisted by the browser proxy
- **GIT_EXEC_PATH blocked:** Inherited environment variable can no longer redirect Git helpers
- **Webhook secrets:** Feishu, LINE and Zalo with stricter signature validation

> ✅ No specific actions needed for students beyond keeping OpenClaw updated. Fixes are automatic after `npm update -g openclaw`.

---

## Tasks (execute in order)

### 1. Telegram Allowlist (CRITICAL — do FIRST)

> 🔴 **Order matters:** Configure dmPolicy BEFORE anything else. UFW and other protections come after.

Verify that OpenClaw is configured with `dmPolicy: "allowlist"` and that ONLY authorized IDs are in the list.

```bash
# Check current config
cat /root/.openclaw/openclaw.json | grep -A5 dmPolicy
```

If it's "open", change IMMEDIATELY to "allowlist" with the correct IDs.

> **Why first?** UFW protects the server port, but Telegram is an OUTBOUND connection — there's no port to block. If dmPolicy is "open", anyone who discovers your bot's username can command your agent, even with UFW active. These are two different layers of protection.

### 2. Firewall (UFW)

```bash
# Install and configure
sudo apt install -y ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw --force enable
sudo ufw status
```

### 3. Fail2ban (SSH protection)

```bash
# Install
sudo apt install -y fail2ban

# Configure
sudo cat > /etc/fail2ban/jail.local << 'EOF'
[sshd]
enabled = true
port = ssh
filter = sshd
logpath = /var/log/auth.log
maxretry = 5
bantime = 3600
findtime = 600
EOF

# Enable
sudo systemctl enable fail2ban
sudo systemctl restart fail2ban

# Verify
sudo fail2ban-client status sshd
```

### 4. Cloudflare Tunnel (secure remote access)

> 🔒 **New in v2026.3.2:** The OpenClaw panel WebSocket now only accepts connections from `127.0.0.1` (loopback). To access the panel remotely (Mission Control, dashboards), you **need** Cloudflare Tunnel. There's no shortcut.

Use Cloudflare Tunnel to expose web services (Mission Control, dashboards) without opening ports:

```bash
# Install cloudflared
curl -L https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb -o cloudflared.deb
sudo dpkg -i cloudflared.deb

# Authenticate
cloudflared tunnel login

# Create tunnel
cloudflared tunnel create my-tunnel

# Configure (example for app on port 18789 — OpenClaw panel)
cat > ~/.cloudflared/config.yml << 'EOF'
tunnel: my-tunnel
credentials-file: /root/.cloudflared/<TUNNEL_ID>.json

ingress:
  - hostname: panel.mydomain.com
    service: http://127.0.0.1:18789
  - service: http_status:404
EOF

# Run as service
cloudflared service install
systemctl enable cloudflared
systemctl start cloudflared
```

**Why:**
- Zero ports exposed on the internet — tunnel makes an OUTBOUND connection
- Server stays "invisible" (no public IP exposed)
- Automatic SSL/TLS via Cloudflare
- Free DDoS protection included
- NEVER use `0.0.0.0` — always `127.0.0.1` + tunnel

### 5. Application Ports

If you have web applications running (Mission Control, dashboards, etc.):
- Change binding from `0.0.0.0` to `127.0.0.1`
- Use Cloudflare Tunnel (above) for external access
- NEVER expose ports directly on the internet

### 6. SSH Hardening

```bash
# Check if root login with password is active
grep "PermitRootLogin" /etc/ssh/sshd_config
```

Ideal: `PermitRootLogin prohibit-password` (SSH key only, no password)

### 7. Credentials: Audit with `openclaw secrets`

**The problem:** The 2026.2.12 CVE exploited hardcoded API keys in configuration files. If someone accesses your server, they get ALL your keys at once.

**Starting from v2026.3.2**, OpenClaw has the `openclaw secrets` command to manage credentials securely. **Use this command instead of manually editing .env.**

**Step 1 — Audit (discover if there are exposed keys):**

```bash
# See everything exposed in your files
openclaw secrets audit
```

This command scans all workspace and configuration files, looking for hardcoded API key patterns. If it finds anything, it lists the exact path and line.

**Step 2 — Migrate to the secure system:**

```bash
# Automatically migrate to the secure secrets manager
openclaw secrets apply
```

This command moves found credentials to OpenClaw's secure vault, where they are encrypted. Original files have the keys removed automatically.

**Step 3 — Verify everything was migrated:**

```bash
# Run audit again — should return clean
openclaw secrets audit
# Expected output: "✅ No exposed credentials found"
```

> ℹ️ **Backward compatibility:** If you already have a manual `.env` with keys, `openclaw secrets apply` reads from there too and migrates to the secure system. After migration, the manual `.env` can be removed.

**Quarterly rotation:** Every 3 months, generate new keys in the provider consoles (Anthropic, OpenAI, Telegram). `openclaw secrets` handles the update:

```bash
openclaw secrets set ANTHROPIC_API_KEY=sk-ant-new-key-here
```

### 8. Sync systemd + secrets (common trap!)

When changing any credential, systemd needs to know:

```bash
# 1. Update the secret
openclaw secrets set KEY_NAME=new-value

# 2. Update the systemd override if it has a hard-coded variable
sudo systemctl edit openclaw

# 3. Reload and restart
sudo systemctl daemon-reload
sudo systemctl restart openclaw
```

**Why:** The systemd override takes priority over the secrets system. If you only change the secret and the override has the old value, it will keep using the old one. Many people lose hours debugging this.

---

## Final Checklist

- [ ] **dmPolicy = allowlist** (FIRST — before UFW)
- [ ] UFW active
- [ ] Fail2ban active
- [ ] Cloudflare Tunnel configured (panel is loopback-only in v2026.3.2)
- [ ] Ports on 127.0.0.1 (not 0.0.0.0)
- [ ] SSH hardened (key-only)
- [ ] `openclaw secrets audit` — zero results
- [ ] `openclaw secrets apply` — credentials migrated to secure vault
- [ ] Quarterly rotation scheduled
- [ ] systemd + secrets synced

## Expected Result

Server hardened against the most common attacks, including the CVE 2026.2.12 vector. **9 layers of protection** active. Report status of each item.

## Stay Updated

Run periodically to ensure you're on the latest version (with all security patches):

```bash
npm update -g openclaw
openclaw gateway restart
openclaw gateway status
```

> ✅ Version 2026.3.13 is the most robust security package to date — includes fixes for exec approvals, device pairing, WebSocket and webhooks.
