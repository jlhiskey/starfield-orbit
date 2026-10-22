# Changelog

All notable changes to the ORBIT character progression planner are summarized here.

[← Back to README](README.md) · [Launch ORBIT](https://jlhiskey.github.io/starfield-orbit/)

## v1.2 — Character-aware Advisor chat

- Added a responsive **Advisor** tab with conversation history and quick questions.
- Added character-aware rule-based local guidance for skill-point mismatches, roadmap decisions, challenges, and Undo.
- Added an optional authenticated Cloudflare Worker backend using the OpenAI Responses API for full AI chat. Requires separate deployment and credentials.
- Added **Copy context & open ChatGPT** for an AI handoff without a custom backend.
- Preserved the existing Bounty Hunter save format and skill purchase rules.

## v1.1 — Learn-button and challenge-tracking fix

- Added rank-challenge checkboxes directly to **Roadmap** and **Overview**, not just the Skill library.
- Changed blocked **Learn** buttons so they can be tapped and explain their requirements, instead of appearing broken.
- Displayed missing prerequisites in the Skill library.
- Prevented future Roadmap rows from accidentally purchasing a different, earlier rank.
- Preserved the ability to import v1 character JSON backups.

## v1.0 — Initial planner

- Responsive single-file HTML interface.
- Skill library covering 82 skills in five categories.
- Bounty Hunter starting build and suggested level-by-level progression.
- Editable progression queue and build presets.
- Skill point, tier gate, and challenge tracking.
- Local browser saves plus JSON export and import.

## Compatibility

The app is a manual planner, not a Starfield save editor. Current character data remains stored locally in the browser using the `orbit-starfield-v1` key. The version in the browser address (local file versus hosted page) affects which storage area is used. Back up with JSON before changing devices or origins.
