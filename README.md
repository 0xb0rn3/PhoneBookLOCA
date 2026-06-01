# PhoneBookLOCA v2.2.1

<div align="center">

```
╔════════════════════════════════════════════════════════════════╗
║  PhoneBookLOCA v2.2.1 — Full Open-Source OSINT Platform       ║
║  Worldwide Database + Advanced Intelligence Features           ║
╚════════════════════════════════════════════════════════════════╝
```

**Worldwide Phone Number OSINT — APIs · Social · Geolocation · Reports**

[![Python Version](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Go Version](https://img.shields.io/badge/go-1.19+-00ADD8.svg)](https://golang.org/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-active-success.svg)]()

*For authorized security research, penetration testing, and law enforcement use only.*

[Features](#features) • [Installation](#installation) • [Usage](#usage) • [Go Scraper](#go-scraper) • [API Keys](#api-keys) • [Changelog](#changelog)

</div>

---

## What is PhoneBookLOCA?

PhoneBookLOCA is an open-source OSINT platform for phone number intelligence. Feed it a number and it pulls carrier data, geolocation, social media presence, paste dump exposure, risk scoring, Google dorks, and structured HTML/JSON reports — all from a single command.

**Original tool:** DezTheJackal  
**Enhanced v1.1–v2.2.1:** 0xb0rn3 | 0xb0rn3

---

## Version History

| Version | Changes | Author |
|---------|---------|--------|
| v1.0 | Basic lookup, validation, carrier info | DezTheJackal |
| v1.1 | Go web scraper, API integration, concurrent OSINT | 0xb0rn3 \| 0xb0rn3 |
| v2.0 | SQLite caching, reputation engine, risk classification | 0xb0rn3 \| 0xb0rn3 |
| v2.1 | Enhanced geolocation, LE mode, missing persons features | DezTheJackal |
| v2.2 | Worldwide area-code DB, porting detection, batch analysis | DezTheJackal |
| **v2.2.1** | **Schema migration fix, HTML render fix, theHarvester bridge** | **0xb0rn3 \| 0xb0rn3** |

---

## Features

### Core Intelligence

- **Phone parsing & validation** via `phonenumbers` — carrier, type, timezone, country
- **Worldwide area-code database** — 80+ cities across North America, Europe, Asia, Africa, Middle East, Latin America, Oceania
- **Enhanced geolocation** — coordinate resolution from area code with ~50 km radius
- **Number porting detection** — flags VoIP and MVNO carriers as likely-ported

### OSINT Pipeline (`osint <number>`)

Runs four stages concurrently:

1. **Multi-API enrichment** — queries NumVerify, AbstractAPI, APILayer, Twilio Lookup, OSINT.club, and community caller/spam databases concurrently via `ThreadPoolExecutor`. Degrades gracefully — missing API keys skip that source, no crash.
2. **Social media probe** — public-endpoint checks across WhatsApp, Telegram, TrueCaller, Facebook, Twitter/X, Instagram, LinkedIn, and Pastebin dump indexes
3. **theHarvester bridge** — optional extended OSINT; if `theHarvester` is installed it runs silently as a subprocess against the number's carrier domain, extracting emails, hosts, and social references
4. **Profile build** — risk scoring (0–100), inferred attributes, 18 Google dorks, and lookup links aggregated into one structured object

### Go Web Scraper (`scraper.go`)

A standalone concurrent scraper written in Go — separate from the Python pipeline. See [Go Scraper](#go-scraper) for build instructions and integration details.

### Reports

- **JSON** — full structured profile saved to `~/.phonebookloca/reports/`
- **HTML** — self-contained report with risk badge, social table, dork links, and OSINT resource links
- Auto-saved on `osint`, `html`, and `le-mode` commands

### Batch Analysis

- Process a file of numbers in one run
- Pattern detection: same-carrier clustering (possible bulk SIM), geographic clustering
- Per-number reports when run with `--osint`

### Law Enforcement Mode

- Structured case intake: case number, officer, agency
- All LE cases stored in SQLite
- Automatically runs full OSINT profile + exports both JSON and HTML

### Database & Caching

- **SQLite backend** at `~/.phonebookloca/intel.db`
- Lookup cache with hit counter and timestamp
- Search history log (number, carrier, location, timestamp)
- Profile storage (full OSINT output per number)
- LE case tracker
- **v2.2.1: automatic schema migration** — existing databases from older versions are patched in-place on startup; no data loss, no manual intervention needed

---

## Installation

### Requirements

```
Python 3.8+
Go 1.19+   (only needed to build scraper.go)
```

### Python dependencies

```bash
pip3 install phonenumbers requests rich
```

Or via the included requirements file:

```bash
pip3 install -r requirements.txt
```

`rich` is optional but strongly recommended — without it the tool falls back to plain ANSI output.

### Quick start

```bash
git clone https://github.com/DezTheJackal/PhoneBookLOCA.git
cd PhoneBookLOCA
pip3 install -r requirements.txt
chmod +x PhoneBookLOCA
./PhoneBookLOCA +14155552671
```

### Optional: theHarvester

Enables extended domain OSINT in the `osint` pipeline.

```bash
# Kali / Debian
sudo apt install theharvester

# pip
pip3 install theHarvester
```

The tool auto-detects it on startup — no configuration required.

---

## Usage

### Command-line flags

```bash
./PhoneBookLOCA <number>                  # Basic lookup (cached)
./PhoneBookLOCA <number> --geo            # + enhanced geolocation + porting check
./PhoneBookLOCA <number> --osint          # Full OSINT pipeline + JSON report
./PhoneBookLOCA <number> --osint --html   # + HTML report
./PhoneBookLOCA <number> --no-cache       # Skip cache, fresh fetch
./PhoneBookLOCA <number> --dorks          # Print dorks and exit
./PhoneBookLOCA --batch numbers.txt       # Batch lookup
./PhoneBookLOCA --batch numbers.txt --osint  # Batch + full OSINT per number
./PhoneBookLOCA --le-mode                 # Law enforcement intake
./PhoneBookLOCA --keys                    # Show API key status
./PhoneBookLOCA --version                 # Print version
```

### Interactive mode

Run `./PhoneBookLOCA` with no arguments to enter the interactive shell:

```
PhoneBook> +255787066570          # Basic lookup
PhoneBook> geo +255787066570      # Enhanced geolocation
PhoneBook> osint +255787066570    # Full OSINT profile + HTML report
PhoneBook> html +255787066570     # Same as osint — always exports HTML
PhoneBook> dorks +255787066570    # Print dorks
PhoneBook> batch numbers.txt      # Batch from file
PhoneBook> le-mode                # LE case intake
PhoneBook> keys                   # API key status
PhoneBook> help                   # Command reference
PhoneBook> quit                   # Exit
```

### Example output: basic lookup

```
╭─────── Basic Intel ───────╮
│ Location   Tanzania        │
│ Code       +255            │
│ Carrier    Vodacom         │
│ Type       Mobile          │
│ Timezone   Africa/Dar_es.. │
╰───────────────────────────╯
```

### Example output: OSINT profile

```
[*] Querying OSINT APIs…        ✓  2 source(s) responded
[*] Probing social media…       ✓  1 confirmed hit(s)
[*] Extended OSINT [vodacom.tz] ✓  3 email(s), 2 social ref(s)

Risk: 35/100 — MEDIUM
  ! VoIP number — commonly used for anonymisation
  ! Number found in public paste dumps

Social Media:
  ✓ Truecaller   https://www.truecaller.com/search/us/...
  ? WhatsApp     Inconclusive — verify manually
  ✗ Pastebin     Not found in paste dumps

[+] JSON report: ~/.phonebookloca/reports/profile_+255..._20250601.json
[+] HTML report: ~/.phonebookloca/reports/profile_+255..._20250601.html
```

### Batch mode

```bash
# numbers.txt — one E.164 number per line
./PhoneBookLOCA --batch numbers.txt

# [*] Batch: 8 numbers
# [!] All on same carrier: Vodacom — possible bulk SIM
# [!] High geographic clustering detected
# [+] Valid: 8/8 | Carriers: 1 | Locations: 2
```

### LE mode

```bash
./PhoneBookLOCA --le-mode

Case Number  : MP-2025-042
Officer Name : Det. Mwangi
Agency       : TPF
Target Number: +255787066570

[+] Case created: MP-2025-042
[*] Running full OSINT profile…
[+] JSON report: ~/.phonebookloca/reports/profile_+255..._20250601.json
[+] HTML report: ~/.phonebookloca/reports/profile_+255..._20250601.html
```

---

## Go Scraper

`scraper.go` is a standalone concurrent web presence checker written in Go. It is **separate from the Python OSINT pipeline** — it does not run automatically when you use `osint` or `full_profile`. The Python tool has its own `SocialMediaProbe` class that handles social checks natively.

The Go scraper is an independent component you build and run directly, or wire into your own workflow.

### What it checks

Concurrently hits 8 targets via goroutines: Google (dork generation), Facebook, LinkedIn, Twitter/X, Instagram, TrueCaller, Pastebin dump index, and GitHub code search.

### Build

```bash
cd PhoneBookLOCA
go build -o scraper scraper.go
```

### Run

```bash
./scraper +255787066570
```

Output is clean JSON on stdout; progress goes to stderr so you can pipe the output directly:

```bash
./scraper +255787066570 | jq .
./scraper +255787066570 > results.json
```

### Output format

```json
{
  "phone_number": "+255787066570",
  "timestamp": "2025-06-01T14:32:00+03:00",
  "results": [
    {
      "source": "TrueCaller",
      "url": "https://www.truecaller.com/search/us/%2B255787066570",
      "found": true,
      "snippet": "May have caller-ID listing",
      "response_time": 0.84
    }
  ],
  "summary": {
    "total_sources": 8,
    "found_in": 3,
    "failed_sources": 1,
    "platforms_found": ["TrueCaller", "Pastebin", "GitHub"]
  }
}
```

### Limitations

Some sources (Google, Twitter/X, LinkedIn) block unauthenticated automated requests. The scraper documents this in its output and provides direct URLs for manual follow-up — it doesn't attempt auth bypass.

### Integrating with PhoneBookLOCA

To run both tools together in a shell pipeline:

```bash
NUMBER="+255787066570"
./PhoneBookLOCA "$NUMBER" --osint
./scraper "$NUMBER" | jq '.summary'
```

A future version may invoke the compiled scraper binary as a subprocess within the Python `full_profile` pipeline alongside `HarvesterBridge`, returning its structured JSON into the unified profile.

---

## API Keys

All keys are optional. The tool works without any — API sources are skipped gracefully when keys are absent.

### Environment variables

```bash
export NUMVERIFY_KEY="your_key"         # numverify.com — 100 req/mo free
export ABSTRACTAPI_KEY="your_key"       # abstractapi.com — free tier
export APILAYER_KEY="your_key"          # apilayer.com/marketplace/number_verification
export OPENCELLID_API_KEY="your_key"    # opencellid.org — 1000 req/day free
export TWILIO_ACCOUNT_SID="ACxxx"       # twilio.com — carrier lookup add-on
export TWILIO_AUTH_TOKEN="your_token"
export OSINT_CLUB_KEY="your_key"        # osint.club
```

### Config file

Alternatively, store keys in `~/.phonebookloca/config.json`:

```json
{
  "NUMVERIFY_KEY":   "abc123",
  "ABSTRACTAPI_KEY": "xyz789",
  "APILAYER_KEY":    "def456",
  "OPENCELLID_KEY":  "ghi012",
  "TWILIO_SID":      "ACxxx",
  "TWILIO_TOKEN":    "your_token",
  "OSINT_CLUB_KEY":  "jkl345"
}
```

Environment variables take priority over the config file.

Check current key status at any time:

```bash
./PhoneBookLOCA --keys
# or
PhoneBook> keys
```

---

## File Structure

```
PhoneBookLOCA/
├── PhoneBookLOCA         # Main Python tool (chmod +x)
├── scraper.go            # Standalone Go web scraper
├── requirements.txt      # Python dependencies
└── README.md
```

Runtime files (auto-created):

```
~/.phonebookloca/
├── intel.db              # SQLite — cache, history, profiles, LE cases
├── config.json           # API keys (optional)
└── reports/              # JSON + HTML output files
```

---

## Troubleshooting

**`sqlite3.OperationalError: table lookups has no column named ts`**

Your `intel.db` was created by an older version of the tool. Fixed in v2.2.1 — the migration runs automatically on startup. Just update to the latest version and rerun. If you prefer a clean slate:

```bash
rm ~/.phonebookloca/intel.db
./PhoneBookLOCA +14155552671
```

**`SyntaxError` on startup**

If you're running a version older than v2.2.1 downloaded before the fix, update to the current file. The f-string backslash issue in the HTML renderer is resolved in v2.2.1.

**theHarvester not running**

```bash
which theHarvester          # check PATH
pip3 install theHarvester   # or: apt install theharvester
./PhoneBookLOCA --keys      # extended OSINT status shows in banner
```

**Go scraper build fails**

```bash
go version                  # needs 1.19+
go build -o scraper scraper.go
```

**Poor geolocation precision**

Area-code resolution gives ~50 km radius. This is a structural limitation of the approach — without a carrier HLR query or cell tower data, the tool can only resolve to the area code's assigned geography. Enable OpenCellID for slightly tighter bounds when the number's tower data is available.

**OpenCellID returning nothing**

```bash
echo $OPENCELLID_API_KEY    # verify it's set
# Key must be active — register at opencellid.org
```

---

## What this tool does and does not do

**Does:**
- Estimate location from public area-code assignment data
- Identify carrier and number type (mobile, VoIP, fixed)
- Detect porting indicators (VoIP type, MVNO carrier)
- Check public social media endpoints and paste dump indexes
- Query opted-in phone intelligence APIs
- Generate investigative dorks and OSINT resource links
- Export structured JSON and HTML reports

**Does not:**
- Provide real-time GPS or device location
- Access live carrier network data
- Bypass authentication on any platform
- Replace lawful interception procedures
- Guarantee precision for ported numbers

For real-time location data, law enforcement must follow 18 U.S.C. § 2703 procedures and contact carrier legal compliance directly.

---

## Legal

MIT License. Free to use, modify, and distribute with attribution.

Use only on numbers you are authorized to investigate. Unauthorized use may violate computer fraud, wiretapping, and privacy laws in your jurisdiction.

---

## Credits

**DezTheJackal** — Original PhoneBookLOCA (v1.0), geolocation enhancements (v2.1), worldwide DB (v2.2)

**0xb0rn3 | 0xb0rn3** — Go scraper (v1.1), OSINT API broker, social probe, theHarvester bridge, profile/risk engine, HTML reporter, SQLite backend, schema migration (v2.0, v2.2.1)

---

<div align="center">

**PhoneBookLOCA v2.2.1**

DezTheJackal · 0xb0rn3 | 0xb0rn3

*Use responsibly. Follow legal procedures. Respect privacy.*

</div>
