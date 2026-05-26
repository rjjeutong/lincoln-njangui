# Meeting Group Portal

A static web app for tracking a rotating savings group (tontine / meeting) with 14 bi-weekly meetings. Members can view their individual payout schedule; the organizer can track completion.

**No backend. No login. No build step.** Pure HTML, CSS, and vanilla JavaScript.

---

## Pages

| Page | URL | Purpose |
|---|---|---|
| Home | `index.html` | Member picker, progress bar, next meeting banner |
| Member | `member.html?id=robby` | Individual payout dates + countdown |
| Organizer | `admin.html` | Full schedule, mark complete, print view |

---

## Deploy to GitHub Pages

1. Create a new public GitHub repository (e.g. `meeting-portal`)
2. Push all files to the `main` (or `master`) branch
3. Go to **Settings → Pages**
4. Under **Source**, select `Deploy from a branch`
5. Choose branch: `main` (or `master`), folder: `/ (root)`
6. Click **Save** — your site will be live at `https://YOUR-USERNAME.github.io/meeting-portal/`

That's it. No npm, no build tools required.

---

## Update meeting data for future rounds

Open `assets/data.js` and edit the `MEETING_DATA` object:

- Change `startDate` to the first meeting date of the new round
- Update each entry in the `meetings` array with new dates and winner slot assignments
- Update `totalMeetings` if the round has a different number of meetings

---

## Add or remove members

Open `assets/data.js` and edit the `MEMBERS` array:

**To add a member:**
```js
{ id: "firstname", name: "First Name", slots: ["First Name I", "First Name II"] },
```
- `id` — URL-safe lowercase string (used in `member.html?id=...`)
- `name` — display name
- `slots` — list of slot names exactly as they appear in `meetings[].winners`

**To remove a member:** delete their entry from the `MEMBERS` array.

> After changing members, also update the `meetings[].winners` arrays so slot names match.

---

## Completion state

The organizer page stores completion marks in `localStorage` under the key `meeting_completions` (an array of meeting numbers). This is per-browser — it is not shared across devices.

Meetings whose date has already passed are automatically shown as completed everywhere.

---

## File structure

```
meeting-portal/
├── index.html        # Home — member picker
├── member.html       # Individual member view (uses ?id= param)
├── admin.html        # Organizer view
├── assets/
│   ├── style.css     # Global dark-gold styles
│   └── data.js       # All meeting + member data (edit this each round)
└── README.md
```
