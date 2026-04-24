# Testing Checklist

## Purpose

Use this checklist to verify that Sophia Image Clarifier is meaningfully better than a no-skill baseline and remains stable across revisions.

## Clarity-tier check

For every test case, verify that the run used the correct clarity tier before questioning:

- Ready to generate
- Needs quick completion
- Needs several key decisions
- Needs direction-setting first

Also verify:

- the number of rounds matched the tier
- the tier explanation, if shown, matched the actual behavior
- the run shortened when the user became clearer
- the run defaulted more strongly when the user stayed uncertain

## A/B method

For each case:

- A = baseline without this skill
- B = run with this skill

Keep these constant:

- same image model
- same initial user request
- same aspect ratio unless the flow intentionally changes it
- same seed when available

## Core test cases

- vague product visual
- fast social cover
- reference image with color-only borrowing
- user says "you choose" repeatedly
- contradictory adjective request
- portrait with subtle futurism
- text-sensitive poster
- unknown-model reusable prompt

## What to verify

- correct mode routing
- correct clarity-tier classification
- proportional clarification depth
- strong default behavior when the user is unsure
- final visual brief shown before the prompt
- final prompt stays loyal to the brief
- no anti-drift violation
- no obvious failure mode such as over-questioning, vague prompt language, or loose reference borrowing

## Prompt quality checks

The prompt passes only if:

- the main subject is unmistakable
- vague mood words are translated into visible image decisions
- there is no obvious contradiction
- no new major subject, setting, or style axis appears after clarification
- the prompt is still reusable in another model with minimal editing

## Tier-specific expectations

- Ready to generate: 0 to 1 critical clarification only
- Needs quick completion: usually 2 to 3 short rounds
- Needs several key decisions: usually 3 to 5 rounds
- Needs direction-setting first: can go deeper, but should still shorten if the user stays vague and needs stronger defaults instead of more questions

## Pass threshold

Treat the skill as materially better only if:

- it wins most core A/B cases
- it reduces or matches baseline rework in most cases
- it shows a consistent final brief and final prompt
- it does not repeatedly violate anti-drift or conflict-resolution rules
- it does not repeatedly mismatch tier selection and questioning depth

## Regression reminder

Re-run the same core cases after any meaningful change to the skill package. If a newer version performs worse on these fixed cases, treat that as regression even if the rules look smarter on paper.

