# 📱 PhoneBookLOCA v2.2

<div align="center">

```ascii
╔═══════════════════════════════════════════════════════════════╗
║     PhoneBookLOCA v2.2 - Professional OSINT Platform          ║
║     Worldwide Database + Advanced Intelligence Features       ║
╚═══════════════════════════════════════════════════════════════╝
```

**🌍 Professional-Grade OSINT Intelligence Platform with Worldwide Coverage**

[![Python Version](https://img.shields.io/badge/python-3.6+-blue.svg)](https://www.python.org/downloads/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-active-success.svg)]()
[![Coverage](https://img.shields.io/badge/coverage-200%2B%20countries-brightgreen.svg)]()

*For educational, authorized security research, and law enforcement use only*

[Features](#-features) • [Installation](#-installation) • [Usage](#-usage) • [What’s New](#-whats-new-in-v22)

</div>

-----

## 🎯 What is PhoneBookLOCA v2.2?

PhoneBookLOCA v2.2 is a **professional-grade OSINT intelligence platform** for phone number reconnaissance with **worldwide database coverage** and **advanced analytics**. Created by DezTheJackal with continuous community enhancements.

### Evolution Timeline

|Version |Key Features                                               |Developer       |
|--------|-----------------------------------------------------------|----------------|
|**v1.0**|Basic phone lookup, validation, carrier info               |**DezTheJackal**|
|**v1.1**|OSINT queries, web scanning, API integration               |0xb0rn3 | 0xb0rn3 |
|**v2.0**|SQLite caching, reputation engine, ML classification       |0xb0rn3 | 0xb0rn3 |
|**v2.1**|🚨 Enhanced geolocation, LE tools, missing persons features |**DezTheJackal**|
|**v2.2**|🌍 **Worldwide database, porting detection, batch analysis**|**DezTheJackal**|

-----

## ✨ What’s New in v2.2

### 🌍 **Worldwide Database (Added by DezTheJackal)**

- **200+ countries** with comprehensive coverage
- **Major cities worldwide** with accurate coordinates
- **US/Canada expanded** - All 50 states + provinces
- **Europe** - UK, Germany, France, Spain, Italy, etc.
- **Asia** - Japan, China, India, South Korea, etc.
- **Americas** - Brazil, Mexico, Argentina, etc.
- **Middle East** - UAE, Saudi Arabia, Israel, Turkey
- **Africa** - South Africa, Egypt, Nigeria, Kenya
- **Oceania** - Australia, New Zealand

```bash
# Now works worldwide!
./PhoneBookLOCA +442071234567    # London, UK
./PhoneBookLOCA +81312345678     # Tokyo, Japan
./PhoneBookLOCA +61298765432     # Sydney, Australia
./PhoneBookLOCA +33145678901     # Paris, France
```

### 📡 **OpenCellID Integration (Optional)**

- **40 million+ cell towers** worldwide
- **Free API** with registration (1000 req/day)
- **Real tower data** instead of samples
- **Much better precision** (±5 km vs ±50 km)
- **Automatic integration** when API key configured

```bash
# Enable OpenCellID
export OPENCELLID_API_KEY="your_key_here"
./PhoneBookLOCA +14155552671 --geo

# Output includes real tower data:
📡 Cell Towers: 5 nearby
Primary Tower:
  • Distance: 2.3 km
  • Range: 1.5 km
  • Samples: 1547
```

### 🔄 **Number Porting Detection**

- **Detects carrier changes** automatically
- **Confidence scoring** (0-100%)
- **Warning system** for ported numbers
- **Historical tracking** of carrier changes
- **Critical for LE** - Area code may be wrong if ported

```bash
⚠️ Porting Detected:
Confidence: 75%
  • Carrier mismatch: Expected AT&T, found Verizon
  • MVNO carrier detected
  • Number likely ported - location may not match area code
```

### 📊 **Batch Analysis & Pattern Detection**

- **Analyze multiple numbers** at once
- **Geographic clustering** detection
- **Burner farm identification** (same carrier)
- **Risk scoring** with confidence levels
- **Pattern detection** for organized crime

```bash
# Create file with numbers
./PhoneBookLOCA --batch numbers.txt

# Output:
[!] Suspicious Patterns Detected:
  • High geographic clustering: 15 numbers in 2 locations
  • All 15 numbers on same carrier - possible bulk purchase
  • High VoIP usage: 12/15 numbers are VoIP
Risk Level: High
```

### 🔍 **Enhanced OSINT Automation**

- **Automated search queries** generation
- **Social media presence** checking
- **Data breach** correlation hints
- **Investigative recommendations**
- **Lookup URL generation** for multiple services

### 📜 **Historical Tracking System**

- **Tracks all lookups** with timestamps
- **Carrier change detection** over time
- **Location movement** tracking
- **Agency/case correlation**
- **Pattern analysis** across investigations

### 🔌 **Real-Time Carrier Integration (Framework)**

- **Emergency ping** request framework
- **CDR request** submission system
- **Carrier contact database** built-in
- **Legal procedure** documentation
- **Note:** Requires LE credentials for actual use

-----

## 🎨 Complete Feature Matrix

<table>
<tr>
<td width="50%">

### 🌍 Geographic Intelligence

- ✅ **200+ countries** coverage
- ✅ Worldwide area code database
- ✅ Accurate coordinates (lat/lon)
- ✅ City, region, country data
- ✅ Population & timezone info
- ✅ OpenCellID integration (40M+ towers)
- ✅ Cell tower proximity analysis
- ✅ Distance calculations

### 🔍 Advanced Analysis

- ✅ **Number porting detection**
- ✅ **Batch pattern analysis**
- ✅ Geographic clustering
- ✅ Burner farm detection
- ✅ Risk scoring (0-100)
- ✅ Confidence levels
- ✅ Historical tracking
- ✅ Carrier change detection

</td>
<td width="50%">

### 🚨 Law Enforcement Tools

- ✅ **Interactive LE mode**
- ✅ Case tracking & management
- ✅ Professional reports (JSON/CSV/HTML)
- ✅ Carrier legal contacts
- ✅ Emergency ping framework
- ✅ CDR request system
- ✅ Investigative recommendations
- ✅ Map link generation

### 📊 Intelligence Features

- ✅ **Enhanced OSINT automation**
- ✅ Social media queries
- ✅ Data breach hints
- ✅ Reputation scoring
- ✅ VoIP/disposable detection
- ✅ ML-powered classification
- ✅ Rich terminal UI
- ✅ SQLite caching (10x faster)

</td>
</tr>
</table>

-----

## 🚀 Installation

### Quick Start

```bash
# Clone repository
git clone https://github.com/DezTheJackal/PhoneBookLOCA.git
cd PhoneBookLOCA

# Install dependencies
pip3 install phonenumbers requests rich

# Make executable
chmod +x PhoneBookLOCA

# Test it
./PhoneBookLOCA +14155552671
```

### System-Wide Installation

```bash
# Install globally
sudo ./install.sh
# Choose option 2

# Use from anywhere
phonebookloca +14155552671
```

### Requirements

```
phonenumbers>=8.12.0    # Core phone number functionality
requests>=2.25.0        # HTTP requests  
rich>=13.0.0            # Enhanced terminal UI (optional but recommended)
```

### Optional: OpenCellID Setup

For **much better precision** with real cell tower data:

1. Register at https://opencellid.org/
1. Get free API key (1000 requests/day)
1. Set environment variable:

```bash
# Linux/Mac
export OPENCELLID_API_KEY="your_key_here"
echo 'export OPENCELLID_API_KEY="your_key"' >> ~/.bashrc

# Windows
set OPENCELLID_API_KEY=your_key_here
```

1. Run normally - tool auto-detects and uses API

-----

## 💡 Usage

### Basic Lookup (Worldwide)

```bash
# United States
./PhoneBookLOCA +14155552671

# United Kingdom
./PhoneBookLOCA +442071234567

# Japan
./PhoneBookLOCA +81312345678

# Australia
./PhoneBookLOCA +61298765432

# Germany
./PhoneBookLOCA +493012345678

# Output:
📊 Basic Intelligence
Country: United States (+1)
Carrier: Verizon Wireless
Type: Mobile
Timezone(s): America/Los_Angeles
```

### Enhanced Geolocation

```bash
./PhoneBookLOCA +14155552671 --geo

# Output includes:
📍 Enhanced Geolocation
Precision: area_code
Confidence: 70%
Radius: ±50 km

Coordinates:
  Lat: 37.774929
  Lon: -122.419418

Location:
  City: San Francisco
  Region: California
  Country: United States

📡 Cell Towers: 5 nearby (if OpenCellID enabled)

⚠️ Porting Analysis:
Likely Ported: Yes
Confidence: 75%

📜 Historical Data:
First seen: 2024-11-15
Total lookups: 8
Carrier changes: Detected
```

### Batch Analysis

Create `numbers.txt`:

```
+14155552671
+12125552671
+13105552671
+14695552671
+17135552671
```

Run:

```bash
./PhoneBookLOCA --batch numbers.txt

# Output:
Batch Analysis: 5 numbers
Valid Numbers: 5
Risk Level: Medium
Suspicious Patterns: 2

[!] Suspicious Patterns Detected:
  • High geographic clustering: 5 numbers in 2 locations
  • All 5 numbers on same carrier - possible bulk purchase

[+] Batch report saved: numbers_analysis.json
```

### Law Enforcement Mode

```bash
./PhoneBookLOCA --le-mode

# Interactive prompts:
🚨 LAW ENFORCEMENT MODE
Case Number: MP-2025-001
Officer Name: Det. Smith
Agency: SFPD
Case Type: missing person
Priority: high

Subject Phone Number: +14155552671

[+] Case created: ID 1
[*] Performing enhanced geolocation analysis...

[Comprehensive analysis with:]
- Enhanced geolocation
- Porting detection
- Historical tracking
- Cell tower analysis
- Carrier legal contacts
- Investigative recommendations

Export Options:
  1) JSON    2) CSV    3) HTML    4) All    5) Skip

[+] Reports saved to ~/.phonebookloca/reports/
```

### Interactive Mode

```bash
./PhoneBookLOCA

PhoneBook> +14155552671              # Standard lookup
PhoneBook> geo +14155552671          # Enhanced geo
PhoneBook> batch numbers.txt         # Batch analysis
PhoneBook> osint +14155552671        # OSINT queries
PhoneBook> le-mode                   # LE interface
PhoneBook> help                      # Show commands
PhoneBook> quit                      # Exit
```

### OSINT Intelligence

```bash
./PhoneBookLOCA +14155552671 --osint --geo

# Output includes:
[+] OSINT Intelligence:
  • Search queries generated (Google dorks)
  • Social media check URLs
  • Data breach recommendations
  • Lookup service URLs
  • Investigation suggestions
```

-----

## 📊 What You Get

### Standard Lookup

```
📊 Basic Intelligence
Country: United States (+1)
Location: San Francisco, CA
Carrier: Verizon Wireless
Type: Mobile
Timezone(s): America/Los_Angeles
```

### Enhanced Geolocation (–geo)

```
📍 Enhanced Geolocation
Precision: area_code
Confidence: 70%
Accuracy Radius: ±50 km

Coordinates:
  Latitude: 37.774929
  Longitude: -122.419418

Location:
  City: San Francisco
  County: San Francisco
  Region: California
  Country: United States
  Timezone: America/Los_Angeles

📡 Cell Towers: 5 nearby
Primary Tower:
  • ID: tower_sf_001
  • Distance: 2.3 km
  • Range: 5 km
  • Technology: 5G, LTE

⚠️ Porting Analysis:
Likely Ported: Yes (75% confidence)
Indicators:
  • Carrier mismatch: Expected AT&T, found Verizon
  • MVNO carrier detected
Warning: Number likely ported - location may not match area code

📜 Historical Data:
First Seen: 2024-11-15 14:30:00
Last Seen: 2025-01-20 10:15:00
Total Lookups: 8
Carrier Changes: Yes
Carriers Seen: AT&T, Verizon Wireless
Agencies: SFPD, FBI

⚖️ Legal Notice:
Public data only - For real-time tracking, obtain legal warrant
```

### Batch Analysis Report

```json
{
  "total_numbers": 15,
  "valid_numbers": 15,
  "geographic_clustering": {
    "unique_locations": 2,
    "most_common": [["San Francisco", 10], ["Oakland", 5]],
    "clustering_score": 0.67
  },
  "carrier_patterns": {
    "unique_carriers": 1,
    "same_carrier_percentage": 100.0
  },
  "risk_assessment": {
    "risk_score": 80,
    "risk_level": "High",
    "patterns_detected": 3
  },
  "suspicious_patterns": [
    "High geographic clustering: 15 numbers in 2 locations",
    "All 15 numbers on same carrier - possible bulk purchase",
    "High VoIP usage: 12/15 numbers are VoIP"
  ]
}
```

-----

## 🎯 Use Cases

### 🚨 Law Enforcement

#### Missing Persons Investigations

- **Initial location approximation** for deployment
- **Case documentation** with professional reports
- **Carrier contact info** for legal requests
- **Search area calculation** based on precision
- **Pattern detection** across multiple numbers
- **Historical tracking** of subject movements

#### Organized Crime / Trafficking

- **Batch analysis** of suspect numbers
- **Geographic clustering** detection
- **Burner farm identification**
- **Network relationship mapping**
- **Temporal pattern analysis**

#### Fraud Investigation

- **VoIP/disposable detection**
- **Porting pattern analysis**
- **Carrier reputation checking**
- **Geographic impossibility detection**

### 🔍 Security Research

#### OSINT Gathering

- **Target reconnaissance**
- **Social media correlation**
- **Data breach checking**
- **Attack surface mapping**

#### Threat Intelligence

- **Number pattern analysis**
- **Geographic distribution**
- **Carrier infrastructure mapping**
- **Historical tracking**

-----

## 🌍 Worldwide Coverage

### Regions Covered (200+ Countries)

**North America:** 🇺🇸 🇨🇦 🇲🇽  
All 50 US states, Canadian provinces, Mexico

**Europe:** 🇬🇧 🇩🇪 🇫🇷 🇪🇸 🇮🇹 🇳🇱 🇧🇪 🇨🇭 🇦🇹 🇵🇱 🇸🇪 🇳🇴 🇩🇰 🇫🇮 🇮🇪  
UK, Germany, France, Spain, Italy, Netherlands, Belgium, Switzerland, Austria, Poland, Sweden, Norway, Denmark, Finland, Ireland

**Asia:** 🇯🇵 🇨🇳 🇮🇳 🇰🇷 🇹🇭 🇲🇾 🇸🇬 🇵🇭 🇻🇳 🇮🇩 🇵🇰 🇧🇩  
Japan, China, India, South Korea, Thailand, Malaysia, Singapore, Philippines, Vietnam, Indonesia, Pakistan, Bangladesh

**Middle East:** 🇦🇪 🇸🇦 🇮🇱 🇹🇷 🇮🇷  
UAE, Saudi Arabia, Israel, Turkey, Iran

**Americas (South):** 🇧🇷 🇦🇷 🇨🇱 🇨🇴 🇵🇪 🇻🇪  
Brazil, Argentina, Chile, Colombia, Peru, Venezuela

**Africa:** 🇿🇦 🇪🇬 🇳🇬 🇰🇪 🇲🇦  
South Africa, Egypt, Nigeria, Kenya, Morocco

**Oceania:** 🇦🇺 🇳🇿  
Australia, New Zealand

-----

## 📖 Command Reference

### Command Line Options

```bash
# Single lookup
./PhoneBookLOCA <number>

# Enhanced geolocation
./PhoneBookLOCA <number> --geo

# Batch analysis
./PhoneBookLOCA --batch <file>

# OSINT intelligence
./PhoneBookLOCA <number> --osint --geo

# Law enforcement mode
./PhoneBookLOCA --le-mode

# Disable cache
./PhoneBookLOCA <number> --no-cache

# Interactive mode (default)
./PhoneBookLOCA
```

### Interactive Commands

```
<number>              Standard lookup
geo <number>          Enhanced geolocation
batch <file>          Batch analysis
osint <number>        OSINT intelligence
le-mode              Law enforcement interface
help                 Show commands
quit                 Exit
```

-----

## 🔧 Advanced Features

### OpenCellID Integration

**Free API** - 1000 requests/day  
**40M+ towers** worldwide  
**Real data** vs samples

```bash
# Setup
export OPENCELLID_API_KEY="your_key"

# Auto-enabled when key detected
./PhoneBookLOCA +14155552671 --geo
```

### Number Porting Detection

Automatically detects:

- Carrier mismatches
- MVNO patterns
- Historical porting
- Confidence scoring

### Batch Pattern Analysis

Detects:

- Geographic clustering
- Burner farms (same carrier)
- VoIP concentration
- Impossible travel
- Temporal patterns

### Historical Tracking

Tracks:

- All lookups with timestamps
- Carrier changes
- Location movements
- Agency access
- Case associations

-----

## 📈 Performance

|Operation          |v2.1     |v2.2                        |
|-------------------|---------|----------------------------|
|Standard lookup    |5-10s    |5-10s (first) / <1s (cached)|
|Enhanced geo       |5-10s    |3-8s (with OpenCellID)      |
|Batch (10 numbers) |N/A      |15-30s                      |
|Batch (100 numbers)|N/A      |2-5min                      |
|Worldwide coverage |US/Canada|200+ countries              |

### Cache Hit Rates

- **Investigation work:** 60-70%
- **Monitoring:** 80-90%
- **Historical analysis:** 95%+

-----

## 🔒 Legal & Privacy

### ⚖️ What This Tool Does

✅ Estimates location based on public data  
✅ Identifies area code geographic assignment  
✅ Detects number porting patterns  
✅ Analyzes carrier infrastructure (public)  
✅ Provides carrier legal contact info  
✅ Generates investigative leads

### ❌ What This Tool Does NOT Do

❌ Provide real-time GPS tracking  
❌ Access live carrier location data  
❌ Bypass legal warrant requirements  
❌ Guarantee precise device location  
❌ Replace proper legal procedures

### 📋 For Real-Time Tracking

Law enforcement MUST:

1. Obtain court order/warrant
1. Contact carrier legal compliance
1. Request emergency ping (life-threatening) OR CDR
1. Follow 18 U.S.C. § 2703 procedures

### Carrier Emergency Contacts (Built-in)

- **Verizon:** 1-888-483-7200 (24/7)
- **AT&T:** 1-800-635-6840 (24/7)
- **T-Mobile:** 1-888-987-4500 (24/7)

-----

## 🛠️ Troubleshooting

### Issue: Poor Worldwide Accuracy

**Solution:**

1. Enable OpenCellID for better precision
1. Check if number has been ported
1. Use `--no-cache` for fresh data
1. Some countries have limited data

### Issue: OpenCellID Not Working

```bash
# Check API key
echo $OPENCELLID_API_KEY

# Set if empty
export OPENCELLID_API_KEY="your_key"

# Test
./PhoneBookLOCA +14155552671 --geo
```

### Issue: Batch Analysis No Patterns

- Need minimum 5-10 numbers
- Numbers must be valid
- Patterns may not exist

### Issue: Database Errors

```bash
# Rebuild database
rm ~/.phonebookloca/intel.db
./PhoneBookLOCA +14155552671
```
'''
### Issue: SyntaxError: invalid character '"' (U+201C)

This occurs when smart quotes are present in the code. Fix it with:

**Quick Fix (One Command):**
```bash
sed -i "s/"/\"/g; s/"/\"/g; s/'/'/g; s/'/'/g" PhoneBookLOCA
chmod +x PhoneBookLOCA
```

**Or use the automatic fixer:**
bash
# Download the fix script
wget https://raw.githubusercontent.com/DezTheJackal/PhoneBookLOCA/main/fix_quotes.py

# Run it
python3 fix_quotes.py

# Done!
./PhoneBookLOCA +14155552671
```

The fixer will:
- ✓ Detect and count smart quotes
- ✓ Create automatic backup
- ✓ Replace all smart quotes with standard quotes
- ✓ Make the file executable
- ✓ Verify the fix worked
-----

## 🤝 Contributing

Contributions welcome!

1. Fork repository
1. Create feature branch
1. Make changes
1. Update documentation
1. Submit pull request

**Credit yourself in CONTRIBUTORS.md**

-----

## 📜 License

MIT License - See <LICENSE>

Free to use, modify, and distribute with attribution.

-----

## 👥 Credits & Attribution

### Creator

**DezTheJackal**

- Original PhoneBookLOCA concept (v1.0)
- v2.1 Law Enforcement Geolocation
- v2.2 Worldwide Database & Advanced Features

### Major Contributors

**0xb0rn3 | 0xb0rn3**

- v1.1 OSINT Features (Go scanner, API integration)
- v2.0 Intelligence Platform (caching, reputation, ML)

-----

## 📚 Documentation

- **README.md** - This file
- **SETUP_v2.2.md** - Installation & configuration guide
- **CHANGELOG.md** - Version history
- **CONTRIBUTORS.md** - Detailed contribution credits

-----

## 🔗 Links

- **Repository:** https://github.com/DezTheJackal/PhoneBookLOCA
- **Issues:** https://github.com/DezTheJackal/PhoneBookLOCA/issues
- **Releases:** https://github.com/DezTheJackal/PhoneBookLOCA/releases

-----

## ⚠️ Important Disclaimers

### For Law Enforcement

This tool provides **investigative leads** using publicly available data:

- Geographic approximations (not GPS)
- Requires legal authorization for real-time tracking
- Should supplement proper legal procedures
- Always follow local laws and regulations

### For Security Researchers

Authorized use only:

- ✅ Penetration testing (with permission)
- ✅ OSINT on public information
- ✅ Educational purposes
- ❌ Unauthorized tracking or stalking
- ❌ Privacy violations

### For General Users

- Use responsibly and ethically
- Respect privacy and legal boundaries
- For missing persons: Contact authorities
- For harassment: This is illegal

-----

<div align="center">

## 🌍 PhoneBookLOCA v2.2 - Worldwide OSINT Intelligence

**Professional-Grade Phone Number Intelligence**

*200+ Countries | 40M+ Cell Towers | Advanced Analytics*

**Created by: DezTheJackal**

v1.1-v2.0: 0xb0rn3 | 0xb0rn3 | v2.1-v2.2: DezTheJackal

⚖️ **Use responsibly. Follow legal procedures. Respect privacy.**

**⭐ Star this repo if you find it useful! ⭐**

</div>
