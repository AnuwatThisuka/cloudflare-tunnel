# 🌐 Cloudflare Tunnel via Docker (MacOS)

## 🧩 Step-by-step

1. Install `cloudflared`:

   ```bash
   brew install cloudflared
   ```

2. Login to Cloudflare:

   ```bash
   cloudflared tunnel login
   ```

3. Create a tunnel:

   ```bash
   cloudflared tunnel create mytunnel
   ```

4. Map DNS:

   ```bash
   cloudflared tunnel route dns mytunnel rpi.example.com
   ```

5. Copy credentials:

   ```bash
   cp ~/.cloudflared/*.json ./credentials.json
   ```

6. Edit [config.yml](config.yml) as needed:
   - Change `hostname` to your desired domain
   - Change `service` to the endpoint you want the tunnel to reach

7. Start the tunnel:

   ```bash
   docker compose up -d
   ```

8. Access via browser:

   ```url
   https://rpi.example.com
   ```

## 📝 File Details

### [config.yml](config.yml)

This file defines the tunnel configuration:

- `tunnel`: The name of the created tunnel
- `credentials-file`: Location of the credentials file in the container
- `ingress`: Defines routing rules

### [docker-compose.yml](docker-compose.yml)

This file configures the container:

- Uses the `cloudflare/cloudflared:latest` image
- Mounts config and credentials files into the container
- Sets restart policy to always

## 🔄 Management

### Viewing logs

```bash
docker logs cloudflared
```

### Stopping the service

```bash
docker compose down
```

### Updating the image

```bash
docker compose pull
docker compose up -d
```
