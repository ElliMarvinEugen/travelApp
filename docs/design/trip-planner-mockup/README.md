# Trip planner UI mockup

A clickable, single-file HTML mockup of the main planning screen. It is a design reference for discussion, not production code. Nothing here decides the tech stack (see `docs/TOOLS.md`).

## Open it
Open `index.html` in a browser. It needs an internet connection for two things: the Inter and Plus Jakarta Sans fonts from Google Fonts, and the icon library Lucide (pinned to 0.469.0, loaded from unpkg).

## Map image
The mockup expects a screenshot named `map.webp` next to `index.html` (central Ho Chi Minh City, north up). The original was a Google Maps screenshot and is **not committed**, because Google's terms do not allow reusing its imagery. Without the file the pins and route still show on a plain background. Replace it with an image we may use before sharing the mockup outside the team.

## What the mockup shows
- Header with menu points and an account menu.
- Sidebar with days grouped by city (Ho Chi Minh City, Da Nang). Each day has an AI-suggested title that can be renamed.
- Place cards with start time, short description, opening hours, entry cost, reservation notes and an example picture.
- Warnings when a place is closed on the planned day or time.
- Transport between places: the best mode is chosen automatically (AI badge), can be overridden, and the travel time can be edited. Tickets can be attached.
- Drag and drop to reorder places or move them to another day in the same city.
- Map card that zooms to a selected place, and AI recommendations (cards or list) that can be added to the day.

## Sample data
All places, opening hours, prices and descriptions are invented examples. Do not rely on them for real planning.
