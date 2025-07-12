# RipBox GUI

A minimalist, web-based GUI for building reliable and repeatable `HandBrakeCLI` commands to rip DVDs for archival, media servers, or personal collections.

This tool is designed for users running **Linux-based home media servers (e.g., Jellyfin setups)** who want a quick and human-friendly interface to generate correct CLI commands with consistent output structure, subtitles, and folder organization.

---

## Features

- 🖥️ **Simple single-page web app** — no backend required, runs locally in any modern browser.
- 📝 **Auto-build `mkdir`, `HandBrakeCLI`, and `ffprobe` commands** ready to paste into your terminal.
- 🔤 **Optional subtitle track selection** — define subtitle tracks if needed.
- 🔒 **No burn-in subtitles by default** — subtitles embedded as selectable tracks if present.
- 📋 **One-click copy buttons** with tooltip feedback.
- 📺 **TV Show support** — season and episode fields enable correct folder structure and file naming for series

---

## Why?

Manually preparing consistent `HandBrakeCLI` commands can be repetitive and error-prone, especially when ensuring:

- Proper subtitle handling
- Reliable command syntax
- Consistent folder structure for movies

This project provides a lightweight, fast, and shareable workflow assistant so you can focus on efficient ripping and enjoy your media collection faster.

---

## Getting the DVD Name

For consistency and better metadata matching in media servers like Jellyfin, it’s worth searching for the correct title and year on a trusted source such as **IMDB** or **The Movie Database (TMDb)**.

✅ Example workflow:
1️⃣ Search for the film or series on [IMDB](https://www.imdb.com) or [The Movie Database](https://www.themoviedb.org).  
2️⃣ Copy the official title exactly as shown, including the year in parentheses — e.g., `Batman & Robin (1997)`.  
3️⃣ Paste this value directly into the **DVD Name** field of the GUI.

This ensures reliable matching during metadata scans.

## Usage

The target directory is very opinionated to suit my setup, but if you download the code, you can make the required changes to suit your setup.

### Open the GUI:  
You can use this tool online at: [https://seemly.github.io/handbrake-cli-helper/](https://seemly.github.io/handbrake-cli-helper/)

### Get Disc Titles
Copy the 'Get Disc Titles' command, paste that into your terminal, and await the response. Decide which title is the likely candidate for ripping/transcoding.

### Fill in:
- Name (e.g., `The Terminator (1984)`)
- Title (always required). This is defined by the CLI output from step 2.
- If applicable, Season and Episode numbers (shown automatically when needed)
- Optional subtitle tracks
  (If no subtitle track selection is provided, subtitles will not be included in the generated command)

### Make Folder
Copy and paste the generated 'Make Folder Command' directly into your terminal to create the DVD target directory.

### Rip Command
Copy and paste the generated 'Rip Command' directly into your terminal to rip/transcode the DVD to the target directory on your media server.

---

## Known issues with subtitles on older DVDs

Not related to this project at all, but something to be aware of:

Many older DVDs use bitmap-based subtitle tracks (VOBSUB), and their structure can vary widely between discs:

- Some contain multiple redundant subtitle tracks (e.g., "Wide Screen", "Letterbox") that require manual inspection.
- Some lack proper language tags or subtitle flags.
- HandBrakeCLI’s `--subtitle-lang-list eng --all-subtitles` works well for most modern discs but may fail or behave unexpectedly on older titles.
- If subtitle tracks aren’t properly flagged on the disc, subtitles may not be embedded automatically even if they exist.

**Recommendation:**  
Before ripping older discs, run a title scan first:

```bash
HandBrakeCLI -i /dev/sr0 -t 0 --min-duration 300
```

Then review subtitle track numbers manually and adjust your `--subtitle` options accordingly in the generated rip command.