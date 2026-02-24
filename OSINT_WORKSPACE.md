# OSINT Investigation Workspace

## Purpose

This repo supports open source intelligence (OSINT) investigations using methodologies from the Bellingcat toolkit and broader OSINT community. Primary focus areas:

* Tracking federal detention facility expansion (property records, procurement, permits)
* Corporate/financial research on government contractors
* Geolocation and visual analysis from photographic evidence
* Cross-referencing public records across multiple databases

Collaborative project with Project Salt Box (Maryland-based volunteer OSINT group).

## My Skill Level

* Familiar with R for business analysis; new to Python and command-line tooling
* Explain what scripts do before running them — use clear comments in all code
* When installing tools, explain what each dependency does
* If something can be done simply, do it simply. Don't over-engineer.
* Prefer step-by-step workflows I can understand and repeat

## Project Structure

```
/data/{investigation-name}/       # Raw collected data per investigation
/data/{investigation-name}/notes/ # Methodology notes, hypothesis tracking
/outputs/                         # Analysis outputs, visualizations, reports
/scripts/                         # Reusable collection and analysis scripts
/tools/                           # Local tool configs and setup notes
```

## Key Installable OSINT Tools (from Bellingcat Toolkit)

These are command-line / Python tools that can run locally. Install as needed, not all at once.

### Corporate & Financial Research

* **edgar-tool** (PyPI: edgar-tool) — CLI for SEC EDGAR filings. Query corporate/financial data.
  Source: https://pypi.org/project/edgar-tool/
  Guide: https://bellingcat.gitbook.io/toolkit/more/all-tools/edgar-suite

### Username & Person Research

* **Maigret** (github.com/soxoj/maigret) — Search usernames across hundreds of sites.
  Guide: https://bellingcat.gitbook.io/toolkit/more/all-tools/maigret
* **Sherlock** (github.com/sherlock-project/sherlock) — Username search across 400+ sites.
  Guide: https://bellingcat.gitbook.io/toolkit/more/all-tools/sherlock
* **Blackbird** (github.com/p1ngul1n0/blackbird) — Username and email search.
  Guide: https://bellingcat.gitbook.io/toolkit/more/all-tools/blackbird
* **holehe** (github.com/megadose/holehe) — Check which sites an email is registered on.
* **GHunt** (github.com/mxrch/GHunt) — Google account information gathering.
  Guide: https://bellingcat.gitbook.io/toolkit/more/all-tools/ghunt

### Archiving & Evidence Preservation

* **Auto Archiver** (github.com/bellingcat/auto-archiver) — Archive social media posts/videos/images.
  Guide: https://bellingcat.gitbook.io/toolkit/more/all-tools/auto-archiver
* **youtube-dl / yt-dlp** — Download video/audio from many platforms.
* **Wayback Machine** has a Python API (waybackpy) for programmatic archiving.

### Geolocation & Mapping

* **Shadow Finder** (github.com/bellingcat/ShadowFinder) — Map possible locations based on shadow length at a given date/time.
  Guide: https://bellingcat.gitbook.io/toolkit/more/all-tools/shadow-finder
* **Instagram Location Search** (github.com/bellingcat/instagram-location-search) — Find Instagram location tags near coordinates.
  Guide: https://bellingcat.gitbook.io/toolkit/more/all-tools/instagram-location-search
* **folium** (PyPI) — Create interactive maps in Python. Good for plotting facility locations.
* **QGIS** — Full desktop GIS application for spatial analysis (install separately, not via pip).

### Telegram Research

* **Telepathy** (github.com/proseltd/Telepathy-Community) — Archive chats, gather memberlists, map messages.
  Guide: https://bellingcat.gitbook.io/toolkit/more/all-tools/telepathy
* **Telegram Phone Number Checker** (Bellingcat Colab notebook) — Check phone numbers against Telegram.
  Guide: https://bellingcat.gitbook.io/toolkit/more/all-tools/telegram-phone-number-checker

### Credential & Breach Research

