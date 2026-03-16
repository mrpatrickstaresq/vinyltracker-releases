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

### 🖼️ Cover Art & Artwork
- Cover art fetched from the Discogs release endpoint using the primary front-cover image
- Falls back to MusicBrainz / Cover Art Archive as a secondary source
- Per-record on-demand background fetch when an album is selected
- Background batch sync for missing artwork — pre-checks the database to avoid redundant API calls
- **Tools → Sync Album Artwork**: fetches art only for records missing it, with status bar progress
- **Tools → Sync Tracklists**: fetches tracklists only for records missing them

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
- Uses stored Discogs release ID (1 API call); falls back to search + release fetch (2 calls) and caches the ID for future efficiency
- **Tools → Sync Pressing Info**: batch-fetch pressing details for your entire collection with status bar progress
- **Tools → Sync Personnel Credits**: batch-fetch personnel credits for records missing them
- **Tools → Sync Barcodes**: batch-fetch barcode data for records missing it

### ▶️ Now Playing Panel
- Large 360px cover art with placeholder fallback
- Album details: label, format, year, genre, style
- Full tracklist grouped by vinyl side
- Last logged play timestamp
- Pressing Details section: country, mastering credits, pressing plant, matrix/runout, personnel, barcodes, liner notes
- **Log Play** button with optional turntable selection
- **＋ Queue** button — adds the album to your personal Listening Queue; shows "✓ Queued" when already queued

### 🕹️ Play History
- Sortable table (date, artist, title, turntable, runtime)
- Multi-select + delete entries
- Context menu: delete entries, clear all history for album
- Clear all history button with confirmation

### 🏠 Home Dashboard
- Three-column layout: Last Played + Recent Plays | Suggested Spins + Album Anniversary | Listening Queue
- **Last Played**: cover art, artist/title, play timestamp, metadata grid, full tracklist — click to jump to album
- **Most Recently Played**: 15 most recently played distinct albums with thumbnails — click to navigate
- **Suggested Spins**: weighted random album suggestion; never-played albums weighted 7×; Log Play and Queue buttons
- **Album Anniversary**: highlights a random album released exactly 10/20/30/40/50/60 years ago with cover art, anniversary badge, Last.fm summary, and tracklist
- Logging a play from any panel refreshes all Home tab panels automatically

### 📥 Listening Queue
- Persistent across sessions (SQLite-backed), right pane of the Home tab
- **My Listening Queue** (manual): user-curated ordered list of up to 50 albums
  - Row: drag handle (⠿), position number, 40px cover thumbnail, artist — title
  - Drag to reorder; new order persisted immediately
  - ▶ Log Play logs a play and removes the entry; ✕ removes without logging
  - "Clear All" button in the section header
- **Suggested** (auto): 20 albums not played in 182+ days (or never played), randomised on each load
  - No duplicate artists — at most one album per artist in the suggestions
  - Auto-refreshes on launch; ↻ Refresh button for a new random set
  - ＋ Queue button on each row to add to your personal queue

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
  - Bigram extraction catches multi-word artist/album names (Pink Floyd, Miles Davis, etc.)
  - Decade detection: "70s", "1970s", "seventies" → year-range filter applied to query
  - Fallback: collections ≤ 75 records always get the full list
- **AI can be fully disabled** via Settings → AI Features checkbox — removes the Ask AI tab and all AI functionality; re-enabling restores everything instantly

### 🎛️ Turntable Management
- Add, edit, and delete turntables (manufacturer, model, cartridge, stylus)
- Per-play turntable tracking
- Play count and total listening hours per turntable

### 🗂️ Navigation
- macOS menu bar: Collection, Tools, View (themes), and Tabs menus
- Keyboard shortcuts: ⌘1–4 to switch tabs, ⌘, for Settings
- **Settings** appears in the VinylTracker macOS app menu (standard ⌘, position) in addition to the Tools menu
- **Detachable tabs** — three ways to pop any tab into its own window:
  - Drag a tab outside the tab bar
  - Right-click a tab → "Open in New Window"
  - Tabs menu → "Detach Current Tab" (⌘⇧D)
  - Closing the detached window re-docks the tab back into the main bar
  - "Reattach All Windows" in the Tabs menu re-docks all floating tabs at once

### ⚙️ Settings & Authentication
- Discogs username and personal access token storage
- Claude API key configuration
- Last.fm API key bundled and auto-stored on first launch (no user configuration required)
- Backend selection: Claude API or any of the 5 local models
- **Collection Refresh**: "Always apply changes without preview" checkbox — skip the diff dialog and apply changes immediately
- **AI Features toggle**: checkbox to disable all AI functionality and remove the Ask AI tab; re-enable to restore
- **Danger Zone**: "Clear All Local Data" removes the database, artwork cache, and all downloaded model caches, then quits

### 🎨 Appearance
- **19 selectable color themes**: System, Light, Default, Warm, Ocean, Purple, Midnight, Sunset, OG Green Console, Rose, Nord, Dracula, Monokai, Espresso, Cherry, Cobalt, Slate, Reggae, Metal
- Theme applies instantly across all widgets and persists across launches
- macOS standard close behaviour: red X hides the window; clicking the Dock icon restores it
- Window size, position, and all panel splitter sizes remembered across launches
- Large, readable fonts throughout (18–20pt artist names, 28px metric cards)
- Skeuomorphic app icon: royal-blue plinth, near-black vinyl, chrome S-curve tonearm with correct headshell offset angle

### 🚀 Performance
- SQLite WAL journal mode: readers never block background writers
- 32 MB page cache — hot pages stay in RAM between queries
- 256 MB memory-mapped I/O — large cover art BLOBs stream via kernel mapping
- Two-pass query design for suggested album and queue fetches (metadata first, BLOBs only for final rows)
- Indexes on artist/title and original_year/year — applied automatically on first launch
- Artwork sync: year, runtime, and tracklist written in a single transaction per record
- Artwork/tracklist batch sync: ~1.1 s/record (authenticated) — safely under Discogs rate limits

### 🗑️ Uninstall
- Included `Uninstall VinylTracker.command` script in the DMG (double-click to run)
- Three modes: Complete Uninstall, Remove App Only, or Free Disk Space (AI model caches only)
- Detects and offers to quit a running instance before removing files
- Shows disk size of each item and prompts before each deletion
- Detects and offers removal of any other Hugging Face model caches on the machine
