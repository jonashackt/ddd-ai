# SIXT.de Style Extraction

Quelle: https://www.sixt.de/  
Screenshot: `sixt-style/sixt_de.png` (1440×900, Scale 1×)  
JSON: `sixt-style/sixt_style.json`  
Erstellt: 2026-10-02 mit `/webapp-style-extractor`

---

## Farbpalette

| Rolle | Hex | Verwendung |
|-------|-----|-----------|
| **Primary Orange** | `#FF5000` | CTA-Buttons (EINVERSTANDEN), Logo-Akzent |
| **Dark Burnt Orange** | `#5E2A12` | Announcement Bar, dunkle Widget-Overlays |
| **Near Black** | `#141414` | Navbar-Hintergrund |
| **Dark Surface** | `#191919` | Sub-Navigation, aktive Tabs |
| **Body Text** | `#222222` | Fließtext in hellen Bereichen (Modal) |
| **Muted** | `#5E5E5E` | Nav-Labels, Input-Hintergrund (dark), Icons |
| **White** | `#FFFFFF` | Modal-Hintergrund, Button-Text, helle Bereiche |
| **Warm Tint** | `#FEF2EB` | Booking-Widget-Hintergrund, Info-Bereiche |

---

## Typografie

Schriftfamilie: **Custom Sans-Serif** (visuell: geometrisch/humanistisch) — wahrscheinlich „SIXT Sans". Exakter Name muss per CSS verifiziert werden.

| Stil | Größe | Gewicht | Farbe | Einsatz |
|------|-------|---------|-------|---------|
| Modal Heading | 20px | 700 | `#222222` | Modale Überschriften |
| Button Label | 14px | 700 | `#FFFFFF` / `#FF5000` | Beschriftung aller Buttons |
| Body / Modal Text | 14px | 400 | `#222222` | Fließtext |
| Nav Label | 14px | 400 | `#5E5E5E` | Navigation |
| Announcement Bar | 14px | 700 | `#FFFFFF` | Top-Banner |
| Label Small | 12px | 400 | `#5E5E5E` | Kleinbeschriftungen |

---

## Spacing

Basis-Einheit: **8px**

Skala: `4 · 8 · 12 · 16 · 24 · 32 · 40 · 48 · 64`

| Element | Wert |
|---------|------|
| Announcement Bar Höhe | 37px |
| Navbar Höhe | 64px |
| Sub-Navigation Höhe | 40px |
| Button Höhe (Primary) | 44px |
| Button Padding horizontal | 24px |
| Modal Padding | 32px |

---

## Komponenten

### Buttons

| Variante | Hintergrund | Text | Border | Radius |
|----------|-------------|------|--------|--------|
| **primary** | `#FF5000` | `#FFFFFF` bold | — | 4px |
| **secondary** | `#FFFFFF` | `#FF5000` bold | `1px solid #FF5000` | 4px |
| **ghost** | transparent | `#FF5000` bold | — | 4px |
| **tab (aktiv)** | `#191919` | `#FFFFFF` medium | `1px solid #353535` | 20px (Pill) |

Alle Buttons: Höhe **44px**, Font 14px/700, Padding 24px horizontal.

### Inputs

| Variante | Hintergrund | Text | Radius |
|----------|-------------|------|--------|
| Search (dark context) | `#5E5E5E` | `#FFFFFF` | 4px |

### Surfaces

| Komponente | Hintergrund | Radius | Besonderheit |
|-----------|-------------|--------|-------------|
| Modal | `#FFFFFF` | 8px | Shadow (CSS messen) |
| Info Bar | `#FEF2EB` | — | `3px solid #FF5000` links |
| Navbar | `#141414` | — | Höhe 64px |
| Announcement Bar | `#5E2A12` | — | Höhe 37px |
| Booking Widget | `#FEF2EB` | 8px | Warm-Tint, 24px Padding |

---

## Caveats & offene Punkte

1. **Font-Familie** nicht aus Pixeln lesbar — aus CSS verifizieren (wahrscheinlich „SIXT Sans").
2. **Schatten** sind nicht aus dem Screenshot messbar — aus DevTools/CSS übernehmen.
3. **Hover/Focus/Disabled-States** im statischen Screenshot nicht sichtbar — nicht enthalten.
4. Der „Autos anzeigen"-Button im Booking Widget erscheint pixelgemessen als `#5E2A12` (dunkles Bildmaterial im Hintergrund scheint durch) — der tatsächliche Brand-Orange ist `#FF5000` laut EINVERSTANDEN-Button.
5. Der Screenshot wurde mit aktivem Cookie-Banner aufgenommen — das überlagert Teile der Seite.
