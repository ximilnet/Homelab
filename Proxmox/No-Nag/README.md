# Proxmox No-Nag Fix

Remove the "No valid subscription" popup on Proxmox 9 permanently.

## Fix Repositories

```bash
rm /etc/apt/sources.list.d/pve-enterprise.sources
```

```bash
cat > /etc/apt/sources.list.d/proxmox.sources << 'EOF'
Types: deb
URIs: http://download.proxmox.com/debian/pve
Suites: trixie
Components: pve-no-subscription
Signed-By: /usr/share/keyrings/proxmox-archive-keyring.gpg
EOF
```

## Remove the Popup

```bash
cp /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js{,.bak}

sed -i "s/data.status.toLowerCase() !== 'active'/data.status.toLowerCase() === 'active'/" \
   /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js

systemctl restart pveproxy
```

## Make it Permanent (APT Hook)

```bash
mkdir -p /etc/apt/scripts
cat > /etc/apt/scripts/no-nag-fix.sh << 'EOF'
#!/bin/bash
TARGET="/usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js"
if [ -f "$TARGET" ]; then
  sed -i "s/data.status.toLowerCase() !== 'active'/data.status.toLowerCase() === 'active'/" "$TARGET"
  systemctl restart pveproxy 2>/dev/null || true
fi
EOF
chmod +x /etc/apt/scripts/no-nag-fix.sh
```

```bash
cat > /etc/apt/apt.conf.d/99no-nag << 'EOF'
DPkg::Post-Invoke { "/etc/apt/scripts/no-nag-fix.sh"; };
EOF
```

```bash
/etc/apt/scripts/no-nag-fix.sh
```

## ⚠️ Note
For homelab and personal use only.

## 📺 Video Tutorial
[Watch on YouTube](YOUR_LINK_HERE)
