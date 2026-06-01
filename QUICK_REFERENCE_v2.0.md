# PhoneBookLOCA v2.0 - Quick Reference

## 🚀 Fast Command Reference

### Basic Usage

```bash
# Standard lookup (uses cache automatically)
phonebookloca +14155552671

# Full intelligence (reputation + OSINT + web scan)
phonebookloca +14155552671 --osint --reputation --web-scan

# Force fresh data (bypass cache)
phonebookloca +14155552671 --no-cache
```

---

## 💾 Cache Management

```bash
# Show cache statistics
phonebookloca --cache-stats

# Clear entries older than 30 days (default)
phonebookloca --clear-cache

# Clear entries older than 7 days
phonebookloca --clear-cache 7

# Interactive mode
phonebookloca
PhoneBook> cache              # Show stats
PhoneBook> clear-cache 14     # Clear 14+ day old entries
```

---

## 📊 What You Get

### Basic Intelligence (Always Included)

```
📊 Basic Intelligence
├─ Country: United States (+1)
├─ Location: San Francisco, CA
├─ Carrier: Verizon Wireless
├─ Type: Mobile
└─ Timezone(s): America/Los_Angeles
```

### Carrier Intelligence (v2.0 - Always Included)

```
📡 Carrier Intelligence
├─ Type: MNO (Mobile Network Operator)
├─ Technology: 5G, LTE, 4G, 3G
├─ Coverage: North America
├─ MVNO Parent: None (or parent if MVNO)
└─ Security: STIR/SHAKEN, Spam Blocking
```

### Risk Assessment (v2.0 - Always Included)

```
⚠️ Risk Assessment
├─ Risk Level: Low Risk (green) / Medium (yellow) / High (red)
├─ Risk Score: 25/100
├─ Sub-types: Personal, Verified
├─ Confidence: 92%
└─ Recommendations:
    ✓ Safe for outbound contact
    ✓ Low spoofing risk
```

### Reputation Analysis (With --reputation flag)

```
🛡️ Reputation Analysis
├─ Overall Score: 78.5/100
├─ Risk Level: Low
├─ Sources Checked: 6
├─ Sources Responded: 5
├─ Confidence: 83%
└─ Reports:
    • Spam: 1
    • Scam: 0
    • Legitimate: 8
```

---

## ⚡ Performance Tips

### 1. Let Cache Work

```bash
# First lookup: 5-10 seconds (fetches and caches)
phonebookloca +14155552671

# Subsequent lookups: <1 second (from cache)
phonebookloca +14155552671
# ⚡ Cache hit! Data age: 2.3 hours
```

### 2. Batch Processing

```bash
# Create list
cat > numbers.txt << EOF
+14155552671
+442071838750
+33142869000
EOF

# Process with caching (fast for repeats)
phonebookloca -b numbers.txt -o results.json

# Force fresh for all
phonebookloca -b numbers.txt --no-cache -o results.json
```

### 3. Cache Maintenance

```bash
# Weekly: Clear old entries
phonebookloca --clear-cache 7

# Check cache efficiency
phonebookloca --cache-stats
# Target: 60-80% hit rate for investigations
```

---

## 🎯 Common Workflows

### Workflow 1: Quick Target Check

```bash
# Single number, full intel
phonebookloca +14155552671 --osint --reputation
```

### Workflow 2: Deep Investigation

```bash
# First pass: Basic info
phonebookloca +14155552671

# Second pass: Full OSINT with web scan
phonebookloca +14155552671 --osint --reputation --web-scan

# Force fresh if needed
phonebookloca +14155552671 --no-cache --osint --reputation
```

### Workflow 3: Bulk Analysis

```bash
# Extract from breach data
phonebookloca --scan breach_dump.txt -o extracted.txt

# Analyze all (uses cache for speed)
phonebookloca -b extracted.txt -o intel.json --reputation

# Export to CSV for Excel
phonebookloca -b extracted.txt -o intel.csv -f csv
```

### Workflow 4: Monitoring

```bash
# Interactive session
phonebookloca

PhoneBook> osint +14155552671     # Check target
PhoneBook> cache                  # Monitor cache
PhoneBook> osint +14155552671     # Check again (instant)
PhoneBook> clear-cache 7          # Weekly cleanup
PhoneBook> quit
```

---

## 📈 Understanding Scores

### Reputation Score (0-100)

| Range | Level | Meaning |
|-------|-------|---------|
| 80-100 | Very Low Risk | Trusted, verified number |
| 60-79 | Low Risk | Generally safe |
| 40-59 | Medium Risk | Unknown, proceed with caution |
| 20-39 | High Risk | Multiple spam reports |
| 0-19 | Very High Risk | Known scam/spam number |

**Formula:**
- Base: 50 (neutral)
- Spam report: -3 each
- Scam report: -5 each
- Legitimate report: +2 each
- Normalized to 0-100

### Risk Score (0-100)

| Range | Category | Action |
|-------|----------|--------|
| 0-29 | Low Risk | Safe to contact |
| 30-59 | Medium Risk | Verify first |
| 60-100 | High Risk | Avoid or investigate |

