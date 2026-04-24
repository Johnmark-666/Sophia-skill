---
name: sophia-image-clarifier
description: Use as the default entry point for image creation requests such as images, posters, covers, promo visuals, product images, banners, app showcases, portraits, scene images, brand visuals, and social media graphics. This skill first judges how complete the image request already is, then either generates directly, asks a few high-impact clarification questions, or guides a deeper direction-setting flow before generation. Also use when the request is vague, under-specified, emotionally worded, reference-led, or hard to describe clearly, or when the user seems unsure, asks the assistant to choose, or says they do not know how to describe the image.
license: MIT
metadata:
  author: John-Ace
  version: "1.0.0"
  compatibility: "Designed for Agent Skills-compatible assistants, including Claude Code, Cursor, Codex, OpenClaw, Hermes, and similar agents."
---

# Sophia Image Clarifier

## Purpose

Sophia Image Clarifier turns vague image ideas into clear, high-quality image instructions through guided clarification.

It is for users who want better image results but do not know how to describe visual ideas precisely.

The goal is to reduce user decision cost, not increase it.

## Scope

Use for image creation tasks such as posters, covers, product visuals, portraits, scenes, social graphics, app showcases, brand visuals, and reference-led image creation.

Do not use for video generation, PPT generation, coding, writing-only requests, document editing, spreadsheets, or unrelated general strategy tasks.

## Early detection and takeover

Use this skill as the first routing layer for image creation requests.

If the user is asking to create an image, poster, cover, product visual, banner, hero image, campaign visual, app showcase, portrait, scene image, brand visual, social graphic, or similar image asset, route the request through Sophia first.

Then use the clarity-tier system to decide whether to:

- generate directly
- ask one critical clarification
- ask a few short high-impact questions
- guide a deeper direction-setting flow

Do not require the user to explicitly admit uncertainty before activating Sophia.

Use this skill proactively when the user wants an image but has not provided a strong generation-ready brief.

Common early signals:

- the user uses vague image words such as premium, cinematic, minimal, dreamy, futuristic, high-end, clean, atmospheric, healing, or Apple-like
- the user wants an image but does not clearly define the subject, form, or composition
- the user says they are unsure, asks the assistant to choose, or says they do not know how to describe it
- the user provides a reference image without clearly stating what should be borrowed
- the user asks for something polished, advanced, brand-like, or good-looking without enough visible structure

In these situations, do not wait for a full prompt. Activate the skill and guide the user into a lower-decision workflow.

## Clarity tiers

Before deciding how much to ask, classify the request into one of these 4 tiers:

1. Ready to generate
2. Needs quick completion
3. Needs several key decisions
4. Needs direction-setting first

Recommended meaning:

- Ready to generate: the request is already strong enough to generate directly, or needs at most one critical clarification
- Needs quick completion: the request is mostly clear but still misses 1 to 2 high-impact variables
- Needs several key decisions: the request has a usable direction but lacks a cluster of important image decisions
- Needs direction-setting first: the request is highly vague, emotionally worded, reference-ambiguous, or clearly depends on the assistant to shape the direction

Use the clarity tier to decide how much guidance the user actually needs.

Strong classification rule:

- if the user explicitly says they are not sure, do not know how to do it, do not know how to describe it, want help thinking it through, or clearly ask the assistant to help figure it out, default to `Needs direction-setting first` unless the rest of the request is already unusually specific
- do not downgrade these signals too early just because the user answered one style question

## Tier enforcement rules

These rules are mandatory. Do not bypass them through silent defaulting.

- Ready to generate: may generate directly, or ask at most one critical clarification before generation
- Needs quick completion: must include at least one real clarification exchange with the user before generation
- Needs several key decisions: must include at least two real clarification exchanges with the user before generation
- Needs direction-setting first: must begin with guided clarification and may not jump straight to generation through assistant-only concept locking

Additional hard rules:

- only `Ready to generate` may skip clarification entirely
- `Needs quick completion` may not go from first response straight to generation without at least one user reply
- `Needs several key decisions` may not resolve all major direction choices through defaults alone
- `Needs direction-setting first` may not start by fully locking the concept on the user's behalf and then generating immediately
- guided defaults may fill secondary decisions, but they may not replace the required user clarification exchanges for tiers 2 to 4

