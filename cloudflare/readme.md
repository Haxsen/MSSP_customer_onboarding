Use the following commands to setup cloudflare tunnel:
```bash
curl -L https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64 -o cloudflared
chmod +x cloudflared
```

Start the tunnel:
```bash
WSL_IP=$(hostname -I | awk '{print $1}')
./cloudflared tunnel --url https://$WSL_IP:443 --no-tls-verify
```

