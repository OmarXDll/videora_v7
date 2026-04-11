# videora_v7

An application for creating lists and saving videos in an organized way with more additional tools.

## Table of Contents

- [Overview](#overview)
- [Getting Started](#getting-started)
  - [Opening the Application](#opening-the-application)
  - [Creating an Account](#creating-an-account)
  - [Logging In](#logging-in)
- [Key Features](#key-features)
  - [Playlists](#playlists)
  - [Adding Videos](#adding-videos)
  - [Video Player](#video-player)
  - [Settings and Customization](#settings-and-customization)
- [User Roles](#user-roles)
- [Admin Panel](#admin-panel)
  - [User Management](#user-management)
  - [Banned Users](#banned-users)
  - [API Keys](#api-keys)
- [Advanced Features](#advanced-features)
  - [Code Editor](#code-editor)
  - [Developers Panel](#developers-panel)
  - [AI-Powered Translation](#ai-powered-translation)
- [License](#license)

---

## Overview

**Vidora** (also stylized as **VIDORA**) is a cloud-based video storage and management application. It allows users to organize their videos into playlists, play them with a built-in player, and manage their media library entirely from the browser. The application is built as a single-page HTML file with no external dependencies beyond Font Awesome icons, making it easy to deploy and use.

## Getting Started

### Opening the Application

Simply open the `vidora_v7.html` file in any modern web browser (Chrome, Firefox, Edge, Safari, etc.). No server or build step is required — the application runs entirely in the browser and stores data in `localStorage`.

### Creating an Account

1. On the login page, click the **"Register Now"** link below the login button.
2. Enter your email address when prompted.
3. Enter a password when prompted.
4. After successful registration, you will be redirected to the login page. Use your new credentials to log in.

### Logging In

1. Enter your **email** and **password** on the login page.
2. Click the **"Login"** button or press **Enter**.
3. You will be taken to the main application dashboard.

> **Pre-configured demo accounts:**
>
> | Email | Password | Role |
> |---|---|---|
> | `admin@vidora.com` | `123456` | Admin |
> | `pro@vidora.com` | `123456` | Pro |
> | `user@vidora.com` | `123456` | User |

---

## Key Features

### Playlists

Playlists are the primary way to organize your videos.

- **Create a Playlist:** Click the **"New Playlist"** button in the left sidebar. Enter a name for your playlist and click **"Create"**.
- **Select a Playlist:** Click on any playlist in the sidebar to view its videos.
- **Edit a Playlist:** Click the three-dot menu icon on any playlist, then select **"Edit Name"** to rename it.
- **Delete a Playlist:** Click the three-dot menu icon on any playlist, then select **"Delete Playlist"**. This will permanently remove the playlist and all its videos.
- **Home View:** Click the **"Home"** button in the top bar to view all your videos across all playlists.

### Adding Videos

After selecting a playlist, click the **"Add Video"** button. There are four methods to add videos:

1. **File Upload:** Upload a video file directly from your device. The application automatically generates a thumbnail and detects the video duration.
2. **Link:** Paste a video URL (supports YouTube links with automatic thumbnail fetching). Enter a title and the video link, then click **"Add"**.
3. **QR Code:** Add a video by scanning a QR code. Click **"Open Camera"** to scan.
4. **Private:** Add a private/personal video by entering a URL. These are labeled with a "Private" badge.

**Deleting a Video:** Hover over any video card and click the red delete button that appears in the top-right corner.

### Video Player

Click on any video card to open the built-in full-screen video player. Player controls include:

| Control | Description |
|---|---|
| **Play/Pause** | Toggle video playback |
| **-10 / +10** | Rewind or fast-forward by 10 seconds |
| **Progress Bar** | Click or drag to seek to any position |
| **Speed** | Cycle through playback speeds: 0.5x, 0.75x, 1x, 1.25x, 1.5x, 2x |
| **Mute** | Toggle audio mute |
| **Fullscreen** | Enter or exit browser fullscreen mode |
| **AI Enhance** | Enhance video quality with AI (Pro users and above only) |
| **Close (X)** | Close the player and return to the main view |

### Settings and Customization

Click the **gear icon** in the top-right corner to open the Settings modal.

#### Themes

Choose from five visual themes:

| Theme | Description |
|---|---|
| **Dark Blue** | Default dark theme with blue accents |
| **Dark Black** | Pure dark theme with gray accents |
| **Light** | Light theme for bright environments |
| **Purple** | Dark theme with purple accents |
| **Green** | Dark theme with green accents |

#### Language

The application supports multiple languages: **Arabic** (default), **English**, **French**, **German**, **Turkish**, and **Spanish**. Language switching uses AI-powered translation via the Gemini API to translate UI elements on the fly.

#### Other Settings

- **Card Size:** Choose between Small (220px), Medium (280px), or Large (340px) video card widths.
- **Motion Effects:** Enable or disable hover animations on video cards.
- **Show Duration:** Toggle the display of video duration badges on cards.
- **Autoplay:** Enable or disable automatic video playback when opening a video.

---

## User Roles

Vidora has a role-based access system with four levels:

| Role | Badge | Capabilities |
|---|---|---|
| **User** | Blue | Create playlists, add videos, use the player |
| **Pro** | Purple | All User features + AI video enhancement |
| **Admin** | Pink | All Pro features + Code Editor access + API panel |
| **Super Admin** | Gradient | All Admin features + User Management panel + full control |

---

## Admin Panel

The Admin Panel is accessible only to **Super Admin** users via the **"User Management"** button in the top bar.

### User Management

- View a table of all registered users with their email, registration date, role, playlist count, and video count.
- **Search** users by email using the search bar.
- **Edit** a user to change their role (User, Pro, or Admin).
- **View Videos** to see all videos uploaded by a specific user.
- **Ban** a user with a specified reason. Banned users cannot log in.

### Banned Users

- View a table of all banned users with their email, ban date, and ban reason.
- **Unban** a user to restore their access.

### API Keys

- View existing API keys with their name, creation date, and permissions.
- **Generate** new API keys with custom names.
- **Copy** API keys to the clipboard.
- **Delete** API keys that are no longer needed.

---

## Advanced Features

### Code Editor

Available to **Admin** and **Super Admin** users via the **"Code Editor"** button in the top bar.

- Edit the application source code directly in the browser with tabs for **HTML**, **CSS**, **JavaScript**, **TypeScript**, and **Backend** code.
- **Apply Changes** to see CSS and JavaScript modifications take effect immediately.
- **Reload** the application to apply HTML changes.

### Developers Panel

Available to **Admin** and **Super Admin** users via the **"API"** button in the top bar.

- Create and manage API keys for programmatic access.
- Each key includes read/write permissions and can be copied or deleted.

### AI-Powered Translation

When switching the language from Arabic to another language (English, French, German, Turkish, or Spanish), the application uses the **Google Gemini API** to translate UI elements in real time. Switch back to Arabic to restore the original interface.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