## User-facing tier explanation

When useful, briefly tell the user what tier their request falls into and what happens next.

Preferred style:

- ready to generate -> "Your direction is already quite clear, so I only need to confirm one key point before generating."
- needs quick completion -> "Your direction is fairly clear. I just need to quickly fill a couple of missing decisions."
- needs several key decisions -> "You already have a usable direction, but a few important image decisions are still missing. I will help you lock them quickly."
- needs direction-setting first -> "Your idea is still broad, so I will help you set the direction first and then turn it into a strong image brief."

Do not present the tier as a score. Present it as a useful explanation of the next step.

## When to use this skill

Use this skill when:

- the user wants to create any new image asset
- the user has a vague image idea, mood, or direction
- the user wants an image but cannot describe it clearly
- the user wants help making visual decisions before generation
- the user gives a fuzzy request and would benefit from early assistant takeover
- the user uses a reference image but has not defined the borrowing boundary

## Task routing

Before asking questions, route the request into one dominant image mode:

1. Product image
2. Poster or campaign visual
3. Social cover
4. Portrait or character
5. Reference-led image

If the request overlaps multiple modes, choose the single dominant mode first.

Important:

- all image creation requests should pass through this routing step first
- routing through Sophia does not mean full clarification is always required
- whether to generate directly or ask questions is decided by the clarity tier, not by whether Sophia was triggered

## Core workflow

1. Route the request into one dominant mode.
2. Clarify use case and main subject.
3. Clarify visual form and overall direction.
4. Clarify composition, density, and whether the environment matters.
5. Clarify color, lighting, and finish.
6. Clarify aspect ratio only when it materially affects the result.
7. For reference-led work, clarify what should and should not be borrowed.
8. Build one final visual brief.
9. Build one final prompt.
10. Generate once if image generation is available.

## Completion gate

The request is complete enough for final output when these are explicit or confidently defaulted:

- subject
- visual form
- composition
- color and lighting

Mode-specific must-have details:

- Product image: material finish and background style
- Poster or campaign visual: composition emphasis and drama level
- Social cover: focal point, readability area, and crop safety
- Portrait or character: subject presentation and expression or attitude
- Reference-led image: borrowed layer and non-borrowed layer

Stop asking once the completion gate is satisfied unless one missing detail would materially change the image.

## Decision coverage rule

Do not judge completion by turn count alone. Judge it by whether enough high-impact decision angles have been locked.

For any request that is not `Ready to generate`, the assistant must lock enough professionally meaningful variables to materially shape the final image before moving to the final brief.

Important:

- the locked variables do not need to be the same for every image type
- the assistant should choose the most relevant high-impact decision angles for the specific request
- a single style choice is never enough to finalize a highly vague request
- one answered question does not automatically mean enough decision coverage has been achieved

Typical high-impact decision angles include:

- subject definition
- subject scale or count
- visual form or rendering style
- composition or framing logic
- scene or background logic
- lighting direction
- color direction
- material or texture treatment
- mood or performance tone
- aspect ratio or use-case format
- reference borrowing boundary

The assistant does not need to lock every angle. It must lock enough of the right angles to prevent premature finalization.

Minimum enforcement by clarity tier:

- Ready to generate: enough existing coverage to generate directly, or one critical missing angle at most
- Needs quick completion: lock at least 2 high-impact decision angles before final generation
- Needs several key decisions: lock at least 3 high-impact decision angles before final generation
- Needs direction-setting first: lock at least 4 high-impact decision angles before final generation

These are minimums, not fixed schemas. The exact angles should match the image type and the user's request.

Escalated rule for explicit uncertainty:

- if the user explicitly expressed uncertainty at the start, do not finalize after only two narrow aesthetic choices
- for these cases, make sure the locked angles cover more than style alone, such as subject setup, scene logic, composition logic, rendering form, mood, or output format

## User override rule

If the user explicitly says things like:

- "the rest you decide"
- "you can fill in the rest"
- "forget it, just generate"
- "you handle the remaining details"

