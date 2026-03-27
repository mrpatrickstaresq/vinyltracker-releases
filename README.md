# VinylTracker

A native macOS app for managing your vinyl record collection. Built with Swift and SwiftUI.

## Download

👉 **[Latest Release](https://github.com/mrpatrickstaresq/vinyltracker-releases/releases/latest)**

| Mac | Download |
|-----|----------|
| Apple Silicon (M1/M2/M3/M4) | `VinylTracker-AppleSilicon.dmg` |

1. Open the DMG and drag VinylTracker to Applications
2. Launch from Applications

## Requirements

- **Apple Silicon (M1/M2/M3/M4):** macOS 13 Ventura or later

---

## Features

### 📀 Collection Management
- Import your vinyl collection via direct Discogs API sync
- Real-time search and filtering across artist, title, genre, style, and label
- Sortable collection view with live record count
- Cover art fetched from Discogs (primary) and iTunes/MusicBrainz (fallback)
- Tracklists with vinyl side groupings (Side A, B, C…)
- Pressing details, personnel credits, barcodes, and liner notes

### 🔍 Metadata & Enrichment
- Original release year sourced from MusicBrainz or Last.fm — never uses pressing date
- Background sync for cover art, tracklists, pressing info, credits, and barcodes
- Targeted per-field sync tools available from the Tools menu

### ▶️ Play History
- Log plays with turntable selection
- Sortable play history with filtering by artist, title, or turntable
- Export play history as CSV

### 🏠 Home Dashboard
- Last Played, Suggested Spins, Album Anniversary, and Listening Queue panels

### 📥 Listening Queue
- **My Queue** (manual): curated ordered list, drag to reorder
- **Suggested** (auto): albums unplayed for 6+ months, randomised, no duplicate artists

### 📊 Statistics
- Genre and decade breakdowns
- Top artists, labels, producers, and engineers
- Plays by day of week and time of day

### 🗂️ Saved Queries
- Save and replay custom collection filters

### ☁️ iCloud Sync
- Collection, play history, and crates sync automatically via iCloud
- Cover art stored locally by default to protect iCloud storage
- Optional cover art iCloud sync available in Settings

### 💾 Backup & Restore
- Full export/import using stable Discogs IDs
- Available on-demand from Settings or prompted on first launch

### 🎛️ Turntable Management
- Add, edit, and delete turntables
- Set a default; per-play tracking

### 🎨 Appearance
- Multiple selectable color themes
- Supports light and dark mode

### ⚙️ API Keys Required
- **Discogs personal access token** — for collection sync ([get one here](https://www.discogs.com/settings/developers))
- **Last.fm API key** — for original release year lookups
- Both entered in the app's Settings panel
