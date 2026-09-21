# TruthLens app (current: Version 1, Core Exploration)

Single-file, no-build prototype of the Version 1 row of the Team 2 feature board.
Open `index.html` in any browser. No server, no dependencies, no API keys.
Google Fonts load when online; the page falls back to system fonts offline.

Since v1.0 the living prototype also shows **Source credibility signals** on every source
(see below). The frozen copy in `releases/v1/` does not include them.

## What it covers

Every sticky in the Version 1 row maps to something you can click:

| Feature (board)            | User story (board)                                | Where it shows up in the prototype                                             |
|----------------------------|---------------------------------------------------|--------------------------------------------------------------------------------|
| Search for a Topic         | Search by keyword                                 | Search bar in the top bar, or any "Try a sample topic" chip                     |
| Search for a Topic         | See when no relevant results are found            | Search anything the sample data does not cover, e.g. `quantum cats`             |
| Read Viewpoint Summaries   | View short titles for distinct viewpoints         | Left rail, "Viewpoints"                                                         |
| Read Viewpoint Summaries   | Select a viewpoint to explore                     | Click a rail item; the right pane switches                                      |
| Compare Viewpoints         | Read a brief AI summary of each viewpoint         | "AI summary" block, or "All summaries" toggle to read them one after another    |
| Compare Viewpoints         | See source citations linked to each summary       | Numbered markers in the summary; click one to jump to that source               |
| Browse Viewpoint Sources   | Browse a source list for each viewpoint           | "Sources behind this viewpoint" under the summary                               |
| Browse Viewpoint Sources   | See when a source is unavailable                  | Red "Unavailable" badge and a plain-language reason in place of the link        |
| Browse Viewpoint Sources   | View source titles, publishers, and available dates | Title line and "Publisher · date" line; missing dates show "Date unavailable" |
| Read Original Content      | Open original source links                        | "Open original source" button (opens a placeholder page in a new tab)           |
| Read Original Content      | Read source excerpts behind each viewpoint        | "Read excerpt" disclosure on each source                                        |
| Review Uncertainty         | See when only one viewpoint is found              | Amber notice above the results                                                  |
| Review Uncertainty         | See when the available evidence is limited        | Amber notice above the results, plus a per-viewpoint note in the rail           |

Save and Share Findings has no Version 1 stories, so it is not in the prototype.

## Source credibility signals

Added after the v1.0 release. The frozen copy in `releases/v1/` does not include it.

Every source listed under "Sources behind this viewpoint" has a compact **Source credibility
signals** panel, placed after the publisher and date and before the excerpt and the
"Open original source" button. It shows four signals as text labels:

| Signal                   | What it describes                                            | Values                                                          |
|--------------------------|--------------------------------------------------------------|-----------------------------------------------------------------|
| Source type              | The kind of organization or outlet that published it         | e.g. Research organization, News organization, Opinion or commentary source |
| Recognition              | How widely known the publisher is                            | Established, Specialized, Limited, Not assessed                 |
| Subject-matter authority | How closely the topic matches the publisher's expertise      | High, Medium, Limited, Not assessed                             |
| Evidence transparency    | How clearly the source shows its data, methods or references | Strong, Moderate, Limited, Not assessed                         |

Under each panel, a **Why these signals?** disclosure shows a short rationale. A notice under the
"Sources behind this viewpoint" heading explains the signals, and **What the signals mean** expands
the definitions. Signals also appear on unavailable sources: they describe the source, not whether
its page can be opened.

What the signals are, and are not:

- Every signal and rationale is sample metadata written for this prototype about fictional
  publishers. Each panel is tagged "Sample data".
- They describe a source's profile. They do not prove that a source, or any claim in it, is
  accurate, and there is no overall or numerical score.
- No live source-verification service runs. Nothing checks real websites or publishers.
- Values are always shown as text, never by color alone. A missing credibility object, a missing
  field, or a label outside the lists above shows as "Not assessed"; a missing rationale says so
  instead of showing a blank.

## Demo script

Each sample topic is built to show a different state:

| Search                  | What it demonstrates                                                          |
|-------------------------|-------------------------------------------------------------------------------|
| `nuclear energy`        | Healthy case: 3 viewpoints, 8 sources, one missing date, one unavailable source |
| `remote work`           | 2 viewpoints, all sources available, no notices                               |
| `phone bans in schools` | Only one viewpoint AND limited evidence, both notices at once                  |
| `four-day week`         | 2 viewpoints but only 3 reachable sources, limited-evidence notice             |
| `AI hiring`             | 3 viewpoints, one of which rests on a single source                            |
| anything else           | No-results state with a way back                                              |

Keyword matching is loose: `nuclear`, `reactors`, `wfh`, `4-day`, `resume screening` all resolve.

Credibility signals vary on purpose: `remote work` includes a commentary source marked Limited for
recognition, authority and evidence transparency; the undated source under `nuclear energy` has
Limited evidence transparency; and the one source behind the transparency viewpoint in `AI hiring`
has recognition and authority marked Not assessed.

## What is mocked

- All topics, viewpoints, summaries, sources, publishers and excerpts are sample data
  written for this prototype. Publishers are fictional. Links go to `example.com`.
- "AI summary" text is hand-written. Nothing calls a model.
- Source credibility signals (source type, recognition, subject-matter authority, evidence
  transparency and rationale) are hand-written sample metadata. No service assesses or verifies
  sources.
- Search is a keyword match against the `keywords` list on each topic in `index.html`.
- The 350 ms "Searching sources…" delay is simulated.

## Adding a topic

Edit the `TOPICS` array at the top of the `<script>` block in `index.html`. Each topic has:

```
{ id, title, keywords: [...],
  viewpoints: [ { id, title, summary, sources: [ { title, publisher, date | null, url, available, excerpt,
    credibility: { sourceType, recognition, authority, evidenceTransparency, rationale } } ] } ] }
```

Write `[1]`, `[2]` in a summary to cite that viewpoint's first, second source.
Set `available: false` to demo an unreachable source, `date: null` to demo a missing date.
`credibility` is optional. Use only these labels (`SIGNAL_FIELDS` in the script): `recognition` is
Established, Specialized, Limited or Not assessed; `authority` is High, Medium, Limited or
Not assessed; `evidenceTransparency` is Strong, Moderate, Limited or Not assessed. `sourceType` and
`rationale` are short free text. Anything missing or unrecognized shows as "Not assessed", and an
unknown label is reported as a console warning when the page loads.
Notices trigger automatically: one viewpoint, or 3 or fewer reachable sources
(`LIMITED_EVIDENCE_MAX` in the script).

## Out of scope (Version 2 on the board)

Full-question search, URL input, keyword disambiguation, filters by date or publisher,
source counts per viewpoint, subtopics, expanded reasoning, fact-versus-opinion labeling,
"last updated", side-by-side compare, conflicting-evidence detection, bookmarks, sharing,
reporting, recent searches.
