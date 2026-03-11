# BNS Obsidian Pitaya Theme

A reading-optimized dark theme for [Obsidian](https://obsidian.md/), inspired by the [Pitaya Smoothie](https://github.com/trallard/pitaya_smoothie) VS Code theme by Tanya Allard.

## Philosophy

A warm, personal, dark writing environment that carries a trace of Pitaya's spirit. The Pitaya heritage lives on in the code blocks and the warm heading/accent palette, but the ground is a quiet, neutral reading surface.

## Design

- **Background**: Cool near-black with ~15% saturation for depth without blue-light fatigue
- **Text**: Neutral `#DCDCDC` body text so warm accents stand out
- **Headings**: Warm peach-gold to dusty-rose gradient (Geist Sans)
- **Accents**: Warm amber links, muted sage external links, gold bold, mauve italic
- **Code**: Original Pitaya Smoothie syntax colors preserved
- **Tables**: Tufte-inspired minimal — no borders except a faint header rule
- **Callouts**: Four color families (slate, sage, amber, red) instead of twelve
- **Graph**: Warm amber constellation — nodes glow on a dark canvas

## Fonts

The theme references these font families (install separately):

- **Body**: [Plus Jakarta Sans](https://fonts.google.com/specimen/Plus+Jakarta+Sans)
- **Headings**: [Geist Sans](https://vercel.com/font)
- **Interface**: [Satoshi](https://www.fontshare.com/fonts/satoshi)
- **Code**: [IBM Plex Mono](https://fonts.google.com/specimen/IBM+Plex+Mono)

Falls back to system fonts if not installed.

## Installation

1. Open Obsidian Settings > Appearance
2. Under "Themes", click "Manage"
3. Search for "BNS Obsidian Pitaya" (once published)

Or manually: copy `theme.css` to your vault's `.obsidian/themes/BNS Obsidian Pitaya Theme/` directory and create a `manifest.json` there.

## Accessibility

Text contrast meets or exceeds **WCAG 2.1 AA** across all primary reading surfaces:

| Element | Ratio | Level |
|---|---|---|
| Body text (`#DCDCDC` on `#121318`) | 13.53:1 | AAA |
| Accent / links (`#D4A574`) | 8.33:1 | AAA |
| Bold (`#E0BA78`) | 10.13:1 | AAA |
| Italic (`#B898A5`) | 7.13:1 | AAA |
| External links (`#8BAA90`) | 7.29:1 | AAA |
| Muted text (`#908D9E`) | 5.73:1 | AA |
| Error text (`#D47676`) | 5.88:1 | AA |
| Headings (H1–H6) | 6.12–12.79:1 | AAA |
| Code syntax (all tokens) | 5.61–19.37:1 | AA–AAA |

**Known limitations**: Some decorative UI elements (borders, scrollbar tracks, graph lines) use intentionally subtle contrast below the 3:1 SC 1.4.11 threshold, following Tufte-inspired minimal chrome principles. This is a deliberate trade-off favoring a distraction-free reading surface over strict non-text contrast conformance.

Design informed by WCAG 2.1 text contrast guidelines, APCA perceptual contrast research, and Material Design dark theme recommendations.

## Credits

- [Pitaya Smoothie](https://github.com/trallard/pitaya_smoothie) by Tanya Allard — original color palette inspiration
- Design informed by perspectives from Edward Tufte, Giorgia Lupi, Nadieh Bremer, and accessibility research
