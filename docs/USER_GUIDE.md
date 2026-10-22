# ORBIT User Guide

[← Back to README](../README.md) · [Open the planner](https://jlhiskey.github.io/starfield-orbit/) · [Changelog](../CHANGELOG.md)

ORBIT is a browser-based *Starfield* character progression companion. It helps you plan a build and manually keep track of ranks you've actually purchased. It cannot read or modify Starfield save files.

## 1. Getting started

1. Open **https://jlhiskey.github.io/starfield-orbit/** once GitHub Pages is enabled, or download and open `index.html`.
2. Open **Character** and choose your captain's **name**, **current level**, and up to three **trait labels**. Select **Save profile**.
3. The current version uses a fixed **Bounty Hunter** background. The three free starting ranks are:
   - **Piloting 1**
   - **Targeting Control Systems 1**
   - **Boost Pack Training 1**
4. Check **Overview** to see your current level, available points, planned upgrades, category investment and milestones.
5. Open **Roadmap** to customize the next skills you want to acquire.

### Default character

| Field | Starting value |
| --- | --- |
| Background | Bounty Hunter (currently fixed) |
| Name | The Bounty Hunter |
| Traits | Wanted · Taskmaster · Kid Stuff |
| Level | 1 |
| Starting ranks | Piloting 1, Targeting Control Systems 1, Boost Pack Training 1 |
| Roadmap preset | Bounty Hunter Captain |

The labels for traits are editable, but changing them in ORBIT does **not** change your actual in-game character.

## 2. Record a level-up

On **Overview**, tap **+** beside the level number. The **−** button corrects accidental level increases, but the app will not allow a level below the number of points you've already spent plus one.

You can also set the level on **Character → Current level → Save profile**.

A level-up adds an available skill point in the planner. It does not automatically purchase a skill.

### Skill-point math

```text
Available points = Current character level − 1 − Purchased ranks
```

In that formula, **purchased ranks exclude the three free Bounty Hunter starting ranks**. At level 5 with two manually purchased ranks, ORBIT shows two available points.

## 3. Plan skill upgrades without spending points

Open **Roadmap** to see the sequence of future skill purchases.

- Choose a suggested plan from the **Suggested route** selector and tap **Load preset**.
- The four presets are **Bounty Hunter Captain**, **Ship Specialist**, **Ground Combat**, and **Social Explorer**.
- Use the **↑ / ↓** arrows to reorder planned upgrades.
- Use **×** to remove a planned step.
- Select **+ Add skill** to browse the full library and select **+ Plan R#** on a skill card.
- **Copy plan as text** makes it easy to share a build with someone else.

**Loading a preset replaces the future queue only**. It does not undo any skill ranks already recorded as purchased.

The roadmap shows estimated levels, assuming one skill point earned per level. Challenges and tier prerequisites can delay the real purchase. A roadmap step is not itself an actual skill purchase.

## 4. Learn a skill rank

Use this workflow **after buying the rank in the game**, to keep ORBIT aligned:

1. Make sure your planner's **level** matches your level in Starfield.
2. Check the skill's category tier requirement.
3. If you already own a rank of the skill, complete the corresponding challenge in Starfield.
4. Check **Mark challenge complete** on the corresponding Roadmap/Overview row, or check the challenge box in **Skill library**.
5. Tap **Learn**. ORBIT records the rank, deducts one planner point, and removes one matching future upgrade from the queue.

### Why does Learn say locked?

The button is **intentionally tappable**. Tapping **Learn · locked** displays why the purchase is blocked:

| Blocker | What to do |
| --- | --- |
| Not enough skill points | Increase your level when you actually level up in Starfield |
| Current-rank challenge incomplete | Finish it in Starfield and tick the challenge checkbox in ORBIT |
| Tier not unlocked | Buy enough ranks in the same skill category first |
| Earlier rank required | Learn the lower rank of that specific skill first |
| Rank 4 already reached | That skill is maxed out; remove extra queued ranks |

**Important:** The checkbox does not complete an in-game challenge; it records your confirmation that you finished it. For most skills, ORBIT uses a **generic reminder** rather than the full exact challenge description. Always check the real challenge in Starfield.

### Category gates

Skills are split into **Physical, Social, Combat, Science, and Tech**. ORBIT enforces these category thresholds:

| Tier | Required ranks already invested in category |
| --- | ---: |
| 1 | 0 |
| 2 | 4 |
| 3 | 8 |
| 4 | 12 |

The starting Bounty Hunter ranks count toward the category totals where applicable. Each rank bought adds one point to the relevant category.

### Correcting a mistake

On a **Skill library** card, you can use the **↶ Undo** control to revert the most recently recorded purchased rank of that skill. It only changes your planner data, not the game. The three starting ranks cannot be undone.

## 5. Find skills in the library

Open **Skill library** to explore the complete catalogue of 82 skills.

- **Search** by skill name or description.
- **Category** filter: Physical, Social, Combat, Science or Tech.
- **Tier** filter: 1 through 4.
- **Owned only** limits the results to skills with a recorded rank.
- **+ Plan** appends a future rank to the Roadmap without spending points.
- **Learn** records the next rank, provided its requirements are satisfied.

## 6. Profile and notes

On **Character**, you can:

- Change the captain's displayed name and level.
- Edit the three trait labels.
- Write notes about your desired ship loadout, factions, equipment, or next missions.
- Select **Save profile** and **Save notes** for those respective fields.
- Export/import the character JSON.
- Reset to a fresh Bounty Hunter build.

The background is fixed to **Bounty Hunter** in v1.1; changing the trait text does not rebuild the background or starting ranks.

## 7. Back up or transfer saves

ORBIT automatically stores progress in local browser storage under the key `orbit-starfield-v1`. This is device-/browser-/site-specific storage. There is **no cloud sync**.

### Export a backup

1. Open **Character**.
2. Tap **↓ Export save**.
3. Keep the downloaded **`starfield-orbit-save.json`** in a safe location.

### Restore or move to another device

1. Open ORBIT on the destination device or browser.
2. Open **Character**.
3. Select **↑ Import save**.
4. Choose the exported JSON file.
5. Confirm that you want to replace the current planner data.

Exporting is especially important when moving from a locally downloaded HTML file to the GitHub Pages URL, opening ORBIT in a different browser, or switching phones.

**Warning:** Import replaces existing ORBIT data. Reset clears your progress, notes, and roadmap. Export before trying either operation if you may want your current character back.

The v1.1 import path accepts prior v1 JSON saves.

## 8. Use ORBIT on mobile

The interface is responsive and intended to work in mobile browsers. Open the [planner URL](https://jlhiskey.github.io/starfield-orbit/) on your phone. Depending on your browser, use the browser menu to add the website to your home screen.

A home-screen shortcut is just a way to open the site; it does **not** turn local browser saves into cloud-synced saves. Keep periodic JSON backups.

## 9. Troubleshooting

### I can increase my level, but Learn won't work

This was the main issue fixed in **v1.1**. The Roadmap and Overview now include challenge checkboxes, and tapping a blocked Learn button explains the missing requirement. If the page still behaves like v1, reload to get the newest `index.html`. Do **not** clear site data without exporting your save.

### I completed the challenge in Starfield but Learn is locked

The app cannot inspect the game. Tick the challenge's checkbox manually, then tap Learn again. If it remains locked, inspect the explanation for missing category points or earlier ranks.

### I get a tier warning in the Roadmap

That part of the future queue is scheduled before the prerequisite category investment. Move lower-tier upgrades earlier in the queue, or choose different skills.

### My progress vanished on a different device

That is expected for browser-local saves. Restore from your most recent exported `.json` file. Without an exported backup, the planner cannot recover progress from another browser or device.

### The site link displays a 404

GitHub Pages must be enabled for the repository:

1. Visit [Settings → Pages](https://github.com/jlhiskey/starfield-orbit/settings/pages).
2. Set **Source** to **Deploy from a branch**.
3. Choose **main** and **/(root)**, then Save.
4. Return to https://jlhiskey.github.io/starfield-orbit/ after deployment.

### I changed the code but the old UI still appears

Refresh the hosted page. If necessary, perform a force refresh to bypass a cached copy. Back up saves before changing or clearing any browser storage.

## 10. Known limitations

- **Background selection is not generalized**; the initial build is Bounty Hunter.
- **The skill catalogue is broad**, but the app only includes specific rank-challenge descriptions for a subset of skills.
- **No integration with Starfield itself:** ranks, challenges and level are updated manually.
- **No cloud sync or multi-character account system.** JSON export/import is the portability mechanism.
- **Projected roadmap levels** are estimates, not a guaranteed leveling schedule.
- Skills and descriptions can differ with game versions and updates; check in-game text if in doubt.

---

ORBIT is an unofficial fan-made planning tool. *Starfield* is a game by Bethesda Game Studios.
