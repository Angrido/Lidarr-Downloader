# 🎵 Lidarr YouTube Downloader

<div align="center">

![Python](https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-v3-blue?logo=docker&logoColor=white)
![Lidarr](https://img.shields.io/badge/Integration-Lidarr-green?logo=lidarr&logoColor=white)
![CasaOS](https://img.shields.io/badge/CasaOS-Ready-orange)
![License](https://img.shields.io/badge/License-Educational-red)

**The missing link between your Lidarr library and YouTube's vast music catalog.**

[Features](#-features) • [Quick Start](#-quick-start) • [Installation](#-installation)

</div>

---

## 🌟 What is this?

Ever had albums sitting in your Lidarr "Missing" list with no torrent seeds? **This tool fixes that.**

Lidarr YouTube Downloader is a lightweight web application that:
- 🔍 Automatically fetches your missing albums from Lidarr
- 🎬 Searches and downloads them from YouTube
- 🎧 Converts to high-quality MP3 with proper ID3 tags
- 📂 Auto-imports them back into Lidarr

**No torrents. No Usenet. Just YouTube and your music library.**

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 🎯 Smart Integration
- **One-Click Sync** with Lidarr API
- **Automatic Artist Rescanning** after downloads
- **Zero Manual Work** - Set it and forget it

</td>
<td width="50%">

### 🚀 Modern Tech Stack
- **Python 3.11** with latest `yt-dlp`
- **Bypasses YouTube 403 blocks** automatically
- **Real-time progress tracking** via WebUI

</td>
</tr>
<tr>
<td width="50%">

### 🏷️ Professional Quality
- **MP3 Conversion** with proper bitrate
- **ID3 Metadata Tagging** (Artist, Album, Track)
- **Smart File Naming** (`01 - Song Title.mp3`)

</td>
<td width="50%">

### 🐳 Deployment Ready
- **Docker Optimized** for CasaOS
- **Lightweight** - Minimal resource usage
- **Clean UI** - Fast, no bloat

</td>
</tr>
</table>

---

## 🚀 Quick Start

### Prerequisites

- ✅ Lidarr instance running (any version)
- ✅ Docker or CasaOS installed
- ✅ 5 minutes of your time

### 🎯 TL;DR Installation

```bash
docker run -d \
  --name lidarr-downloader \
  -p 5005:5000 \
  -v /DATA/Downloads:/DATA/Downloads \
  -e LIDARR_URL="http://YOUR_SERVER_IP:8686" \
  -e LIDARR_API_KEY="YOUR_API_KEY" \
  -e DOWNLOAD_PATH="/DATA/Downloads" \
  angrido/lidarr-downloader:latest
```

**Then open:** `http://YOUR_SERVER_IP:5005`

---

## 📦 Installation

<details>
<summary><b>🏠 Option 1: CasaOS (Click to expand)</b></summary>

### Step-by-Step Guide

1. **Open CasaOS Dashboard**
   - Navigate to your CasaOS web interface

2. **Add Custom App**
   - Click the **+** button
   - Select **"Install a Custom App"**

3. **Basic Configuration**

   | Field | Value |
   |-------|-------|
   | Docker Image | `angrido/lidarr-downloader:latest` |
   | App Name | `Lidarr Downloader` |
   | WebUI Port | `5000` |

4. **Network Settings**
   - **Host Port:** `5005` *(or any available port)*
   - **Container Port:** `5000`

5. **Volume Mapping** ⚠️ *Critical*
   - **Host Path:** `/DATA/Downloads`
   - **Container Path:** `/DATA/Downloads`
   
   > 💡 This is where your music files will be saved

6. **Environment Variables**

   | Variable | Example Value | Where to Find |
   |----------|---------------|---------------|
   | `LIDARR_URL` | `http://192.168.1.100:8686` | Use your **actual server IP** (not localhost!) |
   | `LIDARR_API_KEY` | `abc123def456...` | Lidarr → Settings → General → Security |
   | `DOWNLOAD_PATH` | `/DATA/Downloads` | Must match container path above |

7. **Deploy!**
   - Click "Install" and wait for the container to start
   - Access at: `http://YOUR_SERVER_IP:5005`

</details>

<details>
<summary><b>🐳 Option 2: Docker Compose (Click to expand)</b></summary>

Create a `docker-compose.yml` file:

```yaml
version: '3.8'

services:
  lidarr-downloader:
    image: angrido/lidarr-downloader:latest
    container_name: lidarr-downloader
    restart: unless-stopped
    ports:
      - "5005:5000"
    volumes:
      - /DATA/Downloads:/DATA/Downloads
    environment:
      LIDARR_URL: http://192.168.1.XXX:8686
      LIDARR_API_KEY: your_api_key_here
      DOWNLOAD_PATH: /DATA/Downloads
```

Then run:
```bash
docker-compose up -d
```

</details>

<details>
<summary><b>⚙️ Option 3: Advanced Docker CLI (Click to expand)</b></summary>

Full command with all options:

```bash
docker run -d \
  --name lidarr-downloader \
  --restart unless-stopped \
  -p 5005:5000 \
  -v /DATA/Downloads:/DATA/Downloads \
  -e LIDARR_URL="http://192.168.1.XXX:8686" \
  -e LIDARR_API_KEY="YOUR_API_KEY" \
  -e DOWNLOAD_PATH="/DATA/Downloads" \
  --log-opt max-size=10m \
  --log-opt max-file=3 \
  angrido/lidarr-downloader:latest
```

**Pro Tips:**
- Add `--network host` if container can't reach Lidarr
- Use `-v /path/to/logs:/app/logs` for persistent logs
- Check logs with: `docker logs lidarr-downloader`

</details>

---

## 🎮 How to Use

1. **Open the Web Interface**
   ```
   http://YOUR_SERVER_IP:5005
   ```

2. **Click "Fetch Missing Albums"**
   - The tool queries Lidarr's API
   - Missing albums appear in a clean list

3. **Download!**
   - Click the download button next to any album
   - Watch the real-time progress bar
   - Files are automatically tagged and imported to Lidarr

4. **Enjoy Your Music** 🎶
   - Check Lidarr - the album should now be marked as "Downloaded"


## 🔐 Configuration Reference

| Environment Variable | Required | Default | Description |
|---------------------|----------|---------|-------------|
| `LIDARR_URL` | ✅ Yes | - | Full URL to your Lidarr instance (e.g., `http://192.168.1.50:8686`) |
| `LIDARR_API_KEY` | ✅ Yes | - | API key from Lidarr Settings → General → Security |
| `DOWNLOAD_PATH` | ✅ Yes | - | Directory where music files will be saved (must be accessible by both containers) |


---

## ⚠️ Disclaimer

This tool is intended for **educational purposes** and for managing your **personal music library**.

**You are responsible for:**
- ✅ Complying with YouTube's Terms of Service
- ✅ Respecting copyright laws in your jurisdiction
- ✅ Only downloading content you have the right to access

**The developer assumes no liability for misuse of this software.**


---

## 💖 Support

Found this useful? Consider:
- ⭐ **Starring** this repository
- 🐛 **Reporting bugs** via Issues
- 💡 **Suggesting features** you'd like to see

---

<div align="center">

**Made with ❤️ and Python**

*Bridging the gap between Lidarr and YouTube, one album at a time.*

</div>
