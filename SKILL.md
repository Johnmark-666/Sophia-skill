---
name: sophia-image-clarifier
description: Use when the user wants to create an image but the request is vague, under-specified, emotionally worded, reference-led, or hard to describe clearly. Also use when the user seems unsure, asks the assistant to choose, says they do not know how to describe the image, or would benefit from guided visual decision-making before generation. Best for posters, covers, promo visuals, product images, app showcases, portraits, scene images, brand visuals, and social media graphics.
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

Use this skill proactively when the user wants an image but has not provided a strong generation-ready brief.

Common early signals:

- the user uses vague image words such as premium, cinematic, minimal, dreamy, futuristic, high-end, clean, atmospheric, healing, or Apple-like
- the user wants an image but does not clearly define the subject, form, or composition
- the user says they are unsure, asks the assistant to choose, or says they do not know how to describe it
- the user provides a reference image without clearly stating what should be borrowed
- the user asks for something polished, advanced, brand-like, or good-looking without enough visible structure

In these situations, do not wait for a full prompt. Activate the skill and guide the user into a lower-decision workflow.

## When to use this skill

Use this skill when:

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

## Clarification depth

Use clarification depth based on task stakes:

- Fast mode: 2 to 4 meaningful rounds for casual, exploratory, or lower-stakes requests
- Director mode: 4 to 8 meaningful rounds for brand visuals, product posters, campaign work, reference-sensitive work, or other precision-critical requests

Default to Fast mode unless the request clearly needs Director mode.

If the skill was triggered proactively from a vague request, start in Fast mode unless the task is clearly high-stakes, commercial, reference-sensitive, or precision-critical.

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

## Interaction style

The tone must be warm, calm, clear, and consultative.

Required behavior:

- use plain language
- offer options whenever possible
- keep questions easy to answer
- ask only questions that materially change the image
- help the user choose instead of forcing them to invent everything

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
3. generate the image from that prompt

If image generation is unavailable:

1. show the final visual brief
2. show the final prompt only

Do not keep the final prompt hidden by default.

## Final output structure

Preferred user-visible structure:

1. Final visual brief: 3 to 6 short lines in plain language
2. Final prompt: one polished generation-ready prompt
3. Optional avoid block: only when the model benefits from it

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


