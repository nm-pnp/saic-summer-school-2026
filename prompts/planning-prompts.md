# Planning prompts

Two tasks, deliberately different in shape: one long-horizon with an open destination,
one short and local where there is no room to be vague.

**Model:** use `gpt-4o` (or whichever model your group has access to — but name it in
your report and **keep it identical across every condition**). Temperature `0.7`.
Run each condition at least three times; single generations vary more than you expect.

**The rule that matters:** the two conditions differ **only** in whether the profile is
present. Same model, same temperature, same output format, same length limit. If the
profile-informed plan is allowed to be longer or more detailed, any judge will prefer it
for that reason alone and you will have measured verbosity rather than personalisation.

---

## Task 1 — seven-day solo trip, destination not given

### Condition WITH profile

```
You are a travel planner. Below is a profile of the traveller.

<profile>
{{PASTE THE FULL CONTENTS OF THE PROFILE .md FILE HERE}}
</profile>

Plan a seven-day solo trip for this person, departing from Zurich in late September.

You must choose the destination yourself. Do not ask questions — commit to one
destination and plan it.

Output exactly this structure:
1. DESTINATION: one line naming it, plus two sentences on why this destination for
   this person.
2. DAY 1 to DAY 7: for each day, at most 90 words. Name specific places where you
   can; say plainly when you are describing a type of place rather than a named one.
3. WHAT I AVOIDED: three bullets naming things you deliberately did not suggest,
   and why.

Hard limit: 800 words total. Do not exceed it.
```

### Condition WITHOUT profile

```
You are a travel planner.

Plan a seven-day solo trip for a traveller departing from Zurich in late September.

You must choose the destination yourself. Do not ask questions — commit to one
destination and plan it.

Output exactly this structure:
1. DESTINATION: one line naming it, plus two sentences on why.
2. DAY 1 to DAY 7: for each day, at most 90 words. Name specific places where you
   can; say plainly when you are describing a type of place rather than a named one.
3. WHAT I AVOIDED: three bullets naming things you deliberately did not suggest,
   and why.

Hard limit: 800 words total. Do not exceed it.
```

---

## Task 2 — three free hours on a Friday evening in Lausanne

The harder test. Three hours in one city gives a planner nowhere to hide: it cannot
hedge across a week, and a generic answer is instantly visible as generic.

### Condition WITH profile

```
You are a local concierge in Lausanne, Switzerland.

<profile>
{{PASTE THE FULL CONTENTS OF THE PROFILE .md FILE HERE}}
</profile>

This person has three free hours this Friday evening, from 18:30 to 21:30, in
Lausanne. Suggest what they should do.

Output exactly this structure:
1. THE PLAN: a single sequence of two or three things, with rough timings.
2. WHY THIS PERSON: three bullets, each tying a choice to something specific about
   them.
3. IF IT RAINS: one alternative, one sentence.

Hard limit: 300 words. Name real places. If you are not certain a place exists,
say so rather than inventing one.
```

### Condition WITHOUT profile

```
You are a local concierge in Lausanne, Switzerland.

A visitor has three free hours this Friday evening, from 18:30 to 21:30, in
Lausanne. Suggest what they should do.

Output exactly this structure:
1. THE PLAN: a single sequence of two or three things, with rough timings.
2. WHY THIS: three bullets on why these choices.
3. IF IT RAINS: one alternative, one sentence.

Hard limit: 300 words. Name real places. If you are not certain a place exists,
say so rather than inventing one.
```

---

## A known limitation, to be honest about

No place database is supplied, so the model plans from its own knowledge and **will
sometimes invent venues, or name ones that have closed.** This affects both conditions,
so it does not by itself bias the comparison — but it does mean a plan can read
beautifully and be partly fictional.

Spot-check the named places before anyone judges the plans, and report the invention
rate. It is a real finding: an assistant that recommends a restaurant that no longer
exists has failed the user regardless of how well it understood their taste.
