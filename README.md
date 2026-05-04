# JLPT N3 Prep App

A self-contained web app for preparing for the **JLPT N3** (Japanese Language Proficiency Test, level N3). Includes a diagnostic test, themed learning modules, mock exams, searchable dictionaries, flashcards with reversible cards, and progress tracking.

## Features

- 📋 **Diagnostic test** with personalized recommendations
- 📚 **Five learning modules**: Kanji, Vocabulary, Grammar, Reading, Listening
- 📝 **Mock exams** matching the official JLPT N3 format
- 📖 **Searchable dictionaries** for vocabulary and expressions/adverbs
- 🃏 **Flashcards** with two directions: JP → reading + meaning, or EN → kanji + reading
- 📊 **Progress tracking** with localStorage persistence
- 🌓 **Dark mode** + display modes (furigana / kanji-only / kana-only)
- 💡 **Auto-hover tooltips** on every Japanese word — hover any kanji/word to see its reading and English meaning instantly
- 🔊 **Listening practice** using browser Japanese TTS

## Deployment

### GitHub Pages (recommended)

1. Push this folder to a GitHub repo
2. In repo Settings → Pages, set source to `main` branch, root folder
3. Visit `https://<your-username>.github.io/<repo-name>/`

### Local development

The app fetches JSON data files, which means **opening `index.html` directly with `file://` will not work** (browsers block local fetch). Use a local server:

```bash
# Python 3
python3 -m http.server

# Then open http://localhost:8000 in your browser
```

Or any other static server (live-server, http-server, etc.).

## Adding more vocabulary/kanji

All learning content lives in `data/*.json` files — **the HTML never needs to change to add more words**. Just edit the JSON files and push.

### File structure

```
.
├── index.html              ← the app (no data inside)
├── data/
│   ├── vocab.json          ← vocabulary entries
│   ├── kanji.json          ← kanji with readings + examples
│   ├── expressions.json    ← adverbs, conjunctions, set phrases
│   ├── grammar.json        ← grammar lessons with quizzes
│   ├── readings.json       ← reading comprehension passages
│   ├── listening.json      ← listening dialogue scripts
│   ├── diagnostic.json     ← diagnostic test questions
│   └── exams.json          ← mock exams
└── README.md
```

### Schema

**`vocab.json`** — array of:
```json
{
  "w": "勉強",
  "r": "べんきょう",
  "m": "study",
  "pos": "noun, suru-verb",
  "theme": "education",
  "ex": [{"jp": "毎日勉強します。", "r": "まいにち べんきょう します。", "en": "I study every day."}]
}
```

Themes used: `daily-life`, `work`, `travel`, `emotions`, `food`, `health`, `education`, `society`, `people`, `time`, `nature`, `verbs`, `adjectives`. Add new themes freely — the dictionary will pick them up automatically.

**`kanji.json`** — array of:
```json
{
  "k": "勉",
  "on": "ベン",
  "kun": "つと（める）",
  "m": "exertion, study",
  "ex": [{"w": "勉強", "r": "べんきょう", "m": "study"}],
  "theme": "effort"
}
```

Kanji themes: `thinking`, `movement`, `society`, `emotion`, `health`, `nature`, `quantity`, `time`, `communication`, `effort`, `position`, `modern`.

**`expressions.json`** — array of:
```json
{
  "w": "やはり",
  "r": "やはり",
  "m": "as expected, after all",
  "type": "adverb",
  "ex": [{"jp": "やはり彼が一番速いです。", "r": "やはり かれが いちばん はやいです。", "en": "As expected, he's the fastest."}]
}
```

Types: `adverb`, `conjunction`, `set-phrase`.

**`grammar.json`** — array of:
```json
{
  "id": "youni-naru",
  "title": "〜ようになる",
  "titleEn": "to come to / to begin to",
  "explanation": "<p>HTML allowed here…</p>",
  "examples": [{"jp": "...", "r": "...", "en": "..."}],
  "quiz": [{"q": "...", "choices": ["a","b","c","d"], "answer": 0}]
}
```

**`readings.json`** — array of:
```json
{
  "id": "r1",
  "title": "京都旅行 / Kyoto Trip",
  "level": "短文",
  "text": "Japanese passage...",
  "translation": "English translation...",
  "questions": [{"q": "...", "choices": ["a","b","c","d"], "answer": 1}]
}
```

**`listening.json`** — same as readings but with a `script` field (Japanese text to feed to TTS):
```json
{
  "id": "l1",
  "title": "天気予報 / Weather Forecast",
  "script": "明日の天気...",
  "questions": [...]
}
```

**`diagnostic.json`** — array of:
```json
{ "cat": "vocab", "q": "...", "choices": ["a","b","c","d"], "answer": 0 }
```

Categories: `vocab`, `kanji`, `grammar`, `reading`, `listening`.

**`exams.json`** — array of mock exams:
```json
{
  "id": "exam1",
  "title": "模擬試験 1 / Mock Exam 1",
  "description": "...",
  "sections": [
    {
      "name": "言語知識(文字・語彙) — Kanji & Vocabulary",
      "questions": [{"q": "...", "choices": [...], "answer": 0}]
    }
  ]
}
```

## Data persistence

All user progress (diagnostic results, module completion, exam scores, custom flashcards, theme preference) saves to `localStorage` under the key `jlpt_n3_app_v1`. Data persists per-browser, per-device. Use the Reset button on the Progress page to clear everything.

## License

Personal use. No external services or analytics.
