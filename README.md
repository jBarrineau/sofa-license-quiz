# USFJ SOFA Permit — Practice Quiz

A single-page practice quiz for the U.S. Forces Japan SOFA driver's permit test. Pick your topics and session length, answer multiple-choice questions, and get an explanation and study-guide page reference for every answer.

**Live:** https://jbarrineau.github.io/sofa-license-quiz/

## Features

- **169 questions** across four topics — road signs (83), rules of the road (45), licensing & paperwork (22), signals & markings (19).
- **93 embedded sign images**, so 89 of the questions can ask you to identify an actual Japanese road sign.
- **Session setup** — filter to one topic or the whole bank, choose 20 questions, 50, or the full bank, and toggle question shuffling.
- **Immediate feedback** — answer options are shuffled per question; a wrong pick shows the correct answer, why it's correct, and the briefing page it came from.
- **Results breakdown** — overall score, a per-topic bar chart, and a list of everything you missed.
- **Retry the misses** — restart a session made up only of the questions you got wrong.
- **Keyboard driven** — keys `1`–`4` to answer, `Enter` for the next question.

## Running it

The whole app is one self-contained `index.html` — no build step, no dependencies, no server required. Open the file in a browser, or serve the directory:

```sh
python -m http.server 8000
```

Then visit http://localhost:8000. The only network requests are to Google Fonts; sign images are inlined as data URIs, so the quiz works offline once the page has loaded.

## Question bank

Questions live in the `BANK` array inside `index.html`. Each entry looks like:

```js
{
  "cat": "rules",              // rules | signs | signals | admin
  "q": "…question text…",
  "options": ["…", "…", "…", "…"],
  "a": 2,                      // index of the correct option
  "why": "…explanation…",
  "img": null,                 // key into IMAGES, or null
  "p": 1                       // study guide page number
}
```

Sign images are keyed in the `IMAGES` object as base64 data URIs. To add a question, append an object to `BANK`; per-topic counts on the setup screen update automatically.

The bank is also exposed to embedding pages over `postMessage` — post `"sofa-flashcards:request"` to the frame and it replies with `{type: "sofa-flashcards:data", bank, images, categories, categoryNames}`.

## Related

[sofa-license-flashcards](https://github.com/jBarrineau/sofa-license-flashcards) — the same question bank as a spaced-repetition flashcard deck.

## Disclaimer

Study aid only. The Station Safety Center briefing and PMO Pass & Registration are the authority on licensing requirements and Japanese traffic law.
