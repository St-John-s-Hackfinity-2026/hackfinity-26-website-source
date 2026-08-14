# Published Mobile Timeline Verification

Source capture: GitHub Pages release `d80d3ee` at a 375px viewport on 14 August 2026.

| Tiles inspected | Verified observation |
| --- | --- |
| 1–2 | The published mobile site renders the header, hero, countdown, live squad counter, and the beginning of the mission content at the intended narrow width. The capture is segmented with ordered vertical overlap; timeline cards are inspected in the subsequent tiles. |
| 3–4 | The mission panels and the lead-in to the timeline render without horizontal clipping at the published 375px mobile width. |
| 5–6 | The active 01 card displays the intended complete red/yellow fill and a fully visible yellow outlined numeral. The following 02, 03, and 04 numerals are fully visible at the card edge without the partial-glyph clipping reported in the original screenshots. |
| 7–8 | The 05 numeral is also fully visible at the right edge of the final timeline card. Its full 0 and 5 outlines remain within the mobile card; no cyan activation treatment is visible in the published capture. |
| 9 | The lower-page content completes normally, confirming no layout break occurred after the timeline. The 9-tile review used a 375 × 5000px published capture with ordered 50px vertical overlap. |

## Result

The published 375px mobile review directly verifies the requested repair: the active timeline fill uses St. John’s red/yellow/white rather than cyan, and the 01–05 stage numerals render fully inside their cards. The desktop active state was separately checked in the browser, and the style contract is covered by automated tests.
