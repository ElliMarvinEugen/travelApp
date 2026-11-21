# Trip planner UI mockup

Clickable, single-file HTML mockups of the main planning screen, for desktop and for phones. They are design references for discussion, not production code. Nothing here decides the tech stack (see `docs/TOOLS.md`).

| File | What it is |
|------|------------|
| `index.html` | Desktop version |
| `mobile.html` | Phone version. On a desktop browser it is shown inside a phone frame, on a phone it fills the screen. |

## Open it
Open `index.html` or `mobile.html` in a browser. They need an internet connection for two things: the Inter and Plus Jakarta Sans fonts from Google Fonts, and the icon library Lucide (pinned to 0.469.0, loaded from unpkg).

## Map image
Both mockups expect a screenshot named `map.webp` next to them (central Ho Chi Minh City, north up). The original was a Google Maps screenshot and is **not committed**, because Google's terms do not allow reusing its imagery. Without the file the pins and route still show on a plain background. Replace it with an image we may use before sharing the mockups outside the team.

## Desktop version shows
- Header with menu points and an account menu.
- Sidebar with days grouped by city (Ho Chi Minh City, Da Nang). Each day has an AI-suggested title that can be renamed.
- Place cards with start time, short description, opening hours, entry cost, reservation notes and an example picture.
- Warnings when a place is closed on the planned day or time.
- Transport between places: the best mode is chosen automatically (AI badge), can be overridden, and the travel time can be edited. Tickets can be attached.
- Drag and drop to reorder places or move them to another day in the same city.
- Map card that zooms to a selected place, and AI recommendations (cards or list) that can be added to the day.

## Phone version shows
- Top bar with the trip name, invite and notifications. Bottom bar with My trips, Discover, Bookings, Inspiration and Profile (account settings).
- Day cards grouped by city, each with its AI-suggested title.
- Map card on top and a pull-up list below. The list grows as you scroll down, and the map comes back with the Map button, the handle, or by pulling down at the top.
- Same place cards, warnings, AI-chosen transport and AI recommendations as on desktop, with bottom sheets instead of popovers.
- "Reorder" mode with arrows and "Move to another day" instead of drag and drop.
- A plus button opens the sheet to add a place.

## Sample data
All places, opening hours, prices and descriptions are invented examples. Do not rely on them for real planning.
