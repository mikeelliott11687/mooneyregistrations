# iOS bottom blank / dead-space fix

## Cause
On iPhone (standalone GitHub Pages and Google Sites iframe embeds), a full-bleed layout that leans on **device** viewport units (`100vh` / `100dvh`) or `min-height: 100vh` sizes the page to the phone screen, not the browsing context. That overshoots the visible area / iframe and leaves a **phantom empty band at the bottom**. Extra `env(safe-area-inset-*)` padding on `html`/`body` makes the same strip worse. Leaflet also needs a resize pass when the iOS URL bar or `visualViewport` changes, or the map pane stops short of the real bottom.

## Fix
- Pin `body { position: fixed; inset: 0 }` with `height/max-height: 100%` — fills **this frame** (window or Sites iframe) without `vh`.
- Do **not** put safe-area padding on `html`/`body`.
- Map + `.leaflet-container` fill `#map-wrap` (`inset: 0`, matching dark background).
- Legend max-height uses `%` of `#map-wrap`; filter drawer uses `55dvh` capped at 420px.
- `syncMapSize()` → `map.invalidateSize()` on `resize`, `orientationchange`, and `visualViewport` resize/scroll.
- `viewport-fit=cover` on the viewport meta.

## Untouched
- Marker data, geocode path, filter/legend UX from prior iOS filter fix.
