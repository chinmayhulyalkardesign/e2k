# English → Kannada

A small, personal translator built from your own vocabulary notes — no
backend, no API keys, no ML model. Open `index.html` in a browser and go.

## What it does

**Translate** — type or speak an English sentence and get romanized Kannada.
It tries, in order:
1. **Saved phrases** — an exact match against the full sentences in your notes
   (`Where do you work?` → `Neevu elli keLsa maaDutteera?`).
2. **Sentence frames** — the grammar patterns from your notes (`I like ___`,
   `I want ___`, `I have ___`, `give me ___`, `my name is ___`, `I work in
   ___`, …). The `___` slot is looked up in your word dictionary.
3. **Word-by-word fallback** — anything else gets translated word by word.
   Words not in your dictionary are left in English and shown in grey,
   dotted-underline italics, so you always know what it actually knows versus
   what it guessed/kept.

Voice:
- 🎤 **Speak** uses the browser's `SpeechRecognition` API to transcribe
  English speech into the input box (Chrome desktop/Android; not supported
  in Firefox or Safari — the button disables itself there).
- 🔊 **Listen** uses `speechSynthesis` to read the Kannada result aloud. Real
  Kannada text-to-speech voices are rare on most systems, so it prefers a
  Kannada voice if one exists, falls back to Hindi (phonetically closer to
  the romanization), then to a default voice — pronunciation of the
  romanized text will be approximate either way.

**Dictionary** — search your word list in both directions.

**Sentence builder** — pick a subject, tense, verb and object to see
conjugated forms assembled from the suffix rules in your notes (continuous /
future) or looked up per-verb (irregular past forms). Marks whether a form
is *attested* (seen in your assignments) or *built by rule* (double-check
spelling).

## Running it

No build step — it's one static HTML file.

```bash
open index.html          # macOS
xdg-open index.html      # Linux
```

Or serve it locally so voice features work over `https`-like conditions in
some browsers:

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
- `VERBS` — verb roots, `-ing` stems, and irregular past forms for the
  sentence builder.

Add a row, reload the page — no other code changes needed for new
vocabulary or phrases. New sentence *shapes* need a new entry in `FRAMES`.

## Known limits

- This is a rule-based, personal-vocabulary translator, not a general
  machine translation system — it only knows what's in the notes above.
- Kannada is shown romanized (Latin script), not in the Kannada script.
- Voice input/output quality depends entirely on the browser and OS; there's
  no server-side speech processing.
