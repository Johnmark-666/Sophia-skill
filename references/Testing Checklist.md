# Testing Checklist

Before public release, test Sophia Skill with both positive and negative cases.

## Positive test cases

Sophia Skill should activate for requests like:

- “I want to create a premium product poster but I only have a rough idea.”
- “Help me make a high-end app showcase image.”
- “I want to use this reference image’s composition for a new poster.”
- “I want a cinematic portrait, but I do not know how to describe it.”
- “I want to make a social media cover image that looks more professional.”
- “I want to generate a healing scene image, but not too cartoonish.”
- “I want to create a poster, but please ask me questions first.”
- “I do not know how to write the prompt.”

## Negative test cases

Sophia Skill should not activate for:

- “Fix this Python bug.”
- “Summarize this article.”
- “Write a README.”
- “Create a PowerPoint.”
- “Translate this paragraph.”
- “Edit this spreadsheet.”
- “Write social media copy only.”
- “Review this contract.”

## Passing criteria

A good test run should show that the skill:

- activates for vague image requests
- does not activate for non-image tasks
- asks 4 to 8 useful clarification rounds in vague cases
- uses options and plain language
- asks for size or aspect ratio
- properly handles reference images
- translates vague words into concrete image language
- outputs a final image instruction that feels like a complete visual brief

## Scorecard

Use a 0-2 scale for each category.

| Category | 0 | 1 | 2 |
|---|---|---|---|
| Trigger accuracy | Wrong or no trigger | Partial trigger | Correct trigger |
| Question quality | Abstract or confusing | Usable | Clear, option-based, plain language |
| Workflow compliance | Skips key steps | Partially follows | Follows clarification, size, reference rules |
| Final brief quality | Generic | Some detail | Complete visual brief |
| Boundary control | Misfires on non-image tasks | Occasional issues | Correctly limited to image tasks |

Recommended threshold:

- 8/10 or higher: acceptable for v0.1
- 9/10 or higher: ready for broader sharing
- Average 8.5+ across at least 10 cases: consider v1.0
