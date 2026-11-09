# OneTag AI plugin

Adds a working AI feature to a static site from inside your coding agent: a Q&A box that answers from the page, a summarizer, a translator, an FAQ bot, extract-to-JSON, alt text or a quiz. One script tag, a public key, no backend. Works in Claude Code, GitHub Copilot and Gemini CLI (one repository, three manifests).

## What the skill does

1. Reads the public reference at https://onetagai.com/llms.txt.
2. Asks which email the key should go to and, only after you confirm, sends one request to onetagai.com to create a free key. The key arrives by email and you paste it back.
3. Picks a ready-made block from [Static AI Block](https://github.com/fengyiqicoder/static-ai-block), inserts it into your HTML, Astro, Hugo, Jekyll or Eleventy templates, and replaces the key placeholder.
4. Opens the page and checks the feature answers once.

## Data

The plugin runs no local code and has no hooks. It reads no credentials from your machine. The only data it sends is the email address you confirm, once, to `https://onetagai.com/api/signup`; the only other network requests fetch public documentation and block files. OneTag AI itself keeps token counts and timestamps per key, not page text or questions. This key is designed to be public, like an analytics ID, and can only spend that account's allowance (1,000,000 free tokens per account). If OneTag does not fit your project, the agent will say so.

## Install

Claude Code:

```
/plugin marketplace add fengyiqicoder/onetag-claude-plugin
/plugin install onetag@onetag
```

GitHub Copilot (once listed): `copilot plugin install onetag@awesome-copilot`

Then say "add an AI FAQ bot to this site with OneTag" or run `/onetag-setup`.

MIT.

## See also

- [Static AI Block](https://github.com/fengyiqicoder/static-ai-block): the blocks this skill inserts.
- [Lantern](https://github.com/fengyiqicoder/astro-docs-ai) and [Pitch](https://github.com/fengyiqicoder/astro-landing-ai): free Astro templates with the AI already wired in.
