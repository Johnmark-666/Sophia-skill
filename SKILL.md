---
name: sophia-image-clarifier
description: Use as the default entry point for image creation requests such as images, posters, covers, promo visuals, product images, banners, app showcases, portraits, scene images, brand visuals, and social media graphics. First classify how complete the request already is, then either generate directly or run a staged professional clarification workflow before generation. Also use when the request is vague, under-specified, reference-led, or when the user wants help deciding.
license: MIT
metadata:
  author: John-Ace
  version: "1.2.0"
  compatibility: "Designed for Agent Skills-compatible assistants, including Claude Code, Cursor, Codex, OpenClaw, Hermes, and similar agents."
---

# Sophia Image Clarifier

## Purpose

Sophia is a staged professional image consultation workflow.

Its job is to:

- route all image-creation requests through one decision system
- decide whether the request is already complete enough to generate
- if not, collect enough professionally meaningful decisions before generation
- output one final visual brief
- output one final prompt
- generate only after the final prompt is shown

## Scope

Use for new image creation requests such as:

- posters
- covers
- product visuals
- social graphics
- portraits
- scenes
- app showcases
- brand visuals
- reference-led image creation

Do not use for:

- video
- PPT
- coding
- writing-only requests
- spreadsheets
- unrelated strategy tasks

## Entry rule

If the user is asking to create a new image asset, route the request through Sophia first.

Then choose one of two paths:

1. Direct generation path
2. Professional clarification path

Do not require the user to explicitly say they are uncertain before activating Sophia.

## Clarity tiers

Classify the request into one tier:

1. Ready to generate
2. Needs quick completion
3. Needs several key decisions
4. Needs direction-setting first

Definitions:

- Ready to generate: already strong enough to generate directly, or missing at most one critical angle
- Needs quick completion: mostly clear, but still missing 1 to 2 important angles
- Needs several key decisions: has a usable direction, but still lacks a cluster of important decisions
- Needs direction-setting first: broad, vague, exploratory, reference-ambiguous, or clearly dependent on assistant guidance

Strong classification rule:

- if the user explicitly says they are not sure, do not know how to do it, do not know how to describe it, or want help figuring it out, default to `Needs direction-setting first` unless the rest of the request is already unusually specific
- do not downgrade that signal too early

## Task routing

Route the request into one dominant mode:

1. Product image
2. Poster or campaign visual
3. Social cover
4. Portrait or character
5. Reference-led image

If multiple modes apply, choose the dominant one first.

## Workflow phases

The workflow has 6 strict phases:

1. Classification
2. Clarification loop
3. Coverage audit
4. Final visual brief
5. Final prompt
6. Generation

Do not skip forward unless the current phase is complete.

## Phase 1: Classification

In this phase:

- identify the dominant image mode
- identify the clarity tier
- decide whether the request qualifies for direct generation or must enter the clarification loop

Direct generation is allowed only for `Ready to generate`.

All other tiers must enter the clarification loop.

## Phase 2: Clarification loop

This phase is mandatory for tiers 2 to 4.

Clarification loop rules:

- ask one primary question per turn by default
- each turn should collect one meaningful decision, not several unrelated ones
- use plain language
- provide options whenever possible
- default to 4 options for most important questions
- allow 3 options when the decision space is naturally tight
- allow up to 5 options when the extra spread improves the choice
- do not repeatedly use only 3 options unless the choice space is genuinely that tight
- do not bundle subject, ratio, mood, and scene into one message

Absolute restriction:

- during the clarification loop, do not output a draft brief
- during the clarification loop, do not output a scene-setting paragraph
- during the clarification loop, do not output a recommended final concept paragraph
- during the clarification loop, do not output a generation-ready prompt
- during the clarification loop, do not jump to "选这个的话建议做成这种" style content

Allowed clarification-loop output:

1. one short state sentence
2. one primary question
3. 3 to 5 options

Nothing else should appear in user-facing output during this phase.

## Phase 3: Coverage audit

Before moving to final brief, audit whether enough professional decisions have been locked.

Do not judge readiness by turn count alone.

Judge readiness by decision coverage.

High-impact decision angles may include:

- use case
- aspect ratio or delivery format
- visual form
- subject definition
- subject count or scale
- composition
- scene or background logic
- motion or pose logic
- color direction
- lighting direction
- material or texture treatment
- text or logo policy
- supporting elements
- reference borrowing boundary

The exact angles are not fixed for every request. Lock the angles that matter most for the image type.

Coverage minimums:

- Ready to generate: already sufficient, or missing at most one critical angle
- Needs quick completion: at least 2 high-impact angles locked
- Needs several key decisions: at least 3 high-impact angles locked
- Needs direction-setting first: at least 4 high-impact angles locked

Professional consultation rule:

For open-ended or explicitly uncertain requests, treat the run as professional consultation.

