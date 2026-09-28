# Sprint 2

**Goal:** start Version 2, Deeper Analysis and Personal Use. This sprint covers the
deeper-analysis half.

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

Credibility signals are on `main` (PR #1). The other four are on `feature/v2-deeper-analysis`,
one commit per story, waiting for review.

## Not delivered

- The personal-use half of Version 2: bookmarks, sharing, recent searches. All three need browser
  storage or URL state, and we have not agreed what is stored or how a user clears it. The security
  review raised this as SEC-13.
- The rest of the Version 2 row: full-question search, URL input, keyword disambiguation, filters
  by date or publisher, subtopics, expanded reasoning, "last updated".

## Decisions to confirm

- Fact-versus-opinion is labelled per source, derived from the credibility source type, rather than
  per sentence. This keeps the prototype from inventing a judgement about an individual claim.
  Per-claim labelling would be a separate story.
- Conflicts between viewpoints are hand-written sample metadata and tagged "Sample data" in the UI.
  Only the shared-publisher detection is computed from the data.
- The reading-mode toggle keeps the name "All summaries"; only its layout changed.

## Technical debt

The AI-assisted review produced cards TD-01 to TD-06, DEF-01 to DEF-03, SEC-01 to SEC-15 and
FUT-01. Since then:

- DEF-02 is fixed: "Compare summaries side by side" now matches what the mode does.
- Everything else is still open, including TD-01 (one file, now 1318 lines), TD-02 (no automated
  tests or CI), TD-03 (keyboard focus lost when the page re-renders) and DEF-01 ("AI summary …
  Generated from the sources below" on hand-written text).
- New this sprint: below 820 px the sticky viewpoint rail overlaps the source list while scrolling.
  It behaves the same way in v1, so it is not a regression. One line of CSS fixes it; left out to
  keep the branch scoped.

## Notes

- Everything on the page is still sample data. No live retrieval, no model calls, no backend, no
  browser storage, no dependencies.
- Tested by hand in a browser against a local static server: all five sample topics and 11
  viewpoints, the no-results state, both reading modes, citation navigation, unavailable sources,
  the undated source, light and dark themes, 375 px and 1440 px widths, and sources and conflicts
  with missing or invalid data. No console errors.
