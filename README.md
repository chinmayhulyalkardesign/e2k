# English → Kannada

A small, personal translator built from your own vocabulary notes — no
backend, no API keys, no ML model. Open `index.html` in a browser and go.

## What it does

**Translate** — type an English sentence and get romanized Kannada. It
tries, in order:
1. **Saved phrases** — an exact match against the full sentences in your notes
   (`Where do you work?` → `Neevu elli keLsa maaDutteera?`).
2. **Sentence frames** — the grammar patterns from your notes (`I like ___`,
   `I want ___`, `I have ___`, `give me ___`, `my name is ___`, `I work in
   ___`, …). The `___` slot is looked up in your word dictionary.
3. **Word-by-word fallback** — anything else gets translated word by word.
   Words not in your dictionary are left in English and shown in grey,
   dotted-underline italics, so you always know what it actually knows versus
   what it guessed/kept.

**Dictionary** — search your word list in both directions.

## Running it

No build step — it's one static HTML file.

```bash
open index.html          # macOS
xdg-open index.html      # Linux
```

Or serve it locally:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

To deploy for free: push this repo and turn on **GitHub Pages** (Settings →
Pages → deploy from branch) — `index.html` at the repo root works as-is.

## Extending it

Everything is data at the top of the `<script>` block in `index.html`:

- `DICT` — words and short entries, `[english, kannada, category]`.
- `PHRASES` — full canned sentences, `[english, kannada]`.
- `FRAMES` (further down) — regex sentence templates like `I like ___`.

Add a row, reload the page — no other code changes needed for new
vocabulary or phrases. New sentence *shapes* need a new entry in `FRAMES`.

## Known limits

- This is a rule-based, personal-vocabulary translator, not a general
  machine translation system — it only knows what's in the notes above.
- Kannada is shown romanized (Latin script), not in the Kannada script.
