# VinylTracker

A native macOS app for managing your vinyl record collection.

## Download

👉 **[Latest Release](https://github.com/mrpatrickstaresq/vinyltracker-releases/releases/latest)**

| Mac | Download |
|-----|----------|
| Apple Silicon (M1/M2/M3/M4) | `VinylTracker-AppleSilicon.dmg` — full features including AI |
| Intel | `VinylTracker-Intel.dmg` — all features except AI chat |

1. Open the DMG and drag VinylTracker to Applications
2. Launch from Applications

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
- **Export Collection as CSV**: saves a dated CSV file with all metadata expanded — including pressing credits, personnel, barcodes, and liner notes

### 🔍 Query Builder
- Dedicated **Query tab** (⌘5) with eight ready-to-run query panels:
  1. **By Artist** — substring matching returns all related ensembles
  2. **By Genre / Style** — genre and style dropdowns with "Any" option
  3. **By Decade** — 50s through 2020s
  4. **Never Played** — one-click, no inputs required
  5. **Most / Least Played** — direction toggle and top-N count
  6. **By Label** — label dropdown populated from your collection
  7. **Not Played Since** — 1 month / 3 months / 6 months / 1 year / 2 years / 3 years
  8. **Advanced** — stack any number of AND conditions: Field | Operator | Value; supports text, year range, play counts, never-played, and not-played-in-N-days filters
- Results shown in a sortable, resizable table — double-click any row to jump to that album
- **⭐ Save** button pins named queries; **Recent Queries** shows last 20 runs

### 🖼️ Cover Art & Artwork
- Cover art fetched from Discogs using the primary front-cover image; falls back to MusicBrainz / Cover Art Archive
- Per-record on-demand background fetch; batch sync for missing artwork
- **Tools → Sync Album Artwork / Sync Tracklists**: targeted workers with status bar progress
- **Tools → Sync Album Artwork from Apple**: iTunes-powered, no rate limit, covers most mainstream releases instantly
- **Tools → Sync Album Artwork from Discogs**: for obscure or rare releases Apple doesn't have; uses Discogs with MusicBrainz/Cover Art Archive as fallback
- On first launch after import, the missing artwork prompt offers Apple sync with Discogs as a follow-up option
- Artwork sync year fetching removed; handled separately by dedicated year sync workers
- **Tracklist sync** uses cached Discogs release ID (from pressing info sync) to skip the search step — 1 API call instead of 2 for already-synced records

### 🎵 Metadata Enrichment
- Original release year from MusicBrainz; falls back to Last.fm — Discogs year ignored
- Album runtime calculated from track durations; full tracklist with vinyl side grouping

### 🏭 Pressing Details
- Pressing Details, Personnel Credits, Barcodes, and Liner Notes in the Now Playing panel
- Loaded instantly from local cache; auto-synced from Discogs in background on first view
- **Tools → Sync Pressing Info / Personnel Credits / Barcodes**
- All three sync workers terminate correctly when the API has no data for a record; personnel/barcodes workers never overwrite existing pressing data on a failed retry

### ▶️ Now Playing Panel
- Large 360px cover art; full metadata grid, tracklist, and pressing details
- **Log Play** with turntable selector — pre-selects your default turntable
- **＋ My Listening Queue** button

### 📋 Play History
- Dedicated **Play History tab** (⌘4) — sortable 6-column table (Played On · Artist · Title · Runtime · Turntable · Genre)
- 4 metric cards: Total Plays, Listening Time, This Month, Best Month
- Filter by text search or turntable; Export CSV; multi-select delete
- Column widths saved between sessions
- Charts: Top Artists, Top Albums, Plays by Month, Day of Week, Genre
- Compact 20-row summary panel in the Collection tab

### 🏠 Home Dashboard
- Three-column layout: Last Played (full detail) | Suggested Spins + Album Anniversary | Listening Queue
- Logging a play from any panel refreshes all Home tab panels automatically

### 📥 Listening Queue
- **My Queue** (manual): curated ordered list up to 50 albums; drag to reorder
- **Suggested** (auto): 20 albums unplayed for 182+ days, randomised, no duplicate artists

### 📊 Statistics Dashboard
- 4 metric cards: Records, Artists, Never Played, Avg Album Runtime — update live on play logged
- Genre donut, Decade bar, Collection by Artist, Collection by Label, Lacquer Engineers, New Albums by Month
- Recently-added album tables (30 days + 12 months)
- All charts at consistent 300px height; full multicolor palette throughout

### 🎂 Album Anniversary Panel
- Highlights a random album released exactly 10, 20, 30, 40, 50, or 60 years ago
- Cover art, anniversary badge, Last.fm summary, tracklist; click to navigate to record

### 🗓️ Release Date Sync
- **Tools → Fetch MusicBrainz Release Dates** and **Fetch Last.fm Release Dates**

### 💾 Database Backup & Restore
- Hot-copy backup with timestamp; restore in-place; also available on first launch

### 🎛️ Turntable Management
- Add/edit/delete turntables; set a default; per-play tracking with total hours

### 🤖 AI Chat Assistant *(Apple Silicon only)*
- Dedicated **Ask AI** tab (⌘6) — Claude API (Sonnet) with streaming responses
- Five selectable offline local models (Apple Silicon via MLX): Llama, Qwen, Phi, Gemma variants
- Speculative decoding for ~2-3× generation speedup
- Context-aware queries with keyword-filtered album context (cuts tokens ~90%)
- **AI can be fully disabled** via Settings → AI Features checkbox
- Settings dialog is fully functional on Intel — AI-specific sections are automatically hidden when not applicable

### 🗂️ Navigation
- Keyboard shortcuts: ⌘1 Home · ⌘2 Collection · ⌘3 Statistics · ⌘4 Play History · ⌘5 Query · ⌘6 Ask AI · ⌘, Settings
- **Detachable tabs**: drag, right-click, or ⌘⇧D to pop any tab into its own window
- Centered tab bar; macOS standard close behaviour (hide to Dock)

### ⚙️ Settings & Authentication
- Discogs token; Claude API key; Last.fm key bundled and auto-stored on first launch
- **Danger Zone**: "Clear All Local Data" removes database, artwork cache, and all model caches

### 🎨 Appearance
- **22 selectable color themes** including System, Light, Default (Dark), Nord, Dracula, Monokai, and more
- Window size, position, and all panel splitter sizes remembered across launches

### 🚀 Performance
- SQLite WAL mode + 32 MB page cache + 256 MB memory-mapped I/O
- Two-pass query design; write-behind batch DB optimisations across all sync workers

### 🗑️ Uninstall
- Included `Uninstall VinylTracker.command` in the DMG
- Three modes: Complete Uninstall, Remove App Only, or Free Disk Space (AI model caches only)
