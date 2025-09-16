---
# Agent Metadata
name: developer-agent
version: 1.0.0
category: development
description: AI-powered development assistant for coding tasks, debugging, and implementation guidance

# Usage Context (when to use this agent and what it does)
usage_context: |
  Use this agent for development assistance, coding tasks, debugging, and implementation guidance. It helps with code generation, 
  refactoring, bug fixing, feature implementation, and architectural decisions. Ideal for accelerating development workflow, 
  solving coding challenges, and providing technical guidance. Triggered by mentioning the agent in commit messages, PR descriptions, or comments.

# Invocation Context (how to invoke it and what context it needs)
invocation_context: |
  Invoke this agent by mentioning it in commit messages, PR descriptions, or comments (e.g., "@developer help implement this feature"). 
  Provide specific requirements, context, or code snippets for better assistance. Can help with debugging, code generation, 
  refactoring, performance optimization, and technical implementation questions.

# Execution Configuration

max_turns: 30
verbose: false
timeout: 30

# Trigger Configuration
events: ["pull_request", "push", "issues", "pull_request_review","issue_comment","issue_opened","commit_comment"]  # Events this agent can respond to (acts as filter)

# Mention-based activation  
mentions: "@developer,@dev-help,@ai-dev,@coding-help,@implement"

# Priority (higher = runs first)
priority: 70
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/development/developer-agent.prompt.md

# Agent Discovery Configuration
agent_discovery:
  enabled: true
  include_same_directory: true
  include_external_agents: []
  max_agents_in_context: 8
# app.a5c.ai definitions
app:   
   # these should appear in the app in the right context with the right intergrations (if the condition exists and it doesn't pass, the trigger element (button, etc) should not be visible)
   commands:
     # these translate to buttons in the activations section of the repo dashboard
     repo_dashboard_commands:
        - name: 🔨 Develop
          type: new_issue_and_comment_mention
          inputs:
            type: modal
            fields:
              - name: title
                type: text
          issue_title_format: {inputs.title}
          mention_format: develop this
        - name: 🔨 Fix
          type: new_issue_and_comment_mention
          inputs:
            type: modal
            fields:
              - name: title
                type: text
          issue_title_format: {inputs.title}
          mention_format: fix/change this
     # these translate to buttons in the batch command bar in the issues page (when selecting issues)
     issues_batch_commands:
        - name: 🔨 Develop
          type: comment_mention
          mention_format: do it
     # these translate to buttons in the batch command bar in the admin/issue details page (on the top, but if condition evaluation passes)
     issue_main_commands:
        - name: 🔨 Develop
          mention_format: do it
          type: comment_mention
          conditions:
            and:
              - "{{issue.state}} == 'open'"
     # these translate to buttons in the batch command bar in the admin/prs page (when selecting prs)            
     pr_batch_commands:
        - name: 🔨 Develop
          type: comment_mention
          mention_format: do it
     # these translate to buttons in the batch command bar in the admin/issue details page (on the top, but if condition evaluation passes)        
     pr_main_commands:
        - name: 🔨 Develop
          type: comment_mention
          mention_format: do it   
---