**Factors:**
- +20 if VoIP/virtual
- +10 if toll-free
- +30 if poor reputation (<30)
- -20 if good reputation (>70)

### Confidence Score (0-100%)

| Range | Meaning |
|-------|---------|
| 90-100% | Highly reliable |
| 70-89% | Reliable |
| 50-69% | Moderate confidence |
| 30-49% | Low confidence |
| 0-29% | Very uncertain |

**Based on:**
- Number of sources checked
- Sources that responded
- Data consistency
- Cache freshness

---

## 🎨 Rich UI vs Basic

### With Rich Library

```bash
pip3 install rich
phonebookloca +14155552671
```

**Output:**
```
╭──────────────────────────────────╮
│     📊 Basic Intelligence        │
├──────────────────────────────────┤
│ Country: United States (+1)      │
│ Carrier: Verizon Wireless        │
│ Type: Mobile                      │
╰──────────────────────────────────╯

╭──────────────────────────────────╮
│      ⚠️ Risk Assessment          │
├──────────────────────────────────┤
│ Risk Level: Low Risk              │
│ Risk Score: 25/100                │
╰──────────────────────────────────╯
```

### Without Rich (Basic Fallback)

```
[+] Results:
    Country Code: +1
    Carrier: Verizon Wireless
    Type: Mobile

[*] Risk Assessment:
    Risk Level: Low Risk
    Risk Score: 25/100
```

**Both work perfectly!** Rich just makes it prettier.

---

## 🔍 Carrier Intelligence Guide

### MNO vs MVNO

**MNO (Mobile Network Operator):**
- Own network infrastructure
- Examples: Verizon, AT&T, T-Mobile, Vodafone
- Direct control over network

**MVNO (Mobile Virtual Network Operator):**
- Use MNO network infrastructure
- Examples: Mint Mobile, Cricket, Metro, Visible
- Resell MNO services

### Network Technology

| Technology | Speed | Year |
|------------|-------|------|
| 5G | Up to 10 Gbps | 2019+ |
| LTE/4G | Up to 100 Mbps | 2010+ |
| 3G | Up to 2 Mbps | 2003+ |

### Security Features

- **STIR/SHAKEN**: Caller ID authentication
- **Spam Blocking**: Automatic spam detection
- **Scam Shield**: Scam call protection

---

## 💡 Pro Tips

### Tip 1: Cache Freshness

```bash
# Sensitive lookups: Always fresh
phonebookloca +14155552671 --no-cache --reputation

# Regular intel: Let cache work
phonebookloca +14155552671
```

### Tip 2: Reputation Checking

```bash
# For unknown numbers, always check reputation
phonebookloca +14155552671 --reputation

# For OSINT, reputation is included
phonebookloca +14155552671 --osint  # includes reputation
```

### Tip 3: Batch Efficiency

```bash
# First run: Cache everything
phonebookloca -b large_list.txt -o results.json

# Second run: Instant results
phonebookloca -b large_list.txt -o results2.json
# Uses cache for all previously looked-up numbers
```

### Tip 4: Cache Hit Rate

```bash
# Check your efficiency
phonebookloca --cache-stats

# Good: 60-80% (investigation work)
# Excellent: 80-95% (monitoring)
# Low (<40%): Consider longer cache age or adjust workflow
```

### Tip 5: Interactive Mode

```bash
# Best for research sessions
phonebookloca

# Commands remember context
PhoneBook> osint +14155552671     # Full scan
PhoneBook> osint +14155552671     # Instant (cached)
PhoneBook> cache                  # Check efficiency
```

---

## 🚨 Troubleshooting Quick Fixes

### Cache Not Working

```bash
# Check if database exists
ls ~/.phonebookloca/intel.db

# Check stats
phonebookloca --cache-stats

# Rebuild cache
rm ~/.phonebookloca/intel.db
phonebookloca +14155552671  # Creates fresh
```

### Slow Performance

```bash
# Clear old cache
phonebookloca --clear-cache 7

# Check cache stats
phonebookloca --cache-stats

# If needed, rebuild
rm ~/.phonebookloca/intel.db
```

### Rich UI Not Showing

```bash
# Install Rich
pip3 install rich

# Verify installation
python3 -c "import rich; print('Rich OK')"

# Still works without Rich!
```

---

## 📊 Cache Statistics Explained

```bash
phonebookloca --cache-stats
```

**Output:**
```
💾 Cache Statistics
Total Cached: 47              # Total numbers in cache
Fresh Entries: 38             # Within 24 hours (default)
Stale Entries: 9              # Older than 24 hours
Average Confidence: 82%       # Data quality average
Total Lookups: 156            # All-time lookup count
Cache Hit Rate: 65.3%         # How often cache is used
```

**What's Good:**
- **Hit Rate 60-80%**: Efficient for investigations
- **Hit Rate 80-95%**: Excellent for monitoring
- **Average Confidence >70%**: High data quality
- **Stale Entries <20%**: Good cache maintenance

