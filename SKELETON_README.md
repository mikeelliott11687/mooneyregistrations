# Keeping iOS fixes when refreshing FAA data

`UPDATE_MAP.py` reads **`map_skeleton.html`** and only replaces:

- `__B64__` — compressed Mooney registry rows  
- `__LEGEND__` — model colors / counts  
- `__DATA_DATE__` — date string  
- `__CITY_COUNT__` — splash “N aircraft” number  

Then it writes `index.html`.

**Do not** regenerate HTML/CSS/JS by hand or swap in an old skeleton — that would wipe the iPhone filter panel and bottom blank-band fixes.

Folder for local runs usually looks like:

```
MooneyMap/
  UPDATE_MAP.py
  map_skeleton.html   ← keep this fixed shell
  ReleasableAircraft.zip
  index.html          ← output (upload to GitHub)
```