* **TruffleHog** (trufflesecurity.com/trufflehog) — Find leaked credentials.
  Guide: https://bellingcat.gitbook.io/toolkit/more/all-tools/trufflehog

### Metadata & Forensics

* **jhead** — CLI EXIF metadata viewer/remover.
* **InVID/WeVerify plugin** — Browser-based video/image verification (not CLI, but essential).

## Key Web APIs to Script Against

These aren't installable tools but have APIs or scrapable interfaces:

* **USASpending.gov** — Federal contract/grant data (REST API: api.usaspending.gov)
* **SAM.gov** — Federal procurement opportunities (API available with registration)
* **OpenCorporates** — Global corporate registry (API: api.opencorporates.com)
* **OCCRP Aleph** — Sanctions, registries, leaks (API: aleph.occrp.org/api)
* **OpenSanctions** — Sanctions/PEP data (API: api.opensanctions.org)
* **ACLED** — Conflict event data (API available with free registration)
* **UN Comtrade** — Global trade data (API: comtradeplus.un.org)
* **ICIJ Offshore Leaks** — Offshore entities database (downloadable data)
* **Wayback Machine** — CDX API for checking archived pages

## Key Web-Only Tools (No CLI, but reference frequently)

These require manual browser use but are core to investigations:

* **Maryland SDAT** — Property records (JavaScript-heavy, hard to scrape)
* **Google Earth Pro** — Historical satellite imagery, 3D terrain
* **Bellingcat OSM Search** (osm-search.bellingcat.com) — Proximity feature search
* **SunCalc** (suncalc.org) — Sun position and shadow modeling
* **ShadowMap** (app.shadowmap.org) — 3D building shadow simulation
* **GeoHints** (geohints.com) — Visual clue reference for geolocation
* **Forensically** (29a.ch/photo-forensics) — Image forensics
* **OSINT Tools Map** (cybdetective.com/osintmap) — Business registries by country
* **LittleSis** (littlesis.org) — US political/business relationship mapping
* **OpenSecrets** (opensecrets.org) — US campaign finance and lobbying data

## Data Handling Rules

* **NEVER** commit API keys or credentials. Use environment variables or a `.env` file (gitignored).
* **NEVER** commit personal data about private individuals. Keep in `/data/` which is gitignored.
* Raw data files (CSVs, JSONs, images) go in `/data/`, not tracked by git.
* Only commit scripts, documentation, and sanitized/aggregated outputs.

## Investigation Methodology

* Document every step: what was searched, when, what was found or not found
* Cross-reference findings across at least 2 independent sources before treating as confirmed
* Archive/screenshot evidence at time of discovery (pages change or disappear)
* Track hypotheses explicitly — note when evidence supports or contradicts them
* Acknowledge tool limitations honestly rather than presenting overconfident conclusions

## Common Workflows

### New Investigation Setup

1. Create `/data/{investigation-name}/` directory
2. Create a `notes/README.md` documenting the target, starting evidence, and success criteria
3. Begin with open-source collection before any tool-assisted scraping

### Property/Facility Tracking

1. Collect addresses and parcel IDs from property databases (manual — SDAT is JS-heavy)
2. Structure in CSV: address, owner, transfer_date, assessed_value, permits, notes
3. Cross-reference owners against corporate registries (OpenCorporates, EDGAR)
4. Check for federal contracts tied to same entities (USASpending API)
5. Map locations with folium, overlay with satellite imagery for visual confirmation

### Person/Entity Research

1. Start with known identifiers (name, email, username, phone)
2. Run username enumeration (Maigret or Sherlock)
3. Check corporate affiliations (OpenCorporates, EDGAR, LittleSis)
4. Check sanctions/PEP lists (OpenSanctions)
5. Document network connections — who appears alongside this person/entity

## Python Environment

Use a virtual environment. Key base packages:

* **requests**, **beautifulsoup4** (web scraping basics)
* **pandas** (data analysis — similar to R dataframes)
* **playwright** (for JavaScript-heavy government sites that need a real browser)
* **folium** (interactive mapping)
* **python-dotenv** (managing API keys safely)
