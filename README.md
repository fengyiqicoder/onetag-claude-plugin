# OneTag AI plugin for Claude Code

Adds AI to any static site from inside Claude Code: a skill that signs the user up for a free [OneTag AI](https://onetagai.com/?ref=claude-plugin) key with their email, inserts a ready-made block (ask this page, summarize, translate, FAQ bot, extract to JSON, alt text, quiz…), and tests it. One script tag, no backend, no API key in the page.

## Install

```
/plugin marketplace add fengyiqicoder/onetag-claude-plugin
/plugin install onetag@onetag
```

Then say "add an AI FAQ bot to this site" or run `/onetag-setup`.

## What the skill does

1. Reads the API reference at https://onetagai.com/llms.txt.
2. Asks for your email and POSTs it to the signup endpoint; the key arrives in your inbox.
3. Inserts a block from [Static AI Block](https://fengyiqicoder.github.io/static-ai-block/) and replaces the placeholder key.
4. Opens the page and tries the feature once.

Free: 1,000,000 tokens per account. The key is public by design and can only spend that allowance. MIT.
