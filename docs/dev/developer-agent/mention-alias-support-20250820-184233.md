Plan
- Align developer-agent mention triggers with docs instructing users to mention @developer-agent
- Update agents/development/developer-agent.agent.md mentions to include @developer-agent
- Open a PR and request @validator-agent review

Rationale
- Producer prompt instructs to mention @developer-agent in issues, but agent metadata did not include this alias
- Adding the alias ensures mention-based activation works as documented

Validation
- Static validation: ensure syntax remains valid and other mentions preserved
- Repository has no tests; change is metadata only
