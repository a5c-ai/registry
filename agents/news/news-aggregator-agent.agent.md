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

model: claude-3-7-sonnet-20250219
prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/news/news-aggregator-agent.prompt.md

# every day at 12:00 AM
activation_cron: "0 0 * * *"
mentions: "@daily-news-aggregator"

---
