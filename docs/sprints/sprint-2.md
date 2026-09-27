# Sprint 2

**Goal:** start Version 2, Deeper Analysis and Personal Use. This sprint covers the
deeper-analysis half and the search and filtering stories.

## Delivered

- Source credibility signals on every source: source type, recognition, subject-matter authority,
  evidence transparency, and a "Why these signals?" rationale
- Source counts per viewpoint in the viewpoint rail
- Fact-versus-opinion labeling: every source is labelled Research, Reporting or Opinion, and each
  viewpoint shows the mix of material behind it
- Conflicting-evidence detection: the points two viewpoints disagree on, shown under a summary and
  collected above the compare columns, plus publishers cited under more than one viewpoint
- Side-by-side compare: "All summaries" lays the viewpoints out in columns and stacks them on
  narrow screens
- Full-question search: a typed question such as "should schools ban phones?" now reaches its
  topic, and a short query like "AI" resolves instead of returning nothing
- Keyword disambiguation: when two topics match about equally, the page asks which one was meant
  instead of quietly picking one
- Filters by publisher or date above the source list, with citation numbers unchanged and a
  citation to a filtered-out source clearing the filters

Credibility signals are on `main` (PR #1). The four deeper-analysis stories are on
`feature/v2-deeper-analysis`; the three search stories are on `feature/v2-better-search`, which
builds on that branch. One commit per story, both waiting for review.

## Not delivered

- The personal-use half of Version 2: bookmarks, sharing, recent searches. All three need browser
  storage or URL state, and we have not agreed what is stored or how a user clears it. The security
  review raised this as SEC-13.
- The rest of the Version 2 row: URL input, subtopics, expanded reasoning, "last updated".

## Decisions to confirm

- Fact-versus-opinion is labelled per source, derived from the credibility source type, rather than
  per sentence. This keeps the prototype from inventing a judgement about an individual claim.
  Per-claim labelling would be a separate story.
- Conflicts between viewpoints are hand-written sample metadata and tagged "Sample data" in the UI.
  Only the shared-publisher detection is computed from the data.
- The reading-mode toggle keeps the name "All summaries"; only its layout changed.
- The topic chooser appears when the runner-up topic scores at least half as well as the winner.
  That threshold is a guess; `work` and `phones at work` are the sample queries that trigger it.

## Technical debt

The AI-assisted review produced cards TD-01 to TD-06, DEF-01 to DEF-03, SEC-01 to SEC-15 and
FUT-01. Since then:

- DEF-02 is fixed: "Compare summaries side by side" now matches what the mode does.
- FUT-01 is partly addressed: each topic's normalized keywords and search tokens are worked out
  once and cached, instead of on every keystroke-driven search.
- TD-03 is unchanged in general, but the new filter menus put focus back where it was after the
  pane re-renders, so changing a filter does not drop the keyboard user.
- Everything else is still open, including TD-01 (one file, now 1493 lines), TD-02 (no automated
  tests or CI), TD-03 elsewhere in the page, and DEF-01 ("AI summary … Generated from the sources
  below" on hand-written text).
- New this sprint: below 820 px the sticky viewpoint rail overlaps the source list while scrolling.
  It behaves the same way in v1, so it is not a regression. One line of CSS fixes it; left out to
  keep the branch scoped.

## Notes

- Everything on the page is still sample data. No live retrieval, no model calls, no backend, no
  browser storage, no dependencies.
- Tested by hand in a browser against a local static server: all five sample topics and 11
  viewpoints, the no-results state, the topic chooser, both reading modes, citation navigation
  (including to a filtered-out source), publisher and date filters, unavailable sources, the
  undated source, light and dark themes, 375 px and 1440 px widths, and sources and conflicts with
  missing or invalid data. No console errors.
