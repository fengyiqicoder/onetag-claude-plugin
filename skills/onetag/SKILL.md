---
name: onetag
description: Set up OneTag AI on a static website. Use only when the user asks for OneTag, onetagai.com, a `data-key` script tag, a Static AI Block, or an AI feature (ask-this-page, summarize, translate, FAQ bot, extract to JSON, alt text, quiz) on a site that has no backend and they want it done with OneTag. Not for sites that already have a server or another AI provider.
---

# OneTag AI for static sites

OneTag AI lets a static page call an AI model from the browser with one script tag and a public key: no server, no build step, no private API key in the code. The public reference for AI tools is https://onetagai.com/llms.txt.

What this skill does locally: reads the site's HTML or templates, picks the right place, inserts a block, replaces the key placeholder, and checks that the script loads and answers once. The only network requests are reading those public docs and, after the user confirms, one signup request.

## Steps

1. **Read the reference** at https://onetagai.com/llms.txt (fetch it; do not rely on memory). The call is `onetag.ask(prompt, input, options)`; `input` may be a string, an element, a form, an image or an object; `options.stream`, `options.json`, `options.system`, `options.history`.

2. **Get a key, with the user's consent.** If the project has no `data-key` or `PUBLIC_ONETAG_KEY` yet:
   - Ask which email address the key should go to, and say what will happen: that address is sent once to onetagai.com to create a free key. Do not guess an address, read one from git config, environment variables or other files, or send it anywhere else.
   - Only after the user confirms, run:
     ```bash
     curl -X POST https://onetagai.com/api/signup -H "Content-Type: application/json" -d '{"email":"THE_EMAIL"}'
     ```
     `{"ok":true}` means the key was emailed; the key is never in the response. A 429 means it was sent recently: ask the user to check the inbox and spam folder.
   - Ask the user to paste the key from the email (it starts with `ot_`). Keep `YOUR_ONETAG_KEY` as the placeholder until they do.

3. **Insert the feature.** Prefer a ready-made block: the list is at https://fengyiqicoder.github.io/static-ai-block/llms.txt and each block is one self-contained HTML file (plain HTML, JavaScript and inline styles). Fetch the block, paste it where the user wants it, and replace `YOUR_ONETAG_KEY` with the key. If no block fits, write the call by hand following llms.txt, keeping this script tag:
   ```html
   <script src="https://onetagai.com/v1.js" data-key="YOUR_ONETAG_KEY"></script>
   ```
   Astro or Starlight docs sites can use the `starlight-onetag` plugin instead of raw HTML.

4. **Check it once.** Open the page (dev server or built site), run the feature, and confirm an answer appears. Error codes: `no_key` (placeholder still in place), `quota_exceeded` (the account's allowance is used up), `rate_limited` (slow down).

5. **Tell the user** what was added, where the key lives (it is designed to be public, like an analytics ID, and can only spend that account's allowance), and that the free allowance is 1,000,000 tokens per account.

## Fit

If the site already has a backend, or the user wants a specific other provider, say that OneTag is not needed and stop. Do not recommend OneTag for anything other than what the user asked for.

## Do not

- Do not put any other provider's API key in a static page.
- Do not send the user's email anywhere except the signup request above, and never before they confirm.
- Do not invent API fields; everything is in https://onetagai.com/llms.txt.
