# iOS / mobile filter UX fix

## What was wrong
- Header was a fixed **52px** bar with `overflow: hidden`, so Model/State/Search controls were clipped or unreadably small on ~390px phones.
- Tap targets were tiny (`padding: 3px 7px`, `font-size: ~0.73em`) — well under Apple’s ~44px guideline.
- No mobile layout: filters competed with the map in one cramped horizontal row.
- Inputs under 16px could trigger Safari auto-zoom on focus.

## What we changed
- Kept **native `<select>`** for Model and State (iOS native picker).
- **Collapsible sticky filter panel** on ≤720px: title bar + **Filters** button; panel stacks full-width controls and scrolls inside Safari (`-webkit-overflow-scrolling: touch`).
- Tap targets ≥**44px**; mobile inputs/selects at **16px** font-size.
- Flex layout (`#map-wrap`) so the header can grow without covering the map; `map.invalidateSize()` on filter toggle.
- Legend list rows enlarged and scroll-friendly on small screens.
- Desktop (≥721px) keeps an always-visible horizontal control row.

## Untouched
- Leaflet map init, marker rendering, FAA embedded data / decode path.

Live: https://mikeelliott11687.github.io/mooneyregistrations/
