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

### 🔍 Query Builder
- Dedicated **Query tab** (⌘4) with seven ready-to-run parameterised query panels:
  1. **By Artist** — artist dropdown populated from your collection; substring matching returns all related ensembles
  2. **By Genre / Style** — genre and style dropdowns with "Any" option
  3. **By Decade** — 50s through 2020s
  4. **Never Played** — one-click, no inputs required
  5. **Most / Least Played** — direction toggle and top-N count
  6. **By Label** — label dropdown populated from your collection
  7. **Not Played Since** — 1 month / 3 months / 6 months / 1 year / 2 years / 3 years
- Results shown in a sortable, resizable table — click any column header to sort ascending/descending; double-click to auto-fit width
- **⭐ Save** button on each panel prompts for a name and pins the query to Saved Queries
- **Recent Queries**: last 20 runs shown below the panels — double-click to re-run with the same parameters
- **Saved Queries**: named pinned queries with ✕ delete — double-click to re-run

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
- **Personnel** sub-section: name (left, bold) and role/instruments (right, dim) — wraps on resize
- **Barcodes** sub-section: all barcode identifiers for the pressing
- **Liner Notes** sub-section: full release notes text
- Loads instantly from local cache on album select; fetches from Discogs in background on first view
- **Tools → Sync Pressing Info / Personnel Credits / Barcodes**: batch workers with progress and time estimates

### ⏹️ Stop Sync Controls
- **Per-worker stop buttons** appear inline in the status bar the moment a sync starts
- Buttons disappear immediately when clicked or when the sync completes naturally
- **■ Stop All** button appears automatically when two or more syncs are running simultaneously

### ▶️ Now Playing Panel
- Large 360px cover art with placeholder fallback
- Sections in order: cover → artist/title → Log Play controls → Album Details → Tracklist → Pressing Details → Personnel Credits → Barcodes → Liner Notes
- **Album Details** metadata grid: Genre · Style · Year · Label · Format · Country · Runtime
- Full tracklist (all tracks, no cap)
- Pressing Details, Personnel Credits, Barcodes, and Liner Notes loaded from cache instantly; auto-synced in background if missing
- **Log Play** button with turntable selector — pre-selects your default turntable automatically
- **＋ My Listening Queue** button — adds album to queue; queue panel refreshes immediately

### 🕹️ Play History
- Sortable, resizable table (date, artist, title, turntable, runtime) — click any column to sort
- Columns distribute evenly across the panel on launch; drag to resize, double-click header to auto-fit
- Multi-select + delete entries
- Context menu: delete entries, clear all history for album
- Clear all history button with confirmation

### 🏠 Home Dashboard
- Three-column layout: Last Played (full detail) | Suggested Spins + Album Anniversary | Listening Queue
- **Last Played** (full left pane, scrollable): cover art, artist/title, play timestamp, metadata grid, complete tracklist, Pressing Details, Personnel Credits, Barcodes, and Liner Notes
- **Suggested Spins**: weighted random album suggestion; never-played albums weighted 7×; Log Play and Queue buttons
- **Album Anniversary**: highlights a random album released exactly 10/20/30/40/50/60 years ago with cover art, anniversary badge, Last.fm summary, and tracklist
- Logging a play from any panel refreshes all Home tab panels automatically

### 📥 Listening Queue
- Right pane of the Home tab and Collection tab — persistent across sessions (SQLite-backed)
- **My Queue** (manual): user-curated ordered list — up to 50 albums; drag to reorder
- **Suggested** (auto): 20 albums not played in 182+ days, randomised, no duplicate artists
- Buttons show "✓ In My Queue" when already queued

### 📊 Statistics Dashboard
- **8 metric cards** always visible at the top: total records, unique artists, never-played count, average album runtime, total plays, total listening time, plays this month, best month ever
- **Two chart sub-tabs:**
  - **Collection** — Genre breakdown donut, Collection by Decade bar, Collection by Artist horizontal bar (top 15, variant deduplication), Lacquer/Cutting Engineers horizontal bar (top 5)
  - **Play History** — Top Artists, Top Albums, Plays by Month, Plays by Day of Week, Plays by Genre; fully scrollable with trackpad/mouse wheel
- Refresh button to reload all stats on demand

### 🎂 Album Anniversary Panel
- Highlights a random album released exactly 10, 20, 30, 40, 50, or 60 years ago
- Large centered 220px cover art, anniversary badge, metadata grid, Last.fm summary, and full tracklist
- Random selection on each launch; Refresh (↻) button for another pick
- Click cover art to navigate to that record in the Collection tab

### 🗓️ Release Date Sync
- **Tools → Fetch MusicBrainz Release Dates**: batch cross-reference against MusicBrainz; progress in status bar
- **Tools → Fetch Last.fm Release Dates**: batch fetch, preserving MB-first priority

### 💾 Database Backup & Restore
- **Collection → Backup Database…**: hot-copies the live database, auto-stamped with date and time
- **Collection → Restore from Backup…**: validates, confirms, replaces, and reloads in-place
- Restore from backup also available on first launch

### 🎛️ Turntable Management
- Add, edit, and delete turntables (manufacturer, model, cartridge, stylus)
- **Set as Default**: pre-selected in Now Playing and used automatically when logging plays from queue
- Per-play turntable tracking with total play count and listening hours

### 🤖 AI Chat Assistant
- Dedicated **Ask AI** tab (⌘5) powered by Claude API (Sonnet) with streaming responses
- Five selectable offline local models (Apple Silicon via MLX)
- Speculative decoding for ~2-3× generation speedup
- Context-aware queries with keyword-filtered album context (cuts tokens ~90%)
- **AI can be fully disabled** via Settings → AI Features checkbox

### 🗂️ Navigation
- macOS menu bar: Collection, Tools, View (themes), and Tabs menus
- Keyboard shortcuts: ⌘1 Home · ⌘2 Collection · ⌘3 Statistics · ⌘4 Query · ⌘5 Ask AI · ⌘, Settings
- **Detachable tabs**: drag, right-click, or use ⌘⇧D to pop any tab into its own window; close to re-dock
- Main tab bar centered in the window header

### ⚙️ Settings & Authentication
- Discogs username and personal access token storage
- Claude API key configuration; Last.fm API key bundled and auto-stored on first launch
- Backend selection: Claude API or any of the 5 local models
- **AI Features toggle**: disable/re-enable the Ask AI tab
- **Danger Zone**: "Clear All Local Data" removes database, artwork cache, and all model caches

### 🎨 Appearance
- **22 selectable color themes** including System, Light, Default (Dark), Nord, Dracula, Monokai, and more
- Theme applies instantly across all widgets and persists across launches
- Window size, position, and all panel splitter sizes remembered across launches
- App version number displayed in the main window title bar

### 🚀 Performance
- SQLite WAL journal mode + 32 MB page cache + 256 MB memory-mapped I/O
- Two-pass query design for suggested album and queue fetches
- Write-behind batch DB optimisations across all sync workers

### 🗑️ Uninstall
- Included `Uninstall VinylTracker.command` script in the DMG
- Three modes: Complete Uninstall, Remove App Only, or Free Disk Space (AI model caches only)
