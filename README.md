# VinylTracker

A native macOS app for managing your vinyl record collection.

## Download

👉 **[Latest Release](https://github.com/mrpatrickstaresq/vinyltracker-releases/releases/latest)**

1. Download `VinylTracker.dmg`
2. Open the DMG and drag VinylTracker to Applications
3. Launch from Applications

## Uninstall

Drag **VinylTracker.app** from your Applications folder to the Trash. An uninstaller script is also included inside the DMG — double-click `Uninstall VinylTracker.command` to remove the app and all associated data files in one step.

## Requirements

- macOS 12 Monterey or later

---

## Features

### 📀 Collection Management
- Import your vinyl collection from a Discogs CSV export or via direct Discogs API sync
- Duplicate detection by catalog number or artist/title
- Real-time search filtering across artist, title, genre, style, and label
- Sortable table view with live record count display
- Context menu to clear play history per album
- **Refresh Collection** syncs your Discogs collection and shows a preview dialog before saving any changes — lists new records (green), removed records (red), and metadata updates (amber) with Accept or Keep As-Is buttons
- "Always apply changes without preview" option in Settings to skip the diff dialog and apply immediately
- **Export Collection as CSV**: Collection → Export Collection as CSV… saves a dated CSV file with all metadata expanded — including pressing credits, personnel, barcodes, and liner notes

### 🖼️ Cover Art & Artwork
- Cover art fetched from the Discogs release endpoint using the primary front-cover image
- Falls back to MusicBrainz / Cover Art Archive as a secondary source
- Per-record on-demand background fetch when an album is selected
- Background batch sync for missing artwork — pre-checks the database to avoid redundant API calls
- **Tools → Sync Album Artwork**: fetches art only for records missing it, with status bar progress and time estimate
- **Tools → Sync Tracklists**: fetches tracklists only for records missing them, with time estimate

### 🎵 Metadata Enrichment
- Original release year sourced from MusicBrainz (first-release-date); falls back to Last.fm — Discogs year ignored
- Album runtime calculated from track durations
- Full tracklist with vinyl side grouping (Side A, B, C…)
- Genre and style aggregation

### 🏭 Pressing Details
- **Pressing Details** section in the Now Playing panel (below tracklist)
- Displays: country of pressing, mastering/cutting/plating credits, pressing plant and studio info, matrix/runout identifiers (monospace), and release notes
- **Personnel** sub-section: producer, engineer, performer, writer, and photographer credits
- **Barcodes** sub-section: all barcode identifiers for the pressing
- **Liner Notes** sub-section: full release notes text
- Loads instantly from local cache on album select; fetches from Discogs in background on first view
- **Tools → Sync Pressing Info / Personnel Credits / Barcodes**: batch workers with progress and time estimates

### ▶️ Now Playing Panel
- Large 360px cover art with placeholder fallback
- Album details: label, format, year, genre, style
- Full tracklist grouped by vinyl side
- Last logged play timestamp
- Pressing Details section: country, mastering credits, pressing plant, matrix/runout, personnel, barcodes, liner notes
- **Log Play** button with turntable selector — pre-selects your default turntable automatically
- **＋ My Listening Queue** button — adds album to queue; queue panel refreshes immediately

### 🕹️ Play History
- Sortable table (date, artist, title, turntable, runtime)
- Multi-select + delete entries
- Context menu: delete entries, clear all history for album
- Clear all history button with confirmation

### 🏠 Home Dashboard
- Three-column layout: Last Played (full detail) | Suggested Spins + Album Anniversary | Listening Queue
- **Last Played** (full left pane, scrollable): cover art, artist/title, play timestamp, metadata grid (genre, style, year, label, format, country, runtime), complete tracklist (all tracks), Pressing Details, Personnel Credits, Barcodes, and Liner Notes — all in one view
  - Missing pressing info is auto-synced on load — no manual sync required
  - Click cover art to navigate directly to the album in the Collection tab
- **Suggested Spins**: weighted random album suggestion; never-played albums weighted 7×; Log Play and Queue buttons
- **Album Anniversary**: highlights a random album released exactly 10/20/30/40/50/60 years ago with cover art, anniversary badge, Last.fm summary, and tracklist
- Logging a play from any panel refreshes all Home tab panels automatically

### 📥 Listening Queue
- Right pane of the Home tab and Collection tab — persistent across sessions (SQLite-backed)
- **My Queue** (manual): user-curated ordered list — up to 50 albums
  - Drag rows to reorder; new order saved immediately
  - Log Play removes from queue; ✕ removes without logging
  - ↻ Refresh button in panel header
- **Suggested** (auto): 20 albums not played in 182+ days (or never played), randomised, no duplicate artists
  - "＋ My Listening Queue" button on each row
  - ↻ Refresh button for a new random set
- Buttons in Now Playing and Suggested Spins columns show "✓ In My Queue" when already queued

### 📊 Statistics Dashboard
- **Collection Overview**: total records, unique artists, never-played count, average album runtime
- **Play History Overview**: total plays, total listening time, plays this month, best month ever
- Most Played Artists and Albums (top 10 each, side by side)
- Plays by Genre and Plays by Month (last 12 months)
- Plays by Day of Week breakdown
- Recently Added to Collection: last 10 records with artist, title, year, and date added
- Refresh button to reload all stats on demand

### 🎂 Album Anniversary Panel
- Highlights a random album from your collection released exactly 10, 20, 30, 40, 50, or 60 years ago
- Anniversary based on the original first release year (MusicBrainz primary, Last.fm secondary — never Discogs date)
- Large centered 220px cover art, anniversary badge ("🎉 N Year Anniversary · YYYY"), metadata grid, Last.fm album summary, and full tracklist
- Random selection on each launch; Refresh (↻) button for another pick from the same year set
- Click cover art to navigate to that record in the Collection tab

### 🗓️ Release Date Sync
- **Tools → Fetch MusicBrainz Release Dates**: batch cross-references your entire collection against MusicBrainz; stores original first-release year; progress shown in status bar; updates collection table in real time
- **Tools → Fetch Last.fm Release Dates**: batch fetch from Last.fm album.getInfo; only updates records with no MusicBrainz year (preserving MB-first priority)

### 💾 Database Backup & Restore
- **Collection → Backup Database…**: hot-copies the live database to any file you choose — safe while the app is running; filename auto-stamped with date and time
- **Collection → Restore from Backup…**: validates the file, asks for confirmation, replaces the live database, and reloads your collection in-place
- **Import dialog**: "Restore from Backup" third tab available on first launch — restore a backup as your initial data instead of syncing from Discogs or importing a CSV

### 🎛️ Turntable Management
- Add, edit, and delete turntables (manufacturer, model, cartridge, stylus)
- **Set as Default**: mark one turntable as the default — it's pre-selected in the Now Playing combo and used automatically when logging plays from the queue (★ shown in the turntable list)
- Per-play turntable tracking
- Play count and total listening hours per turntable

### 🤖 AI Chat Assistant
- Dedicated **Ask AI** tab powered by the Claude API (Sonnet) with streaming responses
- Five selectable offline local models (Apple Silicon via MLX):
  - Llama 3.2 3B 4-bit (~1.8 GB) — balanced quality/speed
  - Qwen 2.5 3B 4-bit (~1.8 GB) — stronger structured-data Q&A
  - Phi-3.5 Mini 4-bit (~2.2 GB) — Microsoft 3.8B
  - Gemma 3 4B 4-bit (~2.5 GB) — Google, excellent reasoning
  - Qwen 2.5 1.5B 4-bit (~1.0 GB) — fastest, ideal for 8 GB RAM Macs
- Speculative decoding for ~2-3× generation speedup (paired draft models)
- Persistent model subprocess — stays loaded across tab switches
- Chart generation (bar/pie) on request
- Context-aware queries: play history, album lookup, statistics
- Keyword-filtered album context: only sends matching records instead of your full collection (cuts tokens ~90%)
- **AI can be fully disabled** via Settings → AI Features checkbox

### 🗂️ Navigation
- macOS menu bar: Collection, Tools, View (themes), and Tabs menus
- Keyboard shortcuts: ⌘1–4 to switch tabs, ⌘, for Settings
- **Settings** appears in the VinylTracker macOS app menu (correctly labeled "Settings…" on all macOS versions)
- **Detachable tabs**: drag, right-click, or use ⌘⇧D to pop any tab into its own window; close to re-dock

### ⚙️ Settings & Authentication
- Discogs username and personal access token storage
- Claude API key configuration
- Last.fm API key bundled and auto-stored on first launch
- Backend selection: Claude API or any of the 5 local models
- **Collection Refresh**: "Always apply changes without preview" checkbox
- **AI Features toggle**: disable/re-enable the Ask AI tab
- **Danger Zone**: "Clear All Local Data" removes database, artwork cache, and all model caches

### 🎨 Appearance
- **22 selectable color themes**: System, Light, Default (Dark), Warm, Ocean, Purple, Midnight, Sunset, OG Green Console, Rose, Nord, Dracula, Monokai, Espresso, Cherry, Cobalt, Slate, Reggae, Grateful Dead, Queen, Pet Sounds, Metal
- Theme applies instantly across all widgets and persists across launches
- macOS standard close behaviour: red X hides the window; clicking the Dock icon restores it
- Window size, position, and all panel splitter sizes remembered across launches
- Skeuomorphic app icon: royal-blue plinth, near-black vinyl, chrome S-curve tonearm with correct headshell offset angle

### 🚀 Performance
- SQLite WAL journal mode + 32 MB page cache + 256 MB memory-mapped I/O
- Two-pass query design for suggested album and queue fetches
- Indexes on artist/title and original_year/year — applied automatically on first launch
- Sync operations show time estimates before starting
- Write-behind batch DB optimisations across all sync workers: tracklist/runtime/year in one transaction; MusicBrainz and Last.fm year updates batched every 20 records (~20× fewer lock acquisitions)

### 🗑️ Uninstall
- Included `Uninstall VinylTracker.command` script in the DMG (double-click to run)
- Three modes: Complete Uninstall, Remove App Only, or Free Disk Space (AI model caches only)
- Detects and offers to quit a running instance before removing files
- Shows disk size of each item and prompts before each deletion
