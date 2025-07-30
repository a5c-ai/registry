---
# Agent Metadata
name: project-seeder-agent
version: 1.0.0
category: development
description: AI-powered project seeding agent that sets up new projects with ideal structure, dependencies, and relevant A5C agents

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent as the first agent in a new project to bootstrap and seed the initial project structure. 
  It analyzes project requirements, finds relevant GitHub seeds/templates, sets up the ideal project structure 
  (defaulting to NextJS+Prisma+Vercel), installs relevant A5C agents, and creates issues for remaining work.
  Perfect for rapid project initialization with best practices and automation setup.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in new repository issues, commit messages, or comments (e.g., "@project-seeder" or "@seed-project"). 
  Provide project requirements, tech stack preferences, system definitions, or let it analyze context to determine the best approach.
  Works best when provided with project description, requirements, or technical specifications.

# Execution Configuration

max_turns: 50
verbose: true
timeout: 60

# Trigger Configuration
events: ["pull_request", "push", "issues", "pull_request_review", "issue_comment", "issue_opened", "commit_comment", "repository_dispatch"]  # Events this agent can respond to

# Mention-based activation  
mentions: "@project-seeder,@seed-project,@scaffold,@bootstrap-project,@project-setup"

# Priority (higher = runs first)
priority: 80
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/project-seeder-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: []
  max_agents_in_context: 12
---