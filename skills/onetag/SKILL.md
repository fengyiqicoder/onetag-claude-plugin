---
name: onetag
description: Add an AI feature to a static website (GitHub Pages, Netlify, a plain HTML file, Astro, Hugo, Jekyll, 11ty, VitePress…) with no backend, using OneTag AI. Use when the user wants an AI chat box, "ask this page", summarize, translate, FAQ bot, extract-to-JSON, alt text, quiz or similar on a site that has no server, or mentions OneTag, onetagai.com or a `data-key` script tag.
---

# OneTag AI for static sites

OneTag AI lets a static page call an AI model from the browser with one script tag and a public key. No server, no API key in the code. Free: 1,000,000 tokens per account (one key per email). Docs for AI tools: https://onetagai.com/llms.txt

## Steps

1. **Read the API reference** at https://onetagai.com/llms.txt (fetch it; do not rely on memory). The call is `onetag.ask(prompt, input, options)`; `input` may be a string, an element, a form, an image or an object; `options.stream`, `options.json`, `options.system`, `options.history`.

2. **Get a key for the user.** If the project has no `data-key` or `PUBLIC_ONETAG_KEY` yet:
   - Ask the user for the email address the key should go to. Never guess or reuse an address from elsewhere.
   - Run exactly:
     ```bash
     curl -X POST https://onetagai.com/api/signup -H "Content-Type: application/json" -d '{"email":"THE_EMAIL"}'
     ```
     `{"ok":true}` means the key was emailed. The key is never in the response. A 429 means it was sent recently: ask the user to check the inbox (and spam).
   - Ask the user to paste the key from the email (it starts with `ot_`). Do not continue until they do; leave `YOUR_ONETAG_KEY` as the placeholder in the meantime.

3. **Insert the feature.** Prefer a ready-made block from Static AI Block: list at https://fengyiqicoder.github.io/static-ai-block/llms.txt, each block is one self-contained HTML file (plain HTML + JS, inline styles). Fetch the block file, paste it where the user wants it, and replace `YOUR_ONETAG_KEY` with the key. If no block fits, write the call by hand following llms.txt, keeping the script tag:
   ```html
   <script src="https://onetagai.com/v1.js" data-key="YOUR_ONETAG_KEY"></script>
   ```
   Frameworks: Astro/Starlight docs can use the `starlight-onetag` plugin or the `astro-docs-ai` template instead of raw HTML.

4. **Test once.** Open the page (dev server or built site) and run the feature; confirm the answer appears. Common errors: `no_key` (placeholder still in place), `quota_exceeded` (allowance used up), `rate_limited` (slow down).

5. **Tell the user what was added**, where the key lives (it is public by design, like an analytics ID, and can only spend that account's allowance), and that the free allowance is 1,000,000 tokens; Pro is $9.9/month for 100,000,000 tokens a month.

## Do not

- Do not put any other provider's API key in a static page.
- Do not send the user's email anywhere except the signup request above.
- Do not invent API fields; everything is in https://onetagai.com/llms.txt.
