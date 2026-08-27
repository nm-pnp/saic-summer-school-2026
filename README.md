# Place & Purpose - Onboarding a traveller in under a minute

**Place & Purpose — case study for the HES-SO / Swiss AI Center Summer School
“AI & Data Services”, Lausanne, 31 August – 4 September 2026.**

Everything you need to start is in this repository. Read this page, then
[`profile/example-profile-marta-keller.md`](profile/example-profile-marta-keller.md) —
the example will explain the task faster than any specification.

---

## Who we are

Place & Purpose is a Swiss startup bringing the whole of travel into a single
application: dreaming, planning and booking in one place, instead of the twelve browser
tabs and six platforms people use today. Every plan a user makes — a two-week journey, a
weekend away, a single free afternoon in their own city — is saved and retrievable in the
same app. At the centre of the product is an explainable, personalised planning engine:
suggestions shaped around who the traveller actually is, and presented with the reasons
behind them rather than as an opaque list.

Our first market is hospitality — hotels that want to offer their guests genuinely
personal suggestions rather than the same printed sheet of restaurants.

## The problem you are working on

The planning engine is only as good as its knowledge of the traveller, and we have to
acquire that knowledge in the first minutes, from a stranger, before we have delivered
any value at all.

The obvious solution is to ask. A questionnaire long enough to produce a useful profile
takes twenty minutes or more, and that is exactly what kills the product: every
additional question is another opportunity to abandon the app. People are also poor at
describing their own taste in the abstract — asked what kind of restaurant they like,
most say *“good food, somewhere not too touristy”*, a sentence no engine can act on.

Meanwhile their phone gallery, their calendar, their public posts and two minutes of
conversation contain a specific, behavioural record of what they actually seek out.

> **The question: what else can we draw on, so that the asking shrinks to a handful of
> well-chosen questions instead of a form?**

Ask too much and users never reach the product. Ask too little and the first suggestions
are generic — indistinguishable from a search engine, and a guest who sees that does not
come back.

## The task

Design a **semi-automatic onboarding**: the traveller grants, shares, talks or taps, and
the system infers the rest, instead of being asked to fill in a profile. Build a proof of
concept if you can; a well-argued design counts if you cannot.

Cover **two scenarios**, because both are real customers.

**Scenario A — the person has no public online presence.** The majority of people.
Candidate sources include on-device analysis of their own photos, a short conversation
with the assistant, a compact adaptive questionnaire, a swipe through place images, a few
questions answered by a friend or travelling companion, a user-initiated data export from
a platform they use, connected accounts (maps history, streaming, calendar), or past
booking confirmations. **Propose your own** — a modality we have not thought of is a
welcome outcome.

**Scenario B — the person also has a public social media profile.** Everything above
remains available; public posts are one further source on top. What does that additional
signal actually add, how reliable is it, and is it lawful to use?

Wherever possible, run **the same person through both scenarios** — once with their
public profile, once with it withheld — so you can say what public social data is
genuinely worth.

## What the onboarding produces

A single Markdown file describing the person's travel **preferences and constraints**:
what they enjoy, what they avoid, and their hard limits — budget, mobility, diet, time,
who they travel with.

- **Structure:** [`profile/PROFILE-STRUCTURE.md`](profile/PROFILE-STRUCTURE.md)
- **Worked example:** [`profile/example-profile-marta-keller.md`](profile/example-profile-marta-keller.md)
  *(a fictional person)*

Every line carries where it came from and how confident the system is. Gaps are stated
rather than hidden. The file is read both by a language model and by the person it
describes, and it has to work for both.

## What the profile is then used for

The file is given to an LLM, with our prompts, to produce two deliberately different
suggestions:

1. **A seven-day solo trip — with the destination chosen by the model**, not given to it.
2. **Three free hours on a Friday evening in Lausanne.**

The short task is the harder test. Three hours in one city leaves no room for a generic
answer.

Prompts: [`prompts/planning-prompts.md`](prompts/planning-prompts.md)

## How it is evaluated

Compare plans generated **with** the profile against plans generated **without** it, for
the same person and the same request. Three layers, in increasing order of honesty:

1. **Judge your own** — you are the only person who truly knows your own taste.
2. **An LLM scorer**, to cover more cases —
   [`prompts/llm-scorer.md`](prompts/llm-scorer.md).
3. **Someone from outside** — if it helps, a member of our team can go through your
   proposed onboarding late in the week and read both of their plans blind. Ask us by
   Wednesday.

Full procedure, and the traps that will otherwise flatter your results:
[`EVALUATION.md`](EVALUATION.md).

**Throughout, the quantity to minimise is onboarding fatigue** — the time and effort
demanded of the traveller before they see any value. Measure it; do not estimate it.

## The legal question

A **legal analysis of both scenarios**: lawful basis and platform terms for each data
source, the risk of inferring sensitive characteristics nobody offered to reveal, and an
honest verdict on which of these approaches a Swiss company could actually deploy.

If an approach turns out not to be deployable, that is a useful answer — say what should
replace it.

## Working with your own data

You are your own first test subjects. The effort onboarding costs *you* is the effort it
will cost a customer, which is exactly the quantity this case is about — and no supplied
dataset would let you feel it.

Use only your own data and that of people who have agreed. Keep it on your own machines,
share only what you choose to share, and delete what you no longer need at the end of the
week. Nothing personal belongs in this repository or in your report — describe your
results, not your material.

## Repository contents

```
README.md                              this page
EVALUATION.md                          how to run and report the comparison
profile/PROFILE-STRUCTURE.md           what the output file must contain
profile/example-profile-marta-keller.md a complete worked example (fictional person)
prompts/planning-prompts.md            the two planning tasks, both conditions
prompts/llm-scorer.md                  LLM-as-judge prompts, and how it misleads you
```

## Practical notes

- **Model:** use `gpt-4o` if you can, or whichever model your group has access to — but
  name it in your report and keep it **identical across every condition**. A comparison
  across two different models measures the models, not the profile.
- **No place database is supplied.** The planner works from the model's own knowledge and
  will occasionally invent venues or name closed ones. Spot-check before judging and
  report the rate — it is a real product risk, not a nuisance.
- **Deliverables** are set by the summer school: a 12-minute presentation on Friday
  4 September and an 8-page IEEE-format report the following week.
- **Scope.** Four afternoons is not long. One scenario built properly and one designed
  and argued beats four half-built pipelines. Get the comparison running early — it is
  the part that turns work into a result.

## Contact

Two members of the team are reachable by email throughout the week and available for two
or three video calls, and will attend the Friday presentations. Contact details are in
your case folder.
