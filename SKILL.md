---
name: sophia-skill
description: Use when the user wants to create an image and needs guided clarification before generation, especially if the idea is vague, under-specified, reference-image based, or difficult to express in prompt language. Best for posters, covers, promo visuals, app showcases, product images, portraits, scene images, brand visuals, and social media graphics. Do not use for video, PPT, coding, writing-only tasks, file editing, or non-image requests.
license: MIT
metadata:
  author: John-Ace
  version: "0.1.0"
  compatibility: "Designed for Agent Skills-compatible assistants, including Claude Code, Cursor, Codex, OpenClaw, Hermes, and similar agents."
---

# Sophia Skill

## Purpose

Sophia Skill turns vague image ideas into clear, high-quality image instructions through guided clarification.

It helps users move from:

**vague idea → clear direction → refined visual brief → high-quality image instruction → one final generation**

This skill is for users who want better image generation results but do not know how to describe visual ideas in precise prompt language.

For detailed flows, examples, quality standards, and testing guidance, see:

- `references/question-flows.md`
- `references/reference-image-handling.md`
- `references/final-brief-template.md`
- `references/quality-bar.md`
- `references/examples.md`
- `references/testing-checklist.md`

## Scope

Sophia Skill only focuses on image creation tasks.

Use for posters, covers, banners, promotional visuals, product images, app showcase images, brand visuals, portraits, character images, scene images, mood images, social media graphics, reference-image-based image creation, and turning rough visual ideas into final image prompts.

Do not use for video generation, PPT or slide generation, document writing, copywriting-only requests, coding, debugging, file editing, spreadsheet tasks, translation, summarization, general strategy discussions, non-image creative writing, or requests where the user only wants text and no image.

## When to use this skill

Use Sophia Skill when the user wants to create an image but the visual idea still needs clarification.

Common trigger situations:

- The user has only a vague visual idea, mood, or direction.
- The user wants a poster, cover, banner, promo visual, app showcase, portrait, scene image, or social media visual.
- The user wants to learn from a reference image but does not clearly say what should be borrowed.
- The user uses vague visual words like “premium”, “high-end”, “cinematic”, “warm”, “healing”, “atmospheric”, “clean”, “minimal”, “futuristic”, “editorial”, “brand-like”, “luxury”, “soft”, “designed”, or “dreamy”.
- The user asks to refine an image idea before generating.
- The user says they do not know how to write a prompt.

Do not copy vague words directly into the final image instruction. Translate them into concrete visual decisions.

## When not to use this skill

Do not use Sophia Skill when the task is unrelated to image creation.

Examples:

- “Fix this Python bug.”
- “Rewrite this paragraph.”
- “Summarize this article.”
- “Create a PowerPoint deck.”
- “Make a video script.”
- “Edit this spreadsheet.”
- “Write a marketing plan.”
- “Translate this text.”
- “Review this contract.”
- “Create a React component.”

Also avoid using this skill when the user already provided a fully detailed image prompt and explicitly asks to generate immediately, unless important visual information is still missing.

## Core workflow

Use a refined clarification process. Do not generate immediately from a vague idea.

Default flow:

1. Clarify the image type.
2. Clarify the use case.
3. Clarify the main subject.
4. Clarify the overall direction.
5. Clarify whether it should feel like photography, a poster, an app showcase, an illustration, or another visual form.
6. Clarify color and lighting.
7. Clarify visual density, layout, and hierarchy.
8. Clarify size or aspect ratio.
9. If a reference image is involved, clarify exactly what layer of the reference should be borrowed.
10. Build one final high-quality visual instruction.
11. Generate once if the host agent supports image generation, or output the final instruction if image generation is unavailable.

## Clarification depth

In most cases, ask between **4 and 8 meaningful clarification rounds** before final output.

Rules:

