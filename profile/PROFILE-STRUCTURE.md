# The preference profile — required structure

Your onboarding produces **one Markdown file per person**. This document defines what
that file must contain. [`example-profile-marta-keller.md`](example-profile-marta-keller.md)
is a complete worked example — read it first; it will tell you more than this page does.

The file has two jobs at once. It is fed to a language model to generate travel
suggestions, so it must be unambiguous and self-contained. It is also read by the
person it describes, so it must be honest about where each statement came from and
how sure the system is.

## YAML front matter

```yaml
profile_id: <string>
generated_at: <ISO 8601 timestamp>
onboarding_scenario: A | B          # A = no public presence, B = public social profile also used
sources_used: [<list of the signals your pipeline actually consumed>]
active_user_seconds: <int>          # time the person spent attending to onboarding
user_decisions: <int>               # taps, answers, confirmations, corrections
language: <ISO 639-1>
```

`active_user_seconds` and `user_decisions` are the fatigue measurement. Instrument
them — do not estimate them afterwards. Waiting for a model to finish does not count;
granting a permission does.

## Required sections

| # | Section | What belongs in it |
|---|---|---|
| 1 | Hard constraints | Diet, mobility, budget, travelling party, time windows, languages. Things a suggestion may not violate. |
| 2 | What they are drawn to | Positive affinities, strongest evidence first. |
| 3 | What to avoid | Negative preferences. Weighted equally with §2 — a plan that includes something they hate fails, however good the rest is. |
| 4 | Style and pace | Planning style, novelty appetite, comfort priorities, tolerance for a full schedule. |
| 5 | Alone or with people | Not one setting. Someone may travel alone and socialise at home. |
| 6 | Hobbies and standing interests | What they do at home; the best predictor of what they seek out away. |
| 7 | Countries and regions visited | Repeatedly / once / never. Required — the 7-day task asks the model to choose a destination, and it cannot without this. |
| 8 | Places they return to at home | Repeated free choices are the strongest evidence available. |
| 9 | Evidence from specific places | Concrete reactions to named places: loved, fine, avoid. Worth more than abstract categories. |
| 10 | Not known | Explicit gaps. |
| 11 | Best next questions | The two or three unanswered questions worth the most. |

Sections may be empty if your pipeline genuinely found nothing — but say so. **Never
delete a section to hide a gap.**

## Four rules

**1. Every line carries its provenance.** Which signal produced it, and if it came from
speech, the phrase itself. Format: `— *source: conversation ("I gave up meat six years ago")*`.
A statement the system cannot explain is one it cannot show the user.

**2. Every line carries a confidence.** `high` · `medium` · `low`. Under-confidence is
cheap; over-confidence destroys trust. One observation is not `high`.

**3. `UNKNOWN` is a value.** Absence of evidence is never evidence of absence. Someone
with no beach photographs may hate beaches, or may simply not photograph them.

**4. Exposure is not preference.** A geotagged photograph proves the person *was there*.
It says very little about whether they *liked it* — business trips, obligations, one bad
meal. If your pipeline treats presence as liking, that is a modelling assumption; state
it in your report rather than leaving it implicit.

## Style

Write for a reader, not for a parser. Full sentences where a full sentence is clearer
than a keyword. The planning step is a language model — nuance survives, and
`food_pref: casual_dining` loses almost everything that made the person specific.
