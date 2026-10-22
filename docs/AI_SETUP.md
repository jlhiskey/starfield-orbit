# ORBIT Advisor: Optional AI setup

[Back to README](../README.md) · [Open ORBIT](https://jlhiskey.github.io/starfield-orbit/)

ORBIT v1.2 ships with a new **Advisor** tab, with two different modes:

- **Local guide (no setup):** Works in your browser and gives character-specific advice on points, skills, challenges, ship upgrades, and roadmap. This is deterministic code, not a large language model.
- **AI mode (optional):** A real conversational Starfield advisor powered by an OpenAI model. It requires a privately deployed Cloudflare Worker, your own API key, and an additional gateway access token. API usage can incur separate charges even if you subscribe to ChatGPT.

GitHub Pages is static hosting. **Never paste an OpenAI API key into the browser app, or publish one to GitHub.**

## Deploy the gateway

You need a Cloudflare account, Node.js/npm, and an OpenAI API key with appropriate billing/access configured.

```bash
git clone https://github.com/jlhiskey/starfield-orbit.git
cd starfield-orbit/worker
npx wrangler login
npx wrangler deploy
npx wrangler secret put OPENAI_API_KEY
npx wrangler secret put ORBIT_CHAT_TOKEN
```

When prompted for `OPENAI_API_KEY`, provide your API key **in Cloudflare's terminal prompt only**. When prompted for `ORBIT_CHAT_TOKEN`, set a long, unique random passphrase. This is a second secret that controls access to your paid backend; it is **not** your OpenAI API key.

The deploy command prints a Worker URL similar to `https://orbit-starfield-advisor.YOUR-SUBDOMAIN.workers.dev`. Add `/chat` to the end to get the endpoint URL.

## Connect from your planner

1. Open [ORBIT](https://jlhiskey.github.io/starfield-orbit/), select **✦ Advisor**.
2. Open **AI connection → Configure**.
3. Paste your Worker's complete **HTTPS** endpoint ending in `/chat`.
4. Enter the `ORBIT_CHAT_TOKEN` access passphrase, not your OpenAI API key.
5. Click **Connect AI**. Send a question about your actual character.

The browser only saves the endpoint URL. It keeps the access passphrase in memory until the page is refreshed or closed. Nothing is stored in the GitHub repository.

## Privacy, security and cost

- The AI gateway receives your manually entered character name, level, traits, owned skills, roadmap, current question, and up to 12 recent chat messages. It **does not** transmit your free-form Character notes.
- Chat history remains in local browser storage. AI questions and these selected fields go to Cloudflare and the model provider when you opt into AI mode.
- The gateway checks for the `jlhiskey.github.io` browser origin and requires a separate passphrase. **CORS origin checks are not authentication**, so keep the passphrase private.
- For a website shared with other people, add real authentication, a rate limiter, and API spending controls before enabling broad access. Rotate the `ORBIT_CHAT_TOKEN` secret if compromised.
- You can change the model by setting `OPENAI_MODEL` in `worker/wrangler.toml` and redeploying. The default is `gpt-5-mini`.
- Your GitHub Pages site continues to work entirely in **Local guide** mode without Cloudflare or an OpenAI key.

## Without an API key

**Copy context & open ChatGPT** copies a prompt that includes your current character and last question. ChatGPT opens in a new tab; paste the text there. This is a handoff, not in-app AI chat, and does not require an API backend.

## Errors

| Error | Resolution |
| --- | --- |
| Incorrect ORBIT access token | Re-enter the exact value of `ORBIT_CHAT_TOKEN` configured in Cloudflare |
| Origin not allowed | Use the hosted GitHub Pages site, not a local file; the Worker only accepts that website origin |
| Quota or rate limit | Check OpenAI API billing and usage controls |
| Gateway HTTP error | Confirm your Worker is deployed and its URL ends in `/chat` |
| Empty response | Check Worker logs and verify model/API access |

References: [OpenAI Responses API](https://developers.openai.com/api/docs/guides/text), [Cloudflare Worker secrets](https://developers.cloudflare.com/workers/configuration/secrets/).