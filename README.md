# Sophia Image Clarifier

Sophia Image Clarifier is a skill for users who want an image but cannot yet describe it clearly.

It is not mainly a prompt-writing tool. It is a guided visual decision workflow that:

- detects vague or under-specified image requests early
- reduces user decision cost through short guided clarification
- turns fuzzy aesthetic language into visible image decisions
- shows a readable final visual brief before generation
- outputs a generation-ready final prompt that stays faithful to the clarified brief

## Best use cases

- posters and campaign visuals
- product hero images
- social covers and thumbnails
- portraits and character images
- reference-led image creation
- brand visuals and promo images

## How it works

1. Detect that the image request is vague, emotional, or under-specified.
2. Route the request into one dominant mode.
3. Ask only the questions that materially change the image.
4. Default aggressively when the user is unsure.
5. Present a short final visual brief.
6. Present one strong final prompt.
7. Generate once if image generation is available.

## Package structure

- `SKILL.md`: trigger logic, workflow, rules, and output requirements
- `SYSTEM_PROMPT.txt`: condensed execution behavior for skill-aligned agents
- `references/question-flows.md`: mode-specific clarification flows
- `references/reference-image-handling.md`: borrowing-boundary rules for reference-led work
- `references/final-brief-template.md`: final brief and prompt structure
- `references/quality-bar.md`: what good looks like
- `references/examples.md`: mode-specific examples and dialogue anchors
- `references/testing-checklist.md`: A/B checks, regression checks, and pass thresholds

## Design goal

The goal is not to ask more questions. The goal is to help a user get to a stronger image with less friction and less guesswork.

