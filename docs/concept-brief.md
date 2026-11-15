# ✈️ Travel Planner: Concept Brief

> **One shared place where a group plans a trip together, from first idea to the last day of the journey.**

| | |
|---|---|
| **Status** | Draft for the brainstorming session (ELL-32) |
| **Drafted by** | Claude, for Elli, Marvin and Eugen |
| **How to use this** | Read sections 1 to 4 (5 minutes), then go straight to **section 7, the decision board**. Fill in the "Decision" column during the session. |
| **Scope** | Product concept only. No tech stack or paid service is assumed; those are decided separately through ADRs (`docs/TOOLS.md`). |

Linear is the source of truth for vision and MVP scope. This brief turns it into concrete ideas we can decide on.

---

## 1. Who it is for

| 💑 Couples | 👯 Groups of friends | 🗺️ Complex trips |
|---|---|---|
| Planning a vacation together | One person usually does all the organizing | Several cities, transport legs and places to stay |

What they share: more than one person has opinions, and the plan must stay clear while it changes.

## 2. The problem

A group trip today is scattered across a spreadsheet, a chat thread, booking screenshots, map bookmarks and AI prompts that forget everything.

| Pain | Our answer |
|------|------------|
| The plan is scattered | One shared trip with everything in it |
| Only the organizer sees the whole picture | Everyone sees the same day-by-day plan |
| Edits clash, copies get outdated | Shared editing, one source of truth |
| Multi-city routes are hard to picture | Map with the full route |
| Shared money is awkward | Budget and expenses per trip |
| AI forgets the trip | Optional AI that works with the trip's data (later) |

## 3. How friends plan together

1. **Create:** one traveler creates a trip and is its **Owner**.
2. **Invite:** friends join by invitation as **Editor** (can change the plan) or **Viewer** (can follow along).
3. **Plan:** everyone adds ideas and activities to specific days. Changes show up for all.
4. **Organize:** map, bookings and costs sit next to the days they belong to.
5. **Travel:** everyone opens the same plan to see what is next.

🔒 A trip is private by default. Only invited people can see or edit it.

## 4. Worked example: "Iberia 2027"

Mia plans 10 days with her friends Tom and Jin: Barcelona (3 nights), Madrid (3), Lisbon (4).

| Step | What happens |
|------|--------------|
| 1. Create the trip | Mia sets the dates, adds the three cities in order and a rough budget. The dashboard shows a cover image and the route. |
| 2. Invite friends | Mia sends an invitation to Tom and Jin as Editors. |
| 3. Collect ideas | Tom adds "Sagrada Familia" with a note and cost estimate. Jin adds a Lisbon restaurant. |
| 4. Build the itinerary | Mia drags Sagrada Familia into the morning of day 2 and a tapas tour into the evening. The map shows pins and distances. |
| 5. Edit together | Tom moves the tapas tour to day 3 while Jin edits that day's notes. Both changes are visible to everyone. |
| 6. Add bookings | Mia stores the Barcelona to Madrid train (time, reference, status "booked") and the Lisbon hotel ("to book"). |
| 7. Track costs | The group compares planned costs with the budget. |
| 8. Optional AI (later) | Mia asks for a relaxed Madrid afternoon within budget and accepts, edits or ignores the suggestions. |

## 5. Feature proposals

| Feature | What it helps travelers do | Suggested phase |
|---------|---------------------------|:---------------:|
| Accounts and profiles | Own their trips and edits | 🟢 v1 |
| Invitations and roles (Owner, Editor, Viewer) | Bring friends in and control who may change the plan | 🟢 v1 |
| Trip management (create, edit, archive, delete) | Set up a trip and keep several trips apart | 🟢 v1 |
| Multi-city trips | Organize several destinations and their order | 🟢 v1 |
| Day-by-day itinerary with activities, notes, costs | See exactly what happens each day | 🟢 v1 |
| Drag-and-drop scheduling | Rearrange the plan without retyping | 🟢 v1 |
| Shared editing | Plan together without outdated copies | 🟢 v1 (live updates: see decision D1) |
| Interactive map with route | Understand where things are and how far apart | 🟢 v1 |
| Bookings (flights, hotels, trains, activities) | Keep every reservation next to its day | 🟢 v1, simple |
| Budget and expenses | Know whether the trip fits the budget | 🟢 v1, basic |
| Cost splitting | Settle shared costs fairly | 🟡 later (see D4) |
| AI itinerary suggestions and recommendations | Get a starting plan and ideas | 🔵 later |
| Route and travel-time optimization | Avoid days with too much travel | 🔵 later |
| Comments and voting on ideas | Decide on activities as a group | 🟡 later, discuss |
| Offline access | Use the plan without a connection | 🟡 later, discuss |
| Import of booking emails | Avoid typing bookings by hand | 🟡 later, discuss |

Legend: 🟢 first version · 🟡 later, may move up · 🔵 later, after the core is stable. The app must stay fully usable without AI.

## 6. Suggested first version

**Done when a group can complete steps 1 to 7 of the example without AI.**

- In: accounts, invitations with roles, multi-city trips, day-by-day itinerary with drag and drop, shared editing, map with route, simple bookings, basic budget.
- Out: cost splitting, all AI features, comments and voting, offline access, email import.

## 7. Decision board

Use this during the session. **Recommendation** is Claude's suggestion, not a decision. Write the outcome in **Decision** and tick the box when it is settled.

| # | Question | Recommendation | Owner | Decision | Done |
|---|----------|----------------|-------|----------|:----:|
| D1 | Is live co-editing required in v1, or is "refresh to see changes" enough? | Start with refresh. Add live updates when the core works. It is the biggest effort and cost driver. | Eugen, Elli | | ☐ |
| D2 | Who may invite others: Owner only or any Editor? | Owner only. Simpler and more private. | Elli, Marvin | | ☐ |
| D3 | Can a friend join without creating an account? | No. Require an account so access stays limited to known users. | Elli, Marvin | | ☐ |
| D4 | Is cost splitting part of v1? | No. Track costs first, split later. | Elli | | ☐ |
| D5 | Bookings: free-form notes or structured fields per type? | Structured basics (type, date, reference, status) plus a notes field. | Elli | | ☐ |
| D6 | Which languages and currencies must v1 support? | English and one trip currency per trip. | Elli | | ☐ |
| D7 | Mobile: responsive web only? | Yes, responsive web only. Travelers will use phones, so design mobile first. | Elli, Eugen | | ☐ |
| D8 | What happens to a trip when its owner deletes their account? | Transfer ownership to an Editor, otherwise delete after a warning. | Marvin, Elli | | ☐ |
| D9 | How should AI be limited and paid for, given cost concerns? | Defer. Decide after v1, with real usage and price data. | Eugen, Elli | | ☐ |

## 8. After the brainstorming session

Fill in together after the session.

| Explore in Figma | Set aside | Still open |
|------------------|-----------|------------|
| | | |

Next step: the revised brief is the input for ELL-34 (Figma prototype) and ELL-36 (tech stack verification).
