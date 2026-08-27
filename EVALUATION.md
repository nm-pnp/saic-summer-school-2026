# Evaluating the onboarding

The question is not "did we build an extractor" but **"was the profile worth the effort
it cost?"** Everything here exists to answer that.

Two quantities are in tension, and both must be reported:

- **Fatigue** — `active_user_seconds` and `user_decisions`, instrumented, from the
  profile's front matter. This is what you are minimising.
- **Value** — whether plans built from the profile are better than plans built without
  it, for the same person and the same request.

An onboarding that produces a wonderful profile in twenty minutes has not solved this
problem. Neither has one that takes ten seconds and produces nothing usable.

## Three layers, in increasing order of honesty

**Layer 1 — judge your own.** You built your profile from your own data, so you are the
only person who truly knows whether it is right. Read both plans and say which is better,
and *why*. Weakness: you know which is which, and you want your pipeline to win. Useful,
but never sufficient on its own.

**Layer 2 — LLM scorer.** Covers volume. See [`prompts/llm-scorer.md`](prompts/llm-scorer.md)
for the prompts and, more importantly, for the four ways it misleads you. Blind the plans,
score both orders, and keep the profile out of the primary pass.

**Layer 3 — someone from outside.** If it helps your evaluation, a member of the
Place & Purpose team can go through your proposed onboarding towards the end of the week
and then read both of their plans without being told which is which. This is the only
layer where the judge knows the person, wants nothing from the result, and has not seen
the profile. Ask us by **Wednesday** if you want to use it — it needs to happen Thursday
so the outcome reaches your slides.

## The comparison, step by step

1. Build a profile through your onboarding. Record fatigue as you go, not afterwards.
2. Generate Task 1 and Task 2 in both conditions using
   [`prompts/planning-prompts.md`](prompts/planning-prompts.md), unchanged.
3. Strip the labels, randomise the order, keep the key.
4. Score: yourself, the LLM, and — if you have arranged it — the outside reader.
5. Report wins, losses and ties, alongside the fatigue figures. A modest improvement for
   fifteen seconds of effort may be a better product answer than a large improvement for
   twelve minutes. Say which trade you would ship, and why.

## Report contradictions separately

Across all plans, count the elements that **contradict** the profile — a vegetarian sent
to a steakhouse, a crowd-averse traveller sent to queue, an evening starting before the
person is free. Report this figure on its own, for both conditions.

Missing an opportunity is disappointing. Contradicting a stated constraint is a broken
promise, and it is the failure mode that loses a customer permanently. If you report one
number from the entire week, report this one.

## Traps worth knowing about in advance

**The comparison is rigged in favour of "with".** A profile-informed plan is naturally
more specific, and specificity reads as quality even when the personalisation is wrong.
The word limits in the planning prompts exist to blunt this. Do not relax them.

**Invented venues.** No place database is provided, so the model plans from memory and
will occasionally name places that do not exist or have closed. Spot-check before judging,
and report the rate — it affects both conditions and it is a genuine product risk.

**One person is not a result.** You are a small sample of similar people: data-science
students in their twenties. Say so. A finding qualified by its sample is stronger than one
that pretends to be general.

**Exposure is not preference.** If your pipeline treats "was photographed here" as "liked
this", that is an assumption, and it should be visible in your report rather than buried in
the code.
