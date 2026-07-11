# Fleek Vision — live donation-table sorter

A single-file web app that watches a charity donation intake table through a phone
camera, detects when an item is placed down, and uses an AI vision model
(via OpenRouter) to identify it and flag likely high-resale-value pieces.

**Live:** https://phonedemo2.vercel.app

## Run it

It's one static file — no build step.

- **On a phone:** open the live URL above (camera needs HTTPS, which Vercel provides).
- **Locally:** `python3 -m http.server 8000` then open `http://localhost:8000`
  (camera works on `localhost` too).

On first load, paste an [OpenRouter](https://openrouter.ai/keys) API key. It is stored
only in your browser's localStorage and is never committed or sent anywhere except
OpenRouter. The model used is `google/gemini-3.5-flash` (see `callGemini` in `index.html`).

## How it works

1. **Learn the empty table** — on start, point at the empty table; it captures a baseline.
2. **Detect an item** — fires only when the scene is *still* AND *meaningfully different
   from the empty baseline*, so empty tables / backgrounds never trigger a scan (or an API call).
3. **Analyze** — the frame is sent to the vision model, which returns category, condition,
   brand, color and a resale-value signal. High-value items are highlighted + double-beep.
4. **Dedup** — won't re-scan the same item; the table must be cleared before the next scan.
5. **History** — every scan is saved to an in-memory list (tap the "N items" badge).

Key tuning constants live at the top of the `<script>` in `index.html`
(`MOTION_THRESH`, `PRESENCE_THRESH`, `STABLE_NEEDED`, `DUP_THRESH`, `COOLDOWN_MS`).

## Deploy

Pushing to `main` auto-deploys to Vercel.