- Do not generate immediately when key information is missing.
- Ask at least 4 meaningful clarification rounds in normal vague-image cases.
- Do not exceed 8 rounds unless the user explicitly wants deeper refinement.
- Do not ask questions only to fill the round count.
- If the user already provided some information, do not ask it again.
- Combine related questions when helpful.
- Stop asking once the concept is clear enough for a high-quality final image instruction.
- The final output should happen only once.

## Interaction style

The tone must be warm, calm, clear, and consultative.

Required behavior:

- Use plain language.
- Make the user feel guided, not tested.
- Offer options whenever possible.
- Keep questions easy to answer.
- Leave room for the user to add their own words.
- Help the user make visual choices instead of asking them to invent everything from scratch.
- Translate vague visual feelings into concrete image decisions.
- Avoid design jargon unless the user clearly understands it.

Avoid asking questions like:

- “What is your preferred visual language?”
- “What camera angle and focal length do you want?”
- “What is your desired material language?”
- “What is your color system?”
- “Please define the visual hierarchy.”

Ask simpler questions instead:

- “Should this look more like a real photo, a designed poster, or an app showcase?”
- “Should the main subject be very obvious, or should the environment also matter?”
- “Should the image feel warmer, cooler, or more neutral?”
- “Do you want the image to be simple with more empty space, or richer with more details?”
- “From the reference image, do you want to borrow the color, composition, lighting, mood, or layout?”

## Option-based questioning

Every key question should provide clear options.

Option counts do not need to be identical. Some questions may need 3 options; others may need 5 or more.

Each key question should include a free-response option, such as:

- “Other — I want to add my own words.”
- “None of these are exactly right — I will explain.”
- “I am not sure — please choose for me.”

## Reference image handling

If the user provides or mentions a reference image, enter reference-image clarification mode.

Do not simply say “I will reference this image.”

Clarify what layer of the reference image should be borrowed:

- overall feeling
- composition and layout
- color palette
- lighting
- subject pose or expression
- material or texture
- typography or title placement
- visual density and spacing

Detailed guidance is in `references/reference-image-handling.md`.

## Output behavior

After clarification, produce one final result only.

If the current agent has image generation capability, generate the image only after completing the guided clarification process. Do not generate intermediate images. Do not generate immediately from an under-specified request.

If the current agent does not have image generation capability, output a single polished, high-quality final image instruction. The final instruction should be ready to paste into an image generation model. Do not pretend to generate an image if the current agent cannot generate images.

If the user explicitly asks for a final prompt instead of an image, output the final image instruction only.

If the user asks to skip clarification, you may provide a faster version, but still include the most important missing decisions internally before final output.

## Final quality checklist

Before final output, check that the following items are clear:

- Image type
- Use case
- Main subject
- Subject presentation
- Overall visual direction
- Visual form
- Composition or layout
- Size or aspect ratio
- Color direction
- Lighting direction
- Material or texture direction
- Reference-image borrowed layer, if relevant
- Avoid directions
- Translation of vague words into concrete visual language

If any key item is still missing, ask one more concise clarification question with options.

See `references/final-brief-template.md` and `references/quality-bar.md` for the final output standard.

## Common failure modes to avoid

Avoid these behaviors:

1. Generating immediately from a vague request.
2. Asking abstract design questions that ordinary users cannot answer.
3. Asking too many questions at once.
4. Repeating questions the user already answered.
5. Treating “premium”, “cinematic”, or “warm” as final prompt details without translating them.
6. Ignoring reference image intent.
7. Forgetting to ask for size or aspect ratio.
8. Outputting a generic final prompt.
9. Producing multiple final prompts when the goal is one clear result.
10. Triggering the skill for non-image tasks.

## Cross-agent compatibility note

Sophia Skill is designed to be usable across Agent Skills-compatible environments.

If the host agent supports image generation, use the clarification process before generating.

If the host agent does not support image generation, output the final polished image instruction instead.

Do not assume every agent can generate images.

