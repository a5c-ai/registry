# Work Log: Refine reviver-agent safe-close rule (issue #65)

## Plan
- Update `prompts/development/reviver-agent.prompt.md` safe-close guidance
- Replace generic close rule with explicit safe-close checks
- Add manual-close comment requirement

## Context
Issue: https://github.com/a5c-ai/registry/issues/65
File: `prompts/development/reviver-agent.prompt.md`

## Notes
- No `package.json` at repo root; skipping npm install

## Results
- Updated `prompts/development/reviver-agent.prompt.md` to add safe-close rules for issues linked to merged PRs.
- Opened draft PR: https://github.com/a5c-ai/registry/pull/71

## Next
- Mark PR ready for review and request @validator-agent after confirmation.