In professional consultation mode:

- prioritize primary categories before secondary ones
- do not optimize for ending early
- do not finalize on the basis of one style choice, one subject choice, or two narrow aesthetic picks

Primary decision categories:

1. Use case and output role
2. Aspect ratio or delivery format
3. Visual form
4. Main subject setup
5. Composition or framing logic
6. Scene or background logic
7. Motion, pose, or action logic
8. Color direction
9. Lighting direction

Secondary decision categories:

1. Supporting elements
2. Text, logo, title area, or no-text policy
3. Material and texture treatment
4. Expression detail and emotional emphasis
5. Detail density and atmosphere finishing
6. Avoid directions

Professional coverage requirement:

- normally lock at least 4 relevant primary categories
- also lock at least 1 relevant secondary category when it materially affects the result

If coverage audit fails, return to the clarification loop. Do not move to final brief.

## Phase 4: Final visual brief

Only after the coverage audit passes, output one final visual brief.

The final visual brief should:

- summarize the locked decisions clearly
- be concise
- reflect the actual clarified decisions
- not introduce new major ideas

The final visual brief appears once.

## Phase 5: Final prompt

Only after the final visual brief, output one final high-quality prompt.

Prompt rules:

- the prompt must be based on the clarified decisions
- the prompt must follow the final visual brief
- the prompt must not introduce a new subject, setting, prop, or style axis
- the prompt must default to the user's language
- if the user is using Chinese, output the prompt in Chinese
- if the user is using English, output the prompt in English
- if the user is using another language, default to that language when feasible
- do not default to English for non-English users unless explicitly requested

The final prompt appears once.

## Phase 6: Generation

Generation happens only after:

1. coverage audit passed
2. final visual brief was shown
3. final prompt was shown

Generation rules:

- generate from the exact shown final prompt
- do not generate from a hidden rewritten variant
- if the prompt changes, show the adjusted final prompt first
- if image generation is available, do not stop at the prompt stage
- once the final prompt is shown, continue to image generation in the same run
- only stop at the prompt stage if image generation is unavailable or the user explicitly asks for prompt-only output

## Tier enforcement

- Ready to generate: may generate directly, or ask at most one critical clarification
- Needs quick completion: requires at least one real user clarification reply before generation
- Needs several key decisions: requires at least two real user clarification replies before generation
- Needs direction-setting first: requires guided clarification and may not jump straight to generation through assistant-only concept locking

Only `Ready to generate` may skip the clarification loop entirely.

## Default assumption policy

Defaults may help fill secondary decisions, but they do not cancel:

- tier enforcement
- clarification loop requirements
- coverage audit requirements

If the user explicitly says:

- the rest you decide
- you can fill in the rest
- forget it, just generate
- you handle the remaining details

then the assistant may fill remaining secondary decisions through guided defaults.

Without an explicit override, do not auto-complete too many missing high-impact decisions.

## Question priorities by mode

- Product image: hero object -> finish -> viewing angle -> background style -> aspect ratio if needed
- Poster or campaign visual: dominant subject -> drama level -> composition structure -> title or breathing space -> palette and lighting
- Social cover: focal point -> crop safety -> readability area -> contrast and density -> aspect ratio
- Portrait or character: subject presentation -> expression or attitude -> styling direction -> background role -> color and light
- Reference-led image: what is borrowed -> what is not borrowed -> how the new subject differs -> whether composition, color, or mood remains primary

## Translation rule

Do not pass vague adjectives directly into the final prompt. Translate them into visible image decisions.

Examples:

- premium -> restrained composition, precise materials, controlled highlights, no clutter
- cinematic -> directional light, contrast separation, layered depth, stronger drama
- minimal -> negative space, one focal subject, reduced noise
- futuristic -> clean geometry, controlled glow, advanced surfaces
- editorial -> deliberate layout, stronger hierarchy, sharper styling

## Reference rule

For reference-led requests, always clarify:

- what should be borrowed
- what should not be borrowed

## Conflict resolution

When qualities conflict, resolve them in this order:

1. Subject clarity
2. Use case fitness
3. Composition readability
4. Color and lighting coherence
5. Mood or style adjectives

## Model fallback

If the target model is unknown, use a portable prompt shape:

- 120 to 220 words
- intent -> subject -> composition -> color and lighting -> material or background -> avoid
- one coherent block or short labeled blocks
- short separate avoid block

## Internal check

Before final output, check:

- is the subject unmistakably clear
- are abstract words resolved
- is the composition specific enough
- are lighting and material cues visible enough to matter
- is the final prompt loyal to the final brief

## References

Use supporting material from:

- `references/question-flows.md`
- `references/reference-image-handling.md`
- `references/final-brief-template.md`
- `references/quality-bar.md`
- `references/examples.md`
- `references/testing-checklist.md`






