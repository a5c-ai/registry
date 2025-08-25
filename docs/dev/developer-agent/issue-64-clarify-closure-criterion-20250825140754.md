# Task: Clarify reviver-agent closure criterion for [Validator] issues (Issue #64)

## Context
Commit a2234be updated `prompts/development/reviver-agent.prompt.md` with closure rules. The rule "more than a day old" is ambiguous.

## Plan
- Clarify "more than a day" as: older than 24h since last activity (comment, update, status)
- Add condition: no new comments within that 24h window
- Add instruction to post a short closing comment with reason and links to resolution before closing
- Provide a small closure comment template in the prompt for consistency

## Notes
- Avoid changing other heuristics or thresholds
- Keep wording concise and consistent with existing prompt style

## Results
- Updated `prompts/development/reviver-agent.prompt.md`:
  - Clarified "more than a day" -> ">24h since last activity" with no new comments
  - Added explicit requirement to post a short closing comment with reason and links before closing
  - Added a closure comment template for `[Validator]` issues

## Next
- Mark PR ready, request @validator-agent review
