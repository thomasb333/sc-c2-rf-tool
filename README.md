# SC/C2 — RF Spectrum, Antenna & Site Planning Tool

A single-file, self-contained HTML tool for RF spectrum visualization, radio interoperability analysis, personnel loadout planning, RF link budget calculation, and codeplug channel display.

**No install. No server. No dependencies.** Open `index.html` in any modern browser.

---

## Live Demo

**[▶ Open SC/C2 Tool](https://thomasb333.github.io/sc-c2-rf-tool)**

---

## Features

### RF Spectrum Visualizer
- Log-compressed spectrum view from 1.6 MHz to 6 GHz
- 80+ radios plotted by frequency band
- Hover for full specs, click for programming reference
- Filter by type (CB, HF, VHF/UHF, P25, DMR, Marine, Aviation, GMRS, Mesh, HaLow, Satellite)

### Radio Library
- Filter by **brand**, **band**, or **type**
- Full-text search across name, brand, and notes
- Click any card for detailed spec panel
- Select radios to add to personnel loadouts

### User Loadouts
- Build a personnel roster (stored in browser — never transmitted)
- Assign radios from the library to each operator
- Automatic interoperability matrix for any two operators
- Side-by-side comparison mode

### Site Planner
- Free Space Path Loss (FSPL) calculator
- Point-to-point link budget with margin table
- Auto-loads TX parameters from any radio in the library
- Integrates with [Meshtastic Site Planner](https://site.meshtastic.org) for terrain-corrected coverage maps (ITM/Longley-Rice model)

### Codeplug Parser (In-Browser)
Decode raw codeplug files directly — **no Python, no install required**:

| Extension | Format |
|-----------|--------|
| `.cps` | Motorola CPS XML (XOR 0x95 obfuscated) |
| `.cpglog` | Motorola RSS change log (HT1250 / conventional) |
| `.cpg` | Motorola HT1250 binary (drop with companion `.cpglog`) |
| `.data` | Baofeng DM-32UV binary (IEEE 754 float32, 48-byte records) |
| `.img` | CHIRPnext CSV image |
| `.json` | SC/C2 channel JSON (direct load) |

Outputs channel table, printable field card, and engineer view.

---

## Radio Library Coverage

| Category | Examples |
|----------|---------|
| CB 27 MHz | Cobra 50WX-ST, Cobra 29 LTD, Uniden PRO510XL |
| HF | Barrett 4050, Icom IC-7300, Kenwood TS-890S |
| GMRS/FRS | Motorola MR350R, T800, Midland GXT1050 |
| MURS | Baofeng BF-888S |
| VHF/UHF Portable | Baofeng UV-5R, BF-F8HP, DM-32UV, TYT UV-390, Kenwood TK-260/360 |
| VHF/UHF Mobile | Motorola CDM-1250, M1225, Kenwood TK-7180/8180, Icom F5021 |
| P25 Portable | Motorola APX 6000, XTS2500, Kenwood VP8000/NX-5300, Tait TP9400, Harris XL-200P |
| P25 Mobile | Motorola XTL2500, APX-25 (all bands) |
| DMR | Motorola XPR7550/6550, AnyTone D878UV, TYT MD-380, Retevis H3 |
| Marine | Icom IC-M330, Standard Horizon GX2200, Uniden UM725 |
| Aviation | Icom IC-A25N, Yaesu FTA-750L |
| LoRa Mesh | Meshtastic 433/915/2.4 GHz, RAK WisBlock |
| HaLow | Morse Micro 802.11ah 900 MHz |
| Satellite | Iridium 9575 Extreme, Garmin inReach Mini 2 |

---

## Usage

### Option 1 — Use the hosted version
Click the Live Demo link above. Nothing to install.

### Option 2 — Download and run locally
1. Download `index.html`
2. Open it in Chrome, Firefox, Edge, or Safari
3. Done

### Option 3 — Self-host on GitHub Pages
1. Fork this repository
2. Go to **Settings → Pages → Source → Deploy from branch → main → / (root)**
3. Your tool is live at `https://[your-username].github.io/[repo-name]`

---

## Codeplug JSON Format

The SC/C2 tool uses a simple JSON schema for channel data. If you are generating JSON programmatically or from a custom tool:

```json
{
  "radio": "Radio Model Name",
  "cps_version": "Source tool / version",
  "zone": "Zone or group name",
  "parsed": "YYYY-MM-DD",
  "channels": [
    {
      "num": 1,
      "name": "DISPATCH",
      "band": "VHF",
      "rx": 155.145,
      "tx": 153.845,
      "duplex": "-1.3000 MHz",
      "tone_rx": "123.0",
      "tone_tx": "123.0",
      "power": "High",
      "rx_only": "No",
      "notes": "Primary dispatch"
    }
  ]
}
```

**Field notes:**
- `band` — `"VHF"`, `"UHF"`, `"700"`, or `"800"`
- `duplex` — `"Simplex"`, `"+X.XXXX MHz"`, or `"-X.XXXX MHz"`
- `tone_rx` / `tone_tx` — CTCSS frequency in Hz (e.g. `"127.3"`), DCS code prefixed with `D` (e.g. `"D023"`), or `"None"`
- `rx_only` — `"Yes"` or `"No"`

---

## RF Codeplug Parser (Desktop Tool)

For formats not supported by the in-browser parser (`.rdt`, `.mdf`, and MOTOTRBO `.ctb` with key extraction), a standalone Python-based desktop parser is available:

**RF_Codeplug_Parser** — dark-mode GUI exe for Windows  
Supports: `.cpg/.cpglog` · `.cps` · `.rdt` · `.mdf` · `.img` · `.data`  
Exports: SC/C2 JSON + SC/C2-compatible Excel workbook  

> Source and build instructions available in the companion repo.

---

## Disclaimer

This tool is provided for informational and planning purposes only. Frequency, power, and channel data must be verified against current FCC license authorizations before any operational or on-air use. The author assumes no liability for misconfiguration, unauthorized RF transmissions, or operational decisions made using this tool. All radio specifications are approximate and subject to change by the manufacturer.

---

## License

MIT License — Copyright (c) 2026 BDT / github.com/thomasb333

See [LICENSE](LICENSE) for full text.