**What Needs Attention:**
- **Hit Rate <40%**: Too many unique numbers or cache too aggressive
- **Stale Entries >50%**: Need to run `--clear-cache`
- **Average Confidence <50%**: Mixed quality sources

---

## 🎯 Decision Matrix

### When to Use --no-cache?

| Scenario | Use Cache? | Why |
|----------|-----------|-----|
| Routine investigation | ✅ Yes | Speed matters |
| Critical security incident | ❌ No | Need fresh data |
| Historical analysis | ✅ Yes | Data unlikely to change |
| Real-time threat hunting | ❌ No | Need current intel |
| Bulk processing | ✅ Yes | Efficiency critical |
| Single VIP target | ❌ No | Accuracy critical |
| Reputation check | ✅ Yes | Aggregate data stable |
| Monitoring loop | ✅ Yes | Cache prevents rate limits |

### When to Check Reputation?

| Scenario | Check Reputation? | Why |
|----------|------------------|-----|
| Unknown caller | ✅ Yes | Identify spam/scam |
| Contact from breach | ✅ Yes | Verify legitimacy |
| Business contact | ⚠️ Optional | Usually clean |
| Known friend/family | ❌ No | Not needed |
| Bulk screening | ✅ Yes | Find bad actors |
| Investigation target | ✅ Yes | Complete intel |

### When to Use OSINT Mode?

| Scenario | OSINT Mode? | Why |
|----------|------------|-----|
| Deep investigation | ✅ Yes | Need all intel |
| Quick check | ❌ No | Basic lookup enough |
| Social engineering test | ✅ Yes | Need context |
| Threat actor profiling | ✅ Yes | Complete picture |
| Routine verification | ❌ No | Overkill |
| Pre-call screening | ⚠️ Optional | Depends on context |

---

## 🔗 File Locations

```bash
# Cache database
~/.phonebookloca/intel.db

# Configuration (API keys)
~/.phonebookloca_config.json

# System-wide installation (if used)
/usr/local/bin/phonebookloca
/usr/local/share/phonebookloca/scraper
```

---

## 📖 Interactive Mode Commands

```
PhoneBook> +14155552671          # Standard lookup
PhoneBook> osint +14155552671    # OSINT + reputation
PhoneBook> reputation +number    # Reputation only
PhoneBook> cache                 # Show cache stats
PhoneBook> clear-cache           # Clear 30+ days
PhoneBook> clear-cache 7         # Clear 7+ days
PhoneBook> help                  # Show all commands
PhoneBook> quit                  # Exit
```

---

## 🎓 Learning Path

### Beginner (Day 1)

```bash
# 1. Basic lookup
phonebookloca +14155552671

# 2. Check cache
phonebookloca --cache-stats

# 3. Second lookup (notice speed)
phonebookloca +14155552671
```

### Intermediate (Week 1)

```bash
# 1. Full intelligence
phonebookloca +14155552671 --osint --reputation

# 2. Batch processing
phonebookloca -b numbers.txt -o results.json

# 3. Cache management
phonebookloca --clear-cache 7
```

### Advanced (Month 1)

```bash
# 1. Interactive workflow
phonebookloca
PhoneBook> osint +number
PhoneBook> cache
PhoneBook> clear-cache 14

# 2. Automated pipelines
phonebookloca --scan data.txt -o extracted.txt
phonebookloca -b extracted.txt --reputation -o intel.csv -f csv

# 3. Performance tuning
phonebookloca --cache-stats  # Monitor efficiency
```

---

## ⚡ Speed Comparison

| Operation | Time (v1.1) | Time (v2.0 Cache) | Improvement |
|-----------|-------------|-------------------|-------------|
| Single lookup | 5-10s | <1s | 10x faster |
| 10 lookups | 50-100s | 5-10s | 10x faster |
| 100 lookups | 8-16min | 1-2min | 8x faster |
| Reputation check | 10-15s | <1s (cached) | 15x faster |

---

## 🔒 Privacy & Security

### What's Stored?

```
~/.phonebookloca/intel.db contains:
├─ Lookup history (numbers you've checked)
├─ Cached intelligence data
├─ Reputation scores
├─ Timestamps
└─ Source attribution
```

### Protection

```bash
# Regular cleanup (weekly)
phonebookloca --clear-cache 7

# Full cleanup (sensitive work)
phonebookloca --clear-cache 0  # Clears everything

# Nuclear option (start fresh)
rm ~/.phonebookloca/intel.db
rm ~/.phonebookloca_config.json
```

### Best Practices

1. **Clear cache after sensitive investigations**
2. **Use `--no-cache` for critical targets**
3. **Protect your intel.db file** (contains lookup history)
4. **Don't share your database** (privacy risk)
5. **Regular maintenance** (weekly `--clear-cache`)

---

<div align="center">

**📱 PhoneBookLOCA v2.0 Quick Reference**

*Professional OSINT Intelligence Platform*

Original: **DezTheJackal** | v2.0: **0xb0rn3 | 0xb0rn3**

For full documentation, see README.md

</div>