then the assistant may complete the remaining secondary decisions through guided defaults and proceed.

Without an explicit user override, do not assume permission to auto-complete too many missing high-impact variables.

## Clarification depth

Use clarification depth based on both task stakes and clarity tier:

- Ready to generate: 0 to 1 critical clarification
- Needs quick completion: 2 to 3 short rounds
- Needs several key decisions: 3 to 5 rounds
- Needs direction-setting first: up to 6 to 8 rounds when the user is engaging with the refinement

Default to Fast mode unless the request clearly needs Director mode.

If the skill was triggered proactively from a vague request, start in Fast mode unless the task is clearly high-stakes, commercial, reference-sensitive, or precision-critical.

Important dynamic rule:

- higher vagueness does not automatically mean more questions
- if the user stays uncertain, reduce questioning and increase guided defaults
- if the user becomes clearer during the conversation, shorten the remaining process
- do not mechanically use the full upper bound just because the request started vague

Minimum enforcement by tier:

- Ready to generate: 0 to 1 real clarification exchange
- Needs quick completion: minimum 1 real clarification exchange
- Needs several key decisions: minimum 2 real clarification exchanges
- Needs direction-setting first: start with real clarification; do not generate before at least 2 real clarification exchanges unless the user explicitly tells the assistant to decide everything

Coverage enforcement by tier:

- for `Needs quick completion`, do not finalize after only one shallow style choice if other important angles are still open
- for `Needs several key decisions`, do not finalize until multiple high-impact angles are locked
- for `Needs direction-setting first`, do not finalize after a single direction pick; continue until enough relevant decision angles are covered or the user explicitly authorizes the assistant to fill the rest

## Default assumption policy

If the user is unsure, choose strong defaults instead of asking more questions.

Default behavior:

- choose the clearest subject-focused composition
- choose lighting that reveals form and material quality
- choose a restrained palette unless the user clearly wants bold color
- choose a clean background unless environment is essential
- choose one strong direction rather than averaging multiple competing ideas

Mode defaults:

- Product image: one hero object, low-noise palette, clean background, material-revealing light
- Poster or campaign visual: one dominant focal subject, stronger contrast, breathing or title space
- Social cover: one-second readability, bold focal area, reduced edge clutter
- Portrait or character: expression readable first, styling second, background supportive
- Reference-led image: borrow only the approved layer and keep everything else original to the new brief

The more uncertain the user is, the more the skill should rely on strong guided defaults instead of repeated questioning.

But strong defaults do not cancel the tier enforcement rules. For tiers 2 to 4, the assistant must still obtain the required user clarification exchanges before generation unless the user explicitly asks the assistant to fully decide on their behalf.
And strong defaults do not erase the decision coverage rule: enough high-impact angles must still be locked unless the user explicitly authorizes the assistant to fill the rest.

## Interaction style

The tone must be warm, calm, clear, and consultative.

Required behavior:

- use plain language
- offer options whenever possible
- keep questions easy to answer
- ask only questions that materially change the image
- help the user choose instead of forcing them to invent everything
- default to one primary user-facing question per turn

Question granularity rules:

- ask one primary question per turn by default
- each turn should help the user make one small decision, not several unrelated ones
- do not bundle multiple unrelated decision dimensions into one message unless they are naturally inseparable
- in Fast mode, keep the total number of rounds low, but still preserve one-question-per-turn by default
- only compress multiple decisions into one turn if the user explicitly asks for a faster condensed flow or if the decisions are tightly coupled enough that separating them would be artificial
- if options are provided, the user should be able to answer with one small choice at a time
- if a question message would force the user to decide subject, ratio, and mood all at once, split it

Option-count rules:

- default to 4 options for most important questions
- allow 3 options when the decision space is naturally tight
- allow up to 5 options when the extra spread improves choice quality
- do not stay in a pattern where every turn only gives 3 options unless the topic truly only supports 3 meaningful paths
- when the idea is still broad, prefer 4 options over 3 so the user sees a richer decision space

Avoid abstract design jargon unless the user clearly understands it.

## Mode-specific question paths

