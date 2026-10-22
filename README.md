# ORBIT · Starfield Character Progression Planner

**A mobile-friendly progression planner and conversational character advisor for Bethesda's *Starfield*.** Track purchased skills, queue upcoming ranks, diagnose locked upgrades, and ask the Advisor about your actual character.

**[🚀 Launch ORBIT](https://jlhiskey.github.io/starfield-orbit/)** · [✦ Advisor and AI setup](docs/AI_SETUP.md) · [Full user guide](docs/USER_GUIDE.md) · [Changelog](CHANGELOG.md)

> **Hosting note:** The URL above is the GitHub Pages address for this project. If it shows a 404, publishing may not yet be enabled. Follow the [GitHub Pages setup](#publish-with-github-pages) below. The app's source code is in `index.html`.

## What's new in v1.2

- **✦ Advisor tab:** chat interface that automatically reads the character's recorded level, purchases, available points, roadmap, and active challenges.
- **Local guide:** instant, private, rule-based build advice with no API or setup required. It isn't a language model.
- **Optional AI chat:** use a private Cloudflare Worker and OpenAI Responses API for genuine conversational answers; credentials remain on the server. [Setup guide](docs/AI_SETUP.md).
- **ChatGPT handoff:** copy character context and your last question to paste into ChatGPT without an API connection.
- Existing character save key remains `orbit-starfield-v1`, so the upgrade does not reset your build.

## Features

- **82 skills across five categories:** Physical, Social, Combat, Science, and Tech, with four ranks each.
- **Character dashboard:** current level, available skill points, next upgrades, category progress, and milestones.
- **Editable progression roadmap:** queue future ranks, move steps up or down, remove steps, or select a starter plan.
- **Four roadmap presets:** Bounty Hunter Captain, Ship Specialist, Ground Combat, and Social Explorer.
- **Skill prerequisites:** checks available points, previous-rank challenges, and category tier gates (4 / 8 / 12 invested ranks).
- **Learn-button explanations:** locked buttons can be tapped to show the missing requirement; rank challenges can be checked directly on the roadmap.
- **Saved progress and backups:** automatically saves in this browser, with JSON export/import for backup or transferring devices.
- **No build tools or accounts required:** a single HTML file containing the interface and logic.

> ORBIT is a **manual companion planner**, not an in-game mod or save editor. Level, skill purchases, and completed challenges must be recorded by you.

## Quick start

1. **[Open ORBIT](https://jlhiskey.github.io/starfield-orbit/)** in a browser. If Pages is not enabled, you can [open `index.html` from this repository](index.html) as a local file instead.
2. In **Character**, set your character's name, level, and traits. The current build is tailored to a **Bounty Hunter** background, with **Wanted / Taskmaster / Kid Stuff** as the default traits.
3. Use the **+** level button on **Overview** when you level up in Starfield.
4. In **Roadmap**, review the recommended queue or choose another preset and select **Load preset**. Rearrange steps with the arrow buttons.
5. When you've met a skill's requirements in Starfield, check **Mark challenge complete** when applicable, then select **Learn**. This records the purchased rank in ORBIT.
6. Under **Character → Export save**, download a JSON backup, especially before switching browsers, devices, or URLs.

The Bounty Hunter starts with **Piloting 1**, **Targeting Control Systems 1**, and **Boost Pack Training 1**. These starting ranks don't spend your level-up points.

See the **[step-by-step user guide](docs/USER_GUIDE.md)** for details and troubleshooting.

## Tabs

| Tab | What it does |
| --- | --- |
| **Overview** | Level and skill-point totals, next planned ranks, milestones, category investment |
| **Roadmap** | Presets, reorder/remove future ranks, mark challenges complete, learn available ranks, copy plan as text |
| **Skill library** | Search and filter all skills by category/tier, mark challenges, queue a rank, learn or undo a rank |
| **Character** | Edit your character name, level, and traits; save notes; export/import JSON; reset the planner |
| **Advisor** | Ask about your build, points, challenges, and next skills; optionally connect a private AI gateway |

## How progression works

- **Available points** = character level − 1 − purchased skill ranks **excluding the three free Bounty Hunter ranks**.
- **Skill tiers** require a total of **0, 4, 8, or 12 ranks** already invested in that category for tiers 1–4.
- **Rank 1** needs an available point and its category tier unlocked.
- **Ranks 2–4** also require the *previous rank's in-game challenge* to be completed and checked off.
- **Roadmap steps are plans, not purchases.** Reordering the roadmap does not allocate points; select **Learn** when you actually purchase a skill in the game.
- Level predictions assume one point per level; actual timing may differ because of challenges and tier gates.

For many skills the planner shows a generic challenge reminder; **use Starfield's in-game challenge text as the source of truth**.

## Saves and privacy

ORBIT stores the current character in your browser's **localStorage** (`orbit-starfield-v1`). Advisor history has a separate browser-local key; it is not part of the character JSON export. It does **not** sync saves to GitHub, Bethesda, or other devices. An optional AI request sends your character snapshot and recent conversation to a private gateway and OpenAI, as described in [AI setup](docs/AI_SETUP.md).

- Same browser and same website URL: progress normally persists across visits.
- Different browser, different device, or local file → hosted website: **export JSON from the old app and import it on the new one**.
- **Import save** replaces the current planner data after confirmation, so export a backup first.
- Avoid clearing site data or using private browsing for your only save.

Version 1 exports can be imported into v1.1.

## Publish with GitHub Pages

The site is intended to be hosted at **https://jlhiskey.github.io/starfield-orbit/**.

1. Open **[Settings → Pages](https://github.com/jlhiskey/starfield-orbit/settings/pages)**.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Set branch to **`main`**, folder to **`/(root)`**, then **Save**.
4. Once GitHub finishes the deployment, open the [site URL](https://jlhiskey.github.io/starfield-orbit/).

The site entry point is the root-level `index.html`; no dependency installation or build command is needed. [GitHub Pages documentation](https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site)

## Development

Clone this repository, then open `index.html` locally in your browser. The planner core lives in `index.html`; the Advisor UI lives in `advisor.js` and `advisor.css`. The optional backend template is under `worker/`.

```bash
git clone https://github.com/jlhiskey/starfield-orbit.git
cd starfield-orbit
# Open index.html in your preferred browser
```

When updating the app, preserve the existing localStorage key or supply an explicit migration so players don't lose progress.

## Troubleshooting

**Learn shows locked even after leveling up:** Tap it to see why. You may need a completed rank challenge, enough points in the skill category to unlock its tier, or an earlier rank first. Completing a challenge in Starfield does not automatically check the box in ORBIT.

**A queued skill shows a tier warning:** Reorder your Roadmap so lower-tier purchases meet the category's point threshold first.

**My save is missing on my phone / new URL:** Saves are browser-local. Import the JSON exported from the other device or browser.

**The page link shows 404:** Check the [Pages settings](https://github.com/jlhiskey/starfield-orbit/settings/pages) and make sure deployment is set to `main` and `/(root)`.

**I just updated the app but still see the old one:** Reload the page; if it persists, try a forced refresh. Export your save before clearing browser site data.

## Project status

**v1.2** · Added Advisor chat with local guidance, optional server-backed AI, and ChatGPT context handoff. See the [changelog](CHANGELOG.md).

This is an unofficial fan-made planning tool and is not affiliated with or endorsed by Bethesda or Microsoft.
