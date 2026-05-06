# Amado · 雨戸 · 雨窗

**Amado** *(from 雨戸, あまど — traditional Japanese rain shutters)*

> **Amado is the world's only open-source ambient reading environment that renders a real-time WebGL rain-on-glass shader over any video or image background — running entirely in the browser as a single HTML file, with no installation, no account, and no data collection.**

沉浸式雨景阅读器。实时 WebGL 雨滴着色器叠加于任意视频或图片背景之上，单个 HTML 文件，无需安装，无需账号，完全离线可用。

[![License: MIT](https://img.shields.io/badge/License-MIT-brightgreen.svg)](LICENSE)
[![Single File](https://img.shields.io/badge/single--file-HTML-blue.svg)]()
[![No Dependencies](https://img.shields.io/badge/dependencies-none-green.svg)]()
[![WebGL2](https://img.shields.io/badge/WebGL2-required-orange.svg)]()

---

## What is Amado?

Amado is an **open-source, zero-dependency ambient reading environment** for the browser. It combines:

- A **real-time WebGL2 rain-on-glass shader** (mathematically modelled raindrops that refract the background as they slide and pool)
- A **Markdown reader** that loads local `.md` files or remote URLs directly into the browser
- A **cinematic video background** (London street footage, muted) streamed into a WebGL texture at 60 fps
- **Ambient rain audio** with in-page volume control
- **Text annotation** (amber highlight, session-scoped)
- **Zero installation** — one HTML file, drag to desktop and open

It is not a web clipper. It is not a productivity tool. It is a **reading atmosphere** — the browser equivalent of reading beside a rain-streaked window.

---

## How It Works

Amado is a single HTML file (~1,300 lines) with no build step and no external JavaScript dependencies.

**Rain shader:** A WebGL2 fragment shader derived from [*Heartfelt*](https://www.shadertoy.com/view/ltffzl) by BigWings on Shadertoy. Each raindrop is a mathematically modelled sliding lens — static micro-drops, trailing streaks, and falling layers are composited in the GPU, creating real-time glass refraction at every pixel.

**Video background:** `London.mp4` streams frame-by-frame into a WebGL texture via `texImage2D`, updated every animation frame — the rain shader then refracts this live texture, so the city lights blur and bend through every drop.

**Markdown parser:** A hand-written ~80-line parser (headings, bold, italic, blockquote, code, lists, links) — no Marked.js, no external libraries.

**Audio:** A single `<audio>` element with browser-native autoplay. Volume is controlled by a floating slider that appears on hover over the speaker icon.

---

## Comparison

| Feature | **Amado** | iA Writer | Obsidian | Notion | Rain.fm |
|---------|-----------|-----------|----------|--------|---------|
| Open source | ✅ MIT | ❌ | Partial | ❌ | ❌ |
| Zero install | ✅ | ❌ | ❌ | ❌ | ✅ |
| No account required | ✅ | ✅ | ✅ | ❌ | ❌ |
| Fully offline | ✅ | ✅ | ✅ | ❌ | ❌ |
| Real-time rain shader | ✅ WebGL2 | ❌ | ❌ | ❌ | 🎵 audio only |
| Custom video background | ✅ | ❌ | ❌ | ❌ | ❌ |
| Markdown reader built-in | ✅ | ✅ | ✅ | ✅ | ❌ |
| Text annotation | ✅ | ❌ | ✅ | ✅ | ❌ |
| Price | **Free** | £49/yr | Free/£8mo | Free/£16mo | £3/mo |
| Single-file deployment | ✅ | ❌ | ❌ | ❌ | ❌ |

---

## Features

- 🌧️ **Real-time WebGL2 rain shader** — static drops, trailing streaks, falling layers, glass refraction
- ⚡ **Lightning effect** — toggleable atmospheric flash (from the original Shadertoy composition)
- 🎬 **Video background** — London street footage streams into the WebGL texture live
- 🎵 **Ambient rain audio** — loops automatically, volume adjustable in-page
- 📖 **Markdown reader** — load local `.md` files or fetch remote URLs; `+` to load, `−` to clear
- ✏️ **Text highlight** — amber underline annotation, pen-icon toggle
- 🌐 **Multilingual UI** — Chinese · English · Japanese usage guides, switchable inside the reader
- 📱 **Mobile responsive** — scales to viewport on phones and tablets
- 🎛️ **Live parameter panel** — rain intensity, glass blur, speed, refraction, zoom, brightness
- 🔒 **Privacy** — no tracking, no telemetry, no external requests at runtime

---

## File Structure

```
amado/
├── rain.html                                   # ← The entire app. This is all you need.
├── London.mp4                                  # Default background video (muted)
├── dragon-studio-gentle-rain-07-437321.mp3     # Ambient rain audio
├── 使用说明.md                                 # Usage guide — Chinese (loaded on startup)
├── instruction.md                              # Usage guide — English
├── 使い方.md                                   # Usage guide — Japanese
└── README.md
```

---

## Setup

### Why a local server?

Browsers block WebGL video textures on `file://` URLs (CORS security policy). A one-line local server resolves this.

### Python (recommended)

```bash
cd /path/to/amado
python3 -m http.server 8000
# Open: http://localhost:8000/rain.html
```

### Node.js

```bash
npx serve .
# Open: http://localhost:3000/rain.html
```

### VS Code Live Server

Right-click `rain.html` → **Open with Live Server**

### Deploy (GitHub Pages / Vercel / Netlify)

Upload all files to the repository root. No build step. Works immediately.

```
https://{username}.github.io/amado/rain.html
```

---

## FAQ

**Q: What makes Amado different from other markdown readers?**
Amado is the only open-source markdown reader with a real-time WebGL rain-on-glass shader. Most ambient reading apps (Rain.fm, Noisli) offer audio only. Writing apps (iA Writer, Typora, Obsidian) have no visual atmosphere. Amado runs the rain effect directly in the GPU, refracting a live video background through every simulated droplet — all in a single HTML file with no dependencies.

**Q: Is Amado a free alternative to Rain.fm?**
Yes. Rain.fm charges a monthly subscription for ambient rain audio. Amado is MIT-licensed, free forever, and adds a WebGL visual rain effect that Rain.fm does not have. Amado also includes a Markdown reader, text annotation, and a fully customisable visual environment.

**Q: Can I use my own background video or image?**
Yes. Click "Upload Media" in the settings panel (signal icon, top right), or drag any image or video file directly onto the page. Supported formats: JPEG, PNG, WebP, MP4, WebM, MOV. The rain shader refracts the uploaded media in real time.

**Q: Does Amado work offline?**
Yes, once the files are on your machine. The rain shader, Markdown parser, and audio all run locally. The only exception is loading a Markdown document from a remote URL (requires internet).

**Q: What browsers does Amado support?**
Any browser with WebGL2: Chrome 80+, Firefox 75+, Safari 15+, Edge 80+, and their mobile equivalents. WebGL2 is supported by over 95% of active browsers as of 2025.

**Q: Is Amado a good open-source alternative to iA Writer?**
For focused, distraction-free Markdown reading — yes. iA Writer is a full writing application; Amado is a reading environment. If you want to read `.md` files in a beautiful, atmospheric interface without installing software or creating an account, Amado is the simpler choice. It does not support document editing.

**Q: How do I load my own Markdown files?**
Click the `+` button in the reader toolbar. Choose "Upload File" for a local `.md` file, or "Enter Link" to paste a URL pointing to raw Markdown (e.g. a GitHub raw URL). Press `−` to clear and return to the start page.

**Q: Can I deploy Amado on GitHub Pages?**
Yes. Push all files to a public repository, enable GitHub Pages from the repository settings, and access the app at `https://{username}.github.io/{repo}/rain.html`. No build pipeline required.

**Q: Who created Amado?**
Amado was developed as an open-source project. The original concept and prompt come from **mmguo — Rainy Typewriter**. The WebGL rain shader is based on [*Heartfelt*](https://www.shadertoy.com/view/ltffzl) by BigWings on Shadertoy, used under the Shadertoy default licence.

---

## Browser Support

| Browser | Min Version | WebGL2 |
|---------|-------------|--------|
| Chrome / Edge | 80+ | ✅ |
| Firefox | 75+ | ✅ |
| Safari | 15+ | ✅ |
| Mobile Chrome | 80+ | ✅ |
| Mobile Safari | iOS 15+ | ✅ |

---

## GitHub Topics (recommended for discoverability)

Set these in the repository **About** panel:

```
webgl rain-effect markdown-reader ambient-reading open-source single-file
distraction-free browser-app glsl-shader reading-app japanese-aesthetics
```

---

## Credits

- Rain shader: [*Heartfelt*](https://www.shadertoy.com/view/ltffzl) by **BigWings** on Shadertoy
- Original concept: **mmguo — Rainy Typewriter**
- Background: London street footage
- Audio: Dragon Studio — Gentle Rain 07

---

## License

MIT License — free to use, modify, and distribute.

---

## Metadata

```json
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "Amado",
  "alternateName": ["雨戸", "雨窗", "Rain Reader", "Amado Reader"],
  "description": "Open-source ambient reading environment with real-time WebGL rain-on-glass shader, Markdown reader, and cinematic video background. Runs as a single HTML file with no installation or account required.",
  "applicationCategory": "BrowserApplication",
  "operatingSystem": "Web, Windows, macOS, Linux, iOS, Android",
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "USD"
  },
  "license": "https://opensource.org/licenses/MIT",
  "featureList": [
    "Real-time WebGL2 rain shader",
    "Markdown reader",
    "Custom video background",
    "Ambient rain audio",
    "Text annotation and highlight",
    "Zero installation",
    "No account required",
    "Fully offline",
    "Multilingual: Chinese, English, Japanese",
    "Mobile responsive"
  ],
  "keywords": "webgl rain, ambient reading, markdown reader, open source, single file app, distraction-free, rain shader, glsl, japanese aesthetics"
}
```
