# property-owner-finder
Productivity
# Property Owner Finder — Chrome Extension

A skip-tracing tool for commercial real estate cold outreach. Built around the workflow of: pull tax card → identify owner → find phone number → make the call.

## What it does

**Stage 1 — Owner info.** Click the extension on a tax card page and it auto-extracts the owner name, mailing address, and property address. Has special parsing for Florida Sunbiz pages (pulls the principal/manager when you're on an LLC detail page). If auto-extract can't find the fields, you can either select the text on the page first and click extract again, or just type the info in.

**LLC detection.** When the owner is a business entity (LLC, INC, Holdings, etc.), the extension flags it and tells you to start with Sunbiz first. Sunbiz reveals the human principal — then you skip-trace that person.

**Stage 2 — Search.** Eight skip-trace sources, one click each:
- **Sunbiz** (Florida Division of Corporations — finds the manager/registered agent of an LLC)
- **Google** (smart query construction — different for entities vs. people)
- **TruePeopleSearch**
- **FastPeopleSearch**
- **ThatsThem**
- **Whitepages**
- **LinkedIn**
- **Facebook**

Or hit "Open all sources" and it launches the full set in background tabs.

**Stage 3 — Phone numbers.** On any page (Sunbiz, a search result, a company website, a LinkedIn profile, anywhere), click "Scan this page for phones" and the extension extracts every phone number from the page and prints them in the popup. Each number has a one-click copy button. It deduplicates, prioritizes `tel:` links, filters obvious junk (555-01XX, all-same-digit numbers).

**Captured pad.** A persistent textarea below the phone list. Numbers you copy get appended automatically. You can also paste/type freely. "Format" cleans up phone formatting. "Copy all" dumps everything to clipboard.

**History.** Last 30 owners you searched, with timestamp and source count. Click any entry to reload it.

## How to install

1. Unzip `property-finder.zip` somewhere stable (e.g. a Documents folder — don't put it on the Desktop, you don't want to accidentally delete it).
2. Open Chrome and go to `chrome://extensions/`
3. Toggle "Developer mode" on (top right corner)
4. Click "Load unpacked" (top left)
5. Select the unzipped `property-finder` folder
6. The crosshair icon should appear in your toolbar. If it doesn't, click the puzzle piece icon → pin Property Owner Finder

That's it. No account, no API key, no per-lookup fees. Personal/private — nothing leaves your browser except the search URLs you intentionally launch.

## Typical workflow

1. Open a county property appraiser site (Hillsborough HCPAFL, Pinellas PCPAO, Pasco PASCOPA, etc.). Pull up the tax card for a target property.
2. Click the crosshair icon → "Auto-extract from this page". Owner name and address fill in.
3. If owner is an LLC: click **Sunbiz** button. Sunbiz opens in a new tab.
4. On the Sunbiz entity detail page, click the extension again → "Auto-extract" pulls the principal officer's name.
5. Click "Open all sources" — six skip-trace tabs open with searches pre-filled for the principal.
6. On each result tab, click "Scan this page for phones". Phone numbers print in the popup with copy buttons.
7. Click copy on any number — it goes to clipboard AND gets logged in the captured pad.
8. When done, "Copy all" dumps everything to the call log.

## Tips

- If auto-extract misses, try selecting the owner name on the page with your mouse first, then click "Auto-extract from this page" — selection mode kicks in as a fallback.
- The captured pad and inputs persist between popup opens. Closing the popup doesn't lose work.
- Phone scan works on any page — useful on company websites, LinkedIn profiles, Google snippets, etc.
- TruePeopleSearch sometimes throws CAPTCHAs at first visit — solve once and they typically don't reappear for a while.
- "Open all" opens tabs in the background so it doesn't disrupt your flow. Cycle through them with Ctrl+Tab / Cmd+Option+→.

## Files

```
property-finder/
├── manifest.json      ← Chrome extension config
├── popup.html         ← UI markup
├── popup.css          ← styling
├── popup.js           ← all the smarts
├── icons/             ← toolbar icons
└── README.md          ← this file
```

To modify or extend it (add a new search source, tweak the parser for a specific county's tax card layout, etc.), edit `popup.js` and `popup.html`, then click the refresh icon on the extension card in `chrome://extensions/`.

## Version

v1.0.0
