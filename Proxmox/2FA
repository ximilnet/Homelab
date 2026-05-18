# Proxmox 2FA Setup (TOTP)

Enable Two-Factor Authentication on Proxmox VE 8+ to protect 
your server even if your password is stolen.

## What You'll Need

- Proxmox VE 7 or newer
- Authenticator app on your phone:
  - [Aegis](https://getaegis.app/) (Android - recommended, open source)
  - [Google Authenticator](https://googleauthenticator.net/)
  - [Authy](https://authy.com/)

---

## Step 1 — Enable TOTP for Your Account

1. Log into Proxmox Web GUI
2. Go to **Datacenter** → **Permissions** → **Two Factor**
3. Click **Add** → **TOTP**
4. Scan the QR code with your authenticator app
5. Enter the 6-digit code from your app to verify
6. Click **Add**

> ⚠️ Note: The CLI command `pveum user tfa set` is outdated 
> in Proxmox VE 7+. Always use the Web GUI for 2FA setup.

---

## Step 2 — Test It Works

1. Log out of Proxmox completely
2. Log back in with your username and password
3. You should now see a **second factor prompt**
4. Enter the 6-digit code from your app
5. You're in ✅

---

## Step 3 — Save Your Recovery Keys ⚠️

When setting up 2FA, Proxmox generates **recovery keys**.
These are one-time-use codes to bypass 2FA if you lose your phone.

**Save them in one of these places:**
- Password manager (Bitwarden, KeePass)
- Printed paper in a physical safe
- Encrypted USB drive

**Never save them in:**
- Google Docs
- Email
- Unencrypted cloud storage

---

## Step 4 — Enforce 2FA for All Users (Proxmox 8+)

Force every user to have 2FA — no exceptions:

1. Go to **Datacenter** → **Options**
2. Find **Two Factor Policy**
3. Set it to **Required**

From this point any user without 2FA enrolled 
cannot log into the GUI at all.

---

## Optional — WebAuthn (Hardware Keys)

For even stronger security, Proxmox supports **WebAuthn** 
with hardware keys like YubiKey.

- Phishing-proof — tied to the specific domain
- Works with any FIDO2 key
- Setup guide coming soon

---

## Security Checklist

| Step | Done |
|---|---|
| TOTP enabled on admin account | ☐ |
| Recovery keys saved offline | ☐ |
| Tested login with 2FA prompt | ☐ |
| 2FA policy set to Required | ☐ |
| Not using root for daily tasks | ☐ |

---

## 📺 Video Tutorial
[Watch on YouTube](YOUR_YOUTUBE_LINK_HERE)

## ⚠️ Note
This guide is for homelab and personal use. 
If giving others access to your Proxmox, enforcing 
2FA at the datacenter level is strongly recommended.
