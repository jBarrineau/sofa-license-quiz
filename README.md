# USFJ SOFA Permit — Practice Quiz

A single-page practice quiz for the U.S. Forces Japan SOFA driver's permit test. Pick your topics and session length, answer multiple-choice questions, and get an explanation and study-guide page reference for every answer.

**Live:** https://jbarrineau.github.io/sofa-license-quiz/

## Features

- **181 questions** across four topics — road signs (83), rules of the road (54), licensing & paperwork (24), signals & markings (20).
- **125 keyed visuals**, including 93 embedded road signs and 32 source diagrams/photos, so visual questions include the material they ask about.
- **Session setup** — filter to one topic or the whole bank, choose 20 questions, 50, or the full bank, and toggle question shuffling.
- **Immediate feedback** — answer options are shuffled per question; a wrong pick shows the correct answer, why it's correct, and the briefing page it came from.
- **Linked sources** — every page reference is a link that opens `Training for SOFA License.pdf` in a new tab at that exact page.
- **Results breakdown** — overall score, a per-topic bar chart, and a list of everything you missed.
- **Retry the misses** — restart a session made up only of the questions you got wrong.
- **Keyboard driven** — keys `1`–`4` to answer, `Enter` for the next question.

## Running it

The app is static — no build step, dependencies, or server required. Open `index.html` in a browser, or serve the directory:

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
  "p": 1                       // page in Training for SOFA License.pdf
}
```

`p` is a 1:1 PDF page number in `Training for SOFA License.pdf`, which ships in the repo and is linked as
`Training%20for%20SOFA%20License.pdf#page=<p>`. The `#page=` fragment is honoured by the Chrome, Edge,
Firefox and desktop Safari PDF viewers; iOS Safari ignores it and opens the guide at page 1.

Images are keyed in the `IMAGES` object as base64 data URIs or local asset paths. To add a question, append an object to `BANK`; per-topic counts on the setup screen update automatically.

The bank is also exposed to embedding pages over `postMessage` — post `"sofa-flashcards:request"` to the frame and it replies with `{type: "sofa-flashcards:data", bank, images, categories, categoryNames}`.

## Related

[sofa-license-flashcards](https://github.com/jBarrineau/sofa-license-flashcards) — the same question bank as a spaced-repetition flashcard deck.

## Disclaimer

Study aid only. The Station Safety Center briefing and PMO Pass & Registration are the authority on licensing requirements and Japanese traffic law.
