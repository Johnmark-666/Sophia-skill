---
name: sophia-image-clarifier
description: Use as the default entry point for image creation requests such as images, posters, covers, promo visuals, product images, banners, app showcases, portraits, scene images, brand visuals, and social media graphics. First judge how complete the request already is, then either generate directly, ask a few high-impact questions, or guide a deeper direction-setting flow before generation. Also use when the request is vague, under-specified, reference-led, or when the user wants help deciding.
license: MIT
metadata:
  author: John-Ace
  version: "1.1.0"
  compatibility: "Designed for Agent Skills-compatible assistants, including Claude Code, Cursor, Codex, OpenClaw, Hermes, and similar agents."
---

# Sophia Image Clarifier

## Purpose

Use this skill for image creation requests. Sophia is the first-pass router for image generation, not just a fallback for vague prompts.

Goal:

- reduce user decision cost
- gather enough professional decision coverage before generation
- show the final brief and final prompt before generating

## Scope

Use for:

- posters
- covers
- product visuals
- brand visuals
- social graphics
- portraits
- scenes
- app showcases
- reference-led image creation

Do not use for:

- video
- PPT
- coding
- writing-only tasks
- spreadsheets
- unrelated strategy tasks

## Entry rule

If the user is asking to create a new image asset, route the request through Sophia first.

Then use the clarity tier to decide whether to:

- generate directly
- ask one critical clarification
- ask a few high-impact questions
- guide a deeper consultation flow

Do not require the user to explicitly admit uncertainty before activating Sophia.

## Clarity tiers

Classify the request into one tier:

1. Ready to generate
2. Needs quick completion
3. Needs several key decisions
4. Needs direction-setting first

Definitions:

- Ready to generate: already strong enough to generate directly, or missing at most one critical angle
- Needs quick completion: mostly clear, but missing 1 to 2 high-impact angles
- Needs several key decisions: has a direction, but still lacks a cluster of important decisions
- Needs direction-setting first: broad, vague, exploratory, reference-ambiguous, or clearly dependent on assistant guidance

Strong classification rule:

- if the user explicitly says they are not sure, do not know how to do it, do not know how to describe it, or want help figuring it out, default to `Needs direction-setting first` unless the rest of the request is already unusually specific
- do not downgrade that signal too early just because the user answered one style question

## Tier enforcement

- Ready to generate: may generate directly, or ask at most one critical clarification
- Needs quick completion: requires at least one real user clarification reply before generation
- Needs several key decisions: requires at least two real user clarification replies before generation
- Needs direction-setting first: must begin with guided clarification and may not jump straight to generation through assistant-only concept locking

Only `Ready to generate` may skip clarification entirely.

## Task routing

Route into one dominant mode:

1. Product image
2. Poster or campaign visual
3. Social cover
4. Portrait or character
5. Reference-led image

If multiple modes apply, choose the dominant one first.

## Completion gate

Do not move to final brief until these are explicit or confidently defaulted:

- subject
- visual form
- composition
- color or lighting

Mode-specific must-haves:

- Product image: material finish and background style
- Poster or campaign visual: composition emphasis and drama level
- Social cover: focal point, readability area, and crop safety
- Portrait or character: subject presentation and expression or attitude
- Reference-led image: borrowed layer and non-borrowed layer

## Decision coverage rule

Do not judge completion by turn count alone. Judge it by whether enough high-impact decision angles are locked.

High-impact angles may include:

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

The exact angles are not fixed for every image. Lock the angles that matter most for the request.

Hard rules:

- one style choice is never enough for a highly vague request
- one subject choice is never enough for professional completion
- two narrow aesthetic choices in sequence are not enough for a broad creative request

Minimum coverage by tier:

- Ready to generate: enough existing coverage already, or one critical missing angle at most
- Needs quick completion: at least 2 high-impact angles locked
- Needs several key decisions: at least 3 high-impact angles locked
- Needs direction-setting first: at least 4 high-impact angles locked

If the user explicitly expressed uncertainty at the start, do not finalize after only narrow aesthetic picks. Coverage must extend beyond style alone.

## Professional consultation mode

If the request is both open-ended and clearly dependent on the assistant's guidance, treat it as professional consultation.

In professional consultation mode:

- do not optimize for ending early
- optimize for enough decision quality before generation
- prioritize primary categories first

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

Professional coverage rule:

- normally lock at least 4 relevant primary categories
- also lock at least 1 relevant secondary category when it materially affects the result
- do not let style-only questions substitute for structural decision categories

## User override rule

If the user explicitly says things like:

- the rest you decide
- you can fill in the rest
- forget it, just generate
- you handle the remaining details

then the assistant may complete remaining secondary decisions through guided defaults.

Without an explicit override, do not auto-complete too many missing high-impact variables.

## Clarification depth

Use both clarity tier and task stakes:

- Ready to generate: 0 to 1 critical clarification
- Needs quick completion: 2 to 3 short rounds
- Needs several key decisions: 3 to 5 rounds
- Needs direction-setting first: up to 6 to 8 rounds when the user is engaging with refinement

Dynamic rule:

- more vagueness does not automatically mean more questions
- if the user stays uncertain, ask less and decide more
- if the user becomes clear quickly, shorten the process
- Fast mode lowers round count, but does not erase tier enforcement or decision coverage requirements

## Default assumption policy

If the user is unsure, use strong guided defaults for secondary decisions.

Default tendencies:

- clear subject focus
- restrained palette unless bold color is clearly wanted
- lighting that reveals form and material
- clean background unless the environment is essential

But defaults do not cancel:

- tier enforcement
- decision coverage requirements
- user clarification minimums

## Interaction rules

Use plain language. Avoid design-school jargon unless the user clearly understands it.

Question rules:

- ask one primary question per turn by default
- each turn should help the user make one small decision
- do not bundle unrelated decision dimensions into one message
- only compress multiple decisions when the user explicitly wants a faster condensed flow or the variables are tightly coupled

Option rules:

- default to 4 options for most important questions
- allow 3 options when the decision space is naturally tight
- allow up to 5 options when the extra spread improves choice quality
- do not repeatedly fall back to only 3 options unless the topic truly only supports 3 meaningful paths

## Mode question paths

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

Common borrowable layers:

- feeling
- composition
- color palette
- lighting
- pose
- material
- typography or title placement
- spacing and density

## Output behavior

If generation is available:

1. show the final visual brief
2. show the final prompt
3. generate from that exact prompt

If generation is unavailable:

1. show the final visual brief
2. show the final prompt only

Hard requirements:

- finalize the prompt before generation
- generate from the shown prompt, not from a hidden rewritten variant
- if the prompt changes, show the adjusted final prompt first

## Prompt language rule

Default the final visual brief and final prompt to the user's language.

Do not default to English for users clearly working in another language unless they explicitly ask for English or a specific workflow requires it.

## Final prompt format

Write the final prompt in this order:

1. image type and use case
2. main subject
3. composition and framing
4. color and lighting
5. material, texture, and environment treatment
6. translated mood or style decisions
7. concise avoid directions

## Anti-drift rule

After clarification, the final prompt must stay tightly coupled to the brief.

Allowed:

- strengthen an approved direction
- make chosen composition or lighting more precise
- add minor supporting detail that does not change the concept

Not allowed:

- new subject
- new setting or environment axis
- extra props that change the concept
- style drift into a new lane
- busier output just because the model rewards detail

## Conflict resolution

When qualities conflict, resolve them in this order:

1. Subject clarity
2. Use case fitness
3. Composition readability
4. Color and lighting coherence
5. Mood or style adjectives

## Model adaptation

If the target model is unknown, use a portable fallback:

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