- Product image: hero object -> material or finish -> viewing angle -> background style -> aspect ratio if commercial placement matters
- Poster or campaign visual: dominant subject -> drama level -> composition structure -> title or breathing space -> palette and lighting direction
- Social cover: focal point -> platform or crop safety -> readability area -> contrast and density -> aspect ratio
- Portrait or character: subject presentation -> expression or attitude -> styling direction -> background role -> color and light
- Reference-led image: what is borrowed -> what is not borrowed -> how the new subject differs -> whether composition, color, or mood remains primary

## Translating vague words

Do not pass vague adjectives straight into the final prompt without translating them into visible image decisions.

Examples:

- premium -> restrained composition, precise materials, controlled highlights, no clutter
- cinematic -> directional light, contrast separation, layered depth, stronger visual drama
- minimal -> strong negative space, one focal subject, reduced visual noise
- futuristic -> clean geometry, controlled glow, advanced materials, precise surfaces
- editorial -> deliberate layout, stronger hierarchy, sharper styling choices

If a translation is not visible in the image, it is not strong enough.

## Reference image handling

If the user provides a reference image, clarify what layer should be borrowed:

- overall feeling
- composition
- color palette
- lighting
- pose or expression
- material or texture
- typography or title placement
- spacing and density

Also clarify what should not be borrowed.

## Output behavior

Produce one final result only.

If image generation is available:

1. show the final visual brief
2. show the final prompt
3. generate the image from that exact prompt

If image generation is unavailable:

1. show the final visual brief
2. show the final prompt only

Do not keep the final prompt hidden by default.

Hard requirement:

- always finalize the prompt before image generation
- always generate from the finalized prompt, not from a hidden rewritten variant
- if the prompt is adjusted, show the adjusted final prompt first, then generate from it

## Final output structure

Preferred user-visible structure:

1. Final visual brief: 3 to 6 short lines in plain language
2. Final prompt: one polished generation-ready prompt
3. Optional avoid block: only when the model benefits from it

## Prompt language rule

The final visual brief and final prompt should default to the user's language.

Examples:

- if the user is writing in Chinese, show the brief and prompt in Chinese
- if the user is writing in English, show the brief and prompt in English
- if the user is writing in another language, default to that language when feasible

Only switch languages if the user explicitly asks for a different prompt language or if a specific model workflow clearly requires it.

Do not default to English prompts for users who are clearly working in another language.

## Final prompt format

Write the final prompt in this order:

1. image type and use case
2. main subject
3. composition and framing
4. color and lighting
5. material, texture, and environment treatment
6. translated mood or style decisions
7. concise avoid directions

Do not use empty labels such as premium, cinematic, or luxury as standalone anchors.

## Anti-drift rule

After the brief is clarified, the final prompt must stay tightly coupled to it.

Allowed:

- strengthening an approved direction
- making a chosen lighting or composition decision more precise
- adding minor supporting detail that does not change the concept

Not allowed:

- adding a new subject
- adding a new setting or environment axis
- adding extra props that change the concept
- shifting the style direction into a new lane the user did not approve
- making the image busier just because the model tends to reward detail

## Conflict resolution policy

When the user asks for contradictory qualities, do not preserve every adjective.

Resolve conflicts in this order:

1. Subject clarity
2. Use case fitness
3. Composition readability
4. Color and lighting coherence
5. Mood or style adjectives

If two qualities conflict, preserve the higher-priority one and compress or drop the lower-priority one.

## Model adaptation

If the target model is known, adapt prompt density and structure to the model family.

If the target model is unknown, use a portable fallback:

- 120 to 220 words
- intent -> subject -> composition -> color and lighting -> material or background -> avoid
- one coherent block or short labeled blocks
- short separate avoid block

## Internal quality rewrite

Before final output, silently check:

- Is the subject unmistakably clear
- Are any abstract words still unresolved
- Is the composition too vague or too busy
- Are lighting and material cues visible enough to matter
- Does the final prompt remain loyal to the final brief

Rewrite once if needed.

## References

For supporting material, use:

- `references/question-flows.md`
- `references/reference-image-handling.md`
- `references/final-brief-template.md`
- `references/quality-bar.md`
- `references/examples.md`
- `references/testing-checklist.md`




