# Multiplex

Send one message to several AI models at once and compare their replies side by side — entirely in your browser, with your own free-tier API keys.

Multiplex is a single self-contained HTML file. There's no build step, no server, and no backend of any kind — open the file in a browser (or host it as a static page) and it just works.

## Features

- **Parallel comparison** — up to 4 columns, each running a different provider/model, all answering the same message at once
- **5 built-in providers**, every one of them genuinely usable on a free tier (see table below)
- **Image generation** on the providers that support it (Google, OpenRouter, Cloudflare)
- **Voice** — read replies aloud, dictate your message instead of typing, or start a real-time voice conversation (Gemini Live API)
- **Web search toggle** for providers with a native search tool
- **Chat history** — past conversations are saved locally and browsable from the sidebar
- **Resizable, collapsible sidebar** — drag the edge to resize, or collapse it to an icon rail
- **Optional Supabase sign-in** — entirely opt-in; the app works fully without it (see below)
- **A first-run rules screen** — shown once, before anything else is usable

## Supported providers

| Provider | Default model | Notes |
|---|---|---|
| Google AI Studio | `gemini-3.6-flash` | Image generation supported |
| Groq | `openai/gpt-oss-120b` | |
| OpenRouter | `nvidia/nemotron-3-super-120b-a12b:free` | Must use a `:free`-suffixed model to stay on the free tier; image generation supported |
| Mistral AI | `mistral-large-latest` | |
| Cloudflare Workers AI | `@cf/meta/llama-3.3-70b-instruct-fp8-fast` | Requires your Cloudflare account ID in the base URL; image generation supported |

Every provider ships with a **"Get free key"** link in Settings pointing to where to sign up.

## Getting started

1. Download `chatbot_parallel.html`.
2. Open it directly in a browser, or host it anywhere that serves static files (GitHub Pages, Netlify, Vercel, S3, etc.) — no build, no install.
3. On first launch you'll see a short rules screen. Read it and check the box to continue.
4. Click the **Settings** icon in the sidebar and paste in an API key for at least one provider.
5. Type a message — it goes out to every active column at once.

## Adding API keys

All keys are entered by you, in Settings, and stored only in your own browser's local storage. Nothing is proxied through any server Multiplex controls — every request goes straight from your browser to that provider's own API.

Each provider's key format and base URL are pre-filled with sensible defaults; you can change the base URL, default model, or per-provider max-reply-length ceiling from the same screen.

## Optional: Supabase sign-in & Premium

Signing in is **not required** to use Multiplex. The only place it comes up is an "Upgrade to Premium" button in the sidebar — clicking it will:

1. Ask for a Supabase project URL + anon key, if none is configured yet
2. Prompt you to sign in or create an account
3. Show a placeholder upgrade confirmation

> **Note:** "Premium" currently just sets a flag on the signed-in user's account — there's no payment processor wired up, and no feature is actually gated behind it yet. Treat it as scaffolding for whatever you want Premium to mean (more columns, cloud-synced history, etc.), not a finished paywall.

To set this up, create a free project at [supabase.com](https://supabase.com) and grab the URL and anon key from **Settings → API**.

## Privacy & data

- API keys, chat history, and preferences all live in `localStorage`, scoped to whichever browser you're using. Nothing syncs across devices unless you build that yourself.
- If you use Supabase sign-in, your email/password are handled entirely by Supabase's own auth — Multiplex never sees or stores your password.
- Clearing your browser's site data will erase saved keys and chat history.

## Tech stack

- [React 18](https://react.dev) and [Babel Standalone](https://babeljs.io/docs/babel-standalone), loaded from a CDN — JSX is compiled in-browser, so there's nothing to build
- [Supabase JS SDK](https://supabase.com/docs/reference/javascript) for the optional auth flow
- No bundler, no package.json, no node_modules — the whole app is the one HTML file

## Known limitations

- Free-tier rate limits are real and vary by provider — see each provider's own dashboard for current limits.
- "Premium" is a placeholder (see above).
- No cross-device sync of chats or keys.

## License

No license file is included yet — add one (MIT is a common choice for a project like this) before treating this as open source.
