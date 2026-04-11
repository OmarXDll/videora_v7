# Videora v7

**Videora** (فيدورا) is a cloud-inspired video storage and management application built as a single-page HTML app. It lets you organize videos into playlists, play them with a full-featured player, and manage users — all from a sleek, themeable interface with right-to-left (RTL) Arabic support.

---

## Table of Contents

- [Features](#features)
- [Demo Accounts](#demo-accounts)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Running Locally](#running-locally)
  - [Deploying](#deploying)
- [Usage](#usage)
  - [Logging In](#logging-in)
  - [Managing Playlists](#managing-playlists)
  - [Adding Videos](#adding-videos)
  - [Playing Videos](#playing-videos)
  - [Settings & Themes](#settings--themes)
  - [Admin Panel](#admin-panel)
  - [Developer Tools](#developer-tools)
- [Project Structure](#project-structure)
- [Technologies Used](#technologies-used)
- [Contributing](#contributing)
- [License](#license)

---

## Features

- **Playlist Management** — Create, rename, delete, and color-code playlists to keep your videos organized.
- **Multiple Video Sources** — Add videos from local files, YouTube/direct links, QR codes, or custom URLs.
- **Built-in Video Player** — Full playback controls including play/pause, seek, rewind/forward (10 s), adjustable speed (0.5×–2×), mute, and fullscreen.
- **AI Video Enhancement** — Pro and higher users can trigger AI-powered quality enhancement.
- **Auto-Generated Thumbnails** — Automatically captures a thumbnail frame from locally uploaded videos.
- **Role-Based Access Control** — Four user roles with increasing privileges:
  | Role | Capabilities |
  |------|-------------|
  | **User** | Create playlists, add/play videos |
  | **Pro** | Everything above + AI enhancement |
  | **Admin** | Everything above + code editor, developer API panel |
  | **Super Admin** | Everything above + full user management, ban/unban |
- **Admin Dashboard** — View all users, edit roles, ban/unban accounts, and manage API keys.
- **Live Code Editor** — Admins can view and edit the app's HTML, CSS, JavaScript, TypeScript, and backend code in real time.
- **Multi-Language Support** — UI translation powered by Google Gemini AI for Arabic, English, French, German, Turkish, and Spanish.
- **5 Color Themes** — Dark Blue (default), Light, Purple, Green, and Red.
- **Customizable Settings** — Toggle animations, video duration display, autoplay, and card sizes (small / medium / large).
- **Persistent Storage** — User session and data are saved to `localStorage` so your data survives page reloads.

---

## Demo Accounts

The app ships with pre-configured accounts for testing:

| Email | Password | Role |
|-------|----------|------|
| `omarxdll.x@gmail.com` | `Omar11223` | Super Admin |
| `admin@vidora.com` | `123456` | Admin |
| `pro@vidora.com` | `123456` | Pro |
| `user@vidora.com` | `123456` | User |

---

## Getting Started

### Prerequisites

- A modern web browser (Chrome, Firefox, Edge, Safari).
- No build tools, package managers, or servers are required — it is a standalone HTML file.

### Running Locally

1. **Clone the repository:**

   ```bash
   git clone https://github.com/OmarXDll/videora_v7.git
   cd videora_v7
   ```

2. **Open the app in your browser:**

   ```bash
   # macOS
   open vidora_v7.html

   # Linux
   xdg-open vidora_v7.html

   # Windows
   start vidora_v7.html
   ```

   Or simply double-click `vidora_v7.html` in your file explorer.

### Deploying

Because Videora is a single HTML file with no external dependencies (other than the Font Awesome CDN), you can host it on any static file server:

- **GitHub Pages** — Push to a `gh-pages` branch or enable Pages on your main branch.
- **Netlify / Vercel** — Drag-and-drop the repo or connect it for automatic deploys.
- **Any HTTP Server** — For example:

  ```bash
  # Python
  python3 -m http.server 8000

  # Node.js (with npx)
  npx serve .
  ```

  Then visit `http://localhost:8000/vidora_v7.html`.

---

## Usage

### Logging In

1. Open the app — you will see the login page with the Videora logo.
2. Enter an email and password from the [Demo Accounts](#demo-accounts) table, or click **سجل الآن** (Register Now) to create a new account.

### Managing Playlists

- Click **قائمة جديدة** (New Playlist) in the sidebar to create a playlist.
- Click a playlist name to select it and view its videos.
- Click the **⋮** menu on a playlist to rename or delete it.

### Adding Videos

Select a playlist first, then click **إضافة فيديو** (Add Video). You can add videos from four sources:

| Tab | Description |
|-----|-------------|
| **ملف** (File) | Upload a local video file from your device. |
| **رابط** (Link) | Paste a YouTube URL or direct video link. |
| **QR** | Add a video via QR code. |
| **خاص** (Private) | Add a video from a custom/private URL. |

### Playing Videos

Click any video card to open the full-screen player. Controls:

| Control | Action |
|---------|--------|
| ▶️ / ⏸ | Play / Pause |
| ⏪ / ⏩ | Rewind / Forward 10 seconds |
| 🔊 | Toggle mute |
| Speed | Cycle through 0.5×, 0.75×, 1×, 1.25×, 1.5×, 2× |
| ⛶ | Toggle fullscreen |
| ✨ AI | Enhance video quality (Pro+ only) |

### Settings & Themes

Click the ⚙️ gear icon in the top bar to open settings:

- **Theme** — Choose from Dark Blue, Light, Purple, Green, or Red.
- **Language** — Switch between Arabic, English, French, German, Turkish, and Spanish.
- **Card Size** — Small (220 px), Medium (280 px), or Large (340 px).
- **Toggles** — Enable/disable motion effects, video duration badges, and autoplay.

### Admin Panel

Accessible only to the **Super Admin** role via the **إدارة المستخدمين** (User Management) button:

- **Users Tab** — Search, view, edit roles, view user videos, or ban users.
- **Banned Tab** — View banned users and unban them.
- **API Keys Tab** — Generate and manage API keys.

### Developer Tools

Available to **Admin** and **Super Admin** roles:

- **Code Editor** — Edit the app's source code (HTML, CSS, JS, TS, Backend) live.
- **API Panel** — Create and manage named API keys with read/write permissions.

---

## Project Structure

```
videora_v7/
├── vidora_v7.html   # The entire application (HTML + CSS + JavaScript)
├── LICENSE           # GNU General Public License v3.0
└── README.md         # This file
```

The application is self-contained in a single HTML file. All styles and scripts are embedded inline. The only external resource is the [Font Awesome](https://fontawesome.com/) icon library loaded from a CDN.

---

## Technologies Used

- **HTML5 / CSS3 / JavaScript (ES6+)** — Core application stack.
- **CSS Custom Properties** — For theming and dynamic color switching.
- **Font Awesome 6** — Icon library.
- **Google Gemini AI API** — Powers multi-language UI translation.
- **Web APIs** — `localStorage`, `URL.createObjectURL`, `Canvas`, `Fullscreen API`, `Clipboard API`.

---

## Contributing

Contributions are welcome! Here's how you can help:

1. **Fork** the repository.
2. **Create a feature branch:**

   ```bash
   git checkout -b feature/my-new-feature
   ```

3. **Make your changes** to `vidora_v7.html` (or add new files if needed).
4. **Test** your changes by opening the file in a browser and verifying the feature works across different themes and user roles.
5. **Commit** your changes with a clear message:

   ```bash
   git commit -m "Add: description of your feature"
   ```

6. **Push** to your fork:

   ```bash
   git push origin feature/my-new-feature
   ```

7. **Open a Pull Request** against the `main` branch of this repository.

### Guidelines

- Keep the single-file architecture unless there is a strong reason to split.
- Maintain RTL (right-to-left) support for all UI changes.
- Test with multiple themes to ensure color variables are used correctly.
- Do not commit real API keys or credentials.
- Follow the existing code style (camelCase for JS, kebab-case for CSS classes).

### Ideas for Contributions

- Drag-and-drop video reordering within playlists.
- Export/import data (playlists and videos) as JSON.
- Backend integration for persistent multi-device storage.
- Progressive Web App (PWA) support for offline access.
- Accessibility improvements (keyboard navigation, screen reader support).

---

## License

This project is licensed under the **GNU General Public License v3.0** — see the [LICENSE](LICENSE) file for details.
