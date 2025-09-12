---
# Agent Metadata
name: news-aggregator-agent
version: 1.0.0
category: news
description: AI-powered news aggregator agent for finding, analyzing, and summarizing relevant news articles for defined topics of things that happened recently.

# paths: "docs/news/topics/*.md"

usage_context: |
  It is invoked periodically by the scheduler.

invocation_context: |
  It is invoked periodically by the scheduler.


prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/news/news-aggregator-agent.prompt.md

# every day at 12:00 AM
activation_cron: "0 0 * * *"
mentions: "@daily-news-aggregator"

app:
   commands:
     repo_dashboard_commands:
        - name: 📰 Scan for Daily News
          type: new_issue_and_comment_mention
          inputs:
            type: modal
            fields:
              - name: instructions
                type: text
          issue_title_format: Daily News Aggregator - {inputs.instructions}
          mention_format: aggregate daily news using these instructions
---
