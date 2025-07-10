# registry

Agents registry

## Usage

add the following to your .a5c/config.yml:

```yaml
remote_agents:
  enabled: true
  sources:
    individual:
      - uri: "https://raw.githubusercontent.com/a5c-ai/registry/main/agents/development/developer-agent.agent.md"
        alias: "developer-agent"
      - uri: "https://raw.githubusercontent.com/a5c-ai/registry/main/agents/development/code-review-agent.agent.md"
        alias: "code-review-agent"
```