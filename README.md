# Regulator Watch

Internal reference for AI Notary. One living page tracking where financial
regulators require someone to **prove what an automated system did or decided**.

## What this is

`index.html` is a single page, updated in place — not a series of reports.
It holds the current position across six jurisdiction blocks (EU, UK, US,
South Africa, Australia, global bodies), a deep dive on South Africa, and an
update log with one line per weekly sweep.

Superseded items are removed rather than archived. **Git history is the archive**
— every Monday's state is a commit, so you can diff week over week and show what
the page said on any past date.

## How it updates

A scheduled task runs every Monday at 07:00 Europe/Berlin, sweeps the
twenty-four regulators from primary sources only, and edits `index.html` in place
between these markers:

| Marker pair | Region |
|---|---|
| `WATCH:STAMP_START` / `WATCH:STAMP_END` | last-swept line |
| `WATCH:STATE_START` / `WATCH:STATE_END` | six jurisdiction blocks |
| `WATCH:LOG_START` / `WATCH:LOG_END` | update log (prepend only) |

Leave those comments in the file. Everything else is hand-maintained.

Then commit and push — Netlify deploys on push.

```
git add -A && git commit -m "Weekly sweep: <date>" && git push
```

## Rules the sweep follows

Priority order, deliberately backwards from most monitoring — a decision not
yet made is the most useful signal:

1. Open consultations and discussion papers
2. Published consultation responses
3. Enforcement actions involving automated decisions
4. Speeches by senior supervisors
5. Final guidance, circulars and rules

Primary sources only: the regulator's own site, never a vendor blog or law-firm
summary. No speculation about what a regulator might do. If a document can't be
opened, that is recorded as a coverage gap rather than summarised second-hand.

## Standing content — do not delete

- The South Africa deep dive (`id="south-africa"`), built from the FSCA–PA
  November 2025 report, its databook and the survey instrument.
- POPIA s71 and FAIS automated-advice entries — live legal obligations, not news.

## Structure

```
index.html        the page
assets/style.css  the only stylesheet
netlify.toml      publish config (no build step)
```
