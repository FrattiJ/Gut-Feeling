# Gut Feeling

A privacy-first IBS food and symptom tracker. Log meals in under a minute, track symptoms over time, and surface patterns between what you eat and how you feel.

Built as a single HTML file hosted on GitHub Pages with a Supabase backend — no server, no app to install, works on any device.

**Live:** https://frattij.github.io/Gut-Feeling/

---

## What it does

Most IBS tracking apps are either too clinical or too vague. Gut Feeling is designed around one core insight: **you need to log fast at the time you eat, and update symptoms separately when they hit** — because bloating and cramping often show up an hour or two after the meal, not during.

Each user's data is completely private. Login is required, and Supabase Row Level Security ensures no one can see anyone else's logs.

---

## Features

- **4-step meal logging** — designed to take under 60 seconds
- **Today's feed** — see everything you've eaten today at a glance on the home screen
- **Delayed symptom logging** — tap `+Sx` on any meal in today's feed to add or update symptoms after the fact, without opening a full edit screen
- **IBS trigger tagging** — organized by category: Dairy, Gluten/Grains, High-FODMAP, Fat/Spice/Other
- **History tab** — searchable, filterable log of every meal with severity color-coding
- **Insights tab** — trigger–symptom correlation analysis that shows you which foods appear most often alongside a given symptom, with percentage scores and "Strong signal" flags at 60%+
- **Edit / delete** — update full meal details from the History tab
- **Multi-user** — friends and family can create their own accounts; data is isolated per user
- **Mobile-friendly** — designed for one-handed iPhone use

---

## How to use it

### Logging a meal

1. Open the **Log** tab (home screen)
2. Tap the meal name field and type what you ate — e.g. "Cheeseburger & Fries"
3. Set the date and time (defaults to right now)
4. Pick a meal type and source (Homemade / Restaurant / Packaged)
5. Tap **Next** → rate your discomfort (0 = none, 10 = severe) and select any symptoms you're experiencing right now
6. Tap **Next** → check off any IBS triggers the meal contained — be generous, it's better to over-tag
7. Tap **Next** → optionally note bowel movement type, stress level, and any free-text notes
8. Tap **Save Log**

The whole flow should take under a minute.

### Logging symptoms after the fact

Symptoms often don't show up until 1–2 hours after eating. Don't re-open the full form — just:

1. Find the meal in **Today's feed** on the home screen
2. Tap the **+Sx** button on the right
3. Update your discomfort rating, symptom chips, and timing
4. Tap **Save changes**

This is the primary way to connect a meal to symptoms that came later.

### Finding patterns

1. Open the **Insights** tab
2. Select a symptom from the dropdown (e.g. "Bloating")
3. Optionally set a minimum discomfort level
4. The app calculates how often each trigger tag appeared in logs where you had that symptom
5. Triggers at 60%+ are flagged as **Strong signal** — meaning that ingredient appeared in the majority of your bad days for that symptom

The more logs you have, the more meaningful the correlations become. Aim for at least 2–3 weeks of consistent logging before drawing conclusions.

### Editing a past meal

1. Go to the **History** tab
2. Find the meal and tap **Edit** on the right side of the card
3. Update any fields and tap **Save changes**

Tap anywhere else on the card to open a read-only detail view.

---

## Tech

- **Frontend:** Single `index.html` — no framework, no build step, no dependencies beyond two CDN scripts
- **Auth & database:** [Supabase](https://supabase.com) — Postgres with Row Level Security
- **Hosting:** GitHub Pages
- **Fonts:** Playfair Display + DM Sans via Google Fonts
