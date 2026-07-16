# YouTube Downloader

A clean, self-hosted YouTube downloader with a minimal dark UI. Paste a link, pick your settings, and download straight to your machine — no accounts, no tracking, no nonsense.

---

## Features

- Real-time download progress with live percentage feedback
- Resolution picker — Best, 4K, 1440p, 1080p, 720p
- Codec picker — H.264, H.265, VP9, AV1, or MP3 (audio only)
- Video preview showing thumbnail, title, and formatted duration
- Automatic filename sanitization from the video title

---

## Requirements

| Tool | Install |
|------|---------|
| [Node.js](https://nodejs.org) | Download from nodejs.org |
| yt-dlp | `winget install yt-dlp` |
| FFmpeg | Installed automatically alongside yt-dlp |

---

## Setup

Run once to install Node dependencies:

```bash
npm install
```

---

## Usage

```bash
node server.js
```

Then open `index.html` in your browser, paste a YouTube URL, wait for the preview to load, choose your resolution and codec, and hit **Fetch & Download**.

---

## Resolution & Codec Notes

| Resolution | Codec Behavior |
|------------|----------------|
| Best / 4K / 1440p | Downloads in VP9 or AV1 — YouTube does not offer H.264 above 1080p |
| 1080p / 720p | Codec selection applies (H.264, H.265, VP9, AV1) |
| MP3 | Extracts high-quality audio regardless of codec setting |

---

## Project Structure

```
├── server.js       # Express backend, proxies yt-dlp calls
├── index.html      # Frontend UI
├── package.json
└── README.md
```

> **Note:** This tool is intended for personal use. Respect copyright and YouTube's Terms of Service when downloading content.
