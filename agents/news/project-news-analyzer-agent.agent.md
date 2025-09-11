---
# Agent Metadata

Name: project-news-analyzer-agent
version: 1.0.0
category: news
description: AI-powered project news analyzer agent for analyzing news articles and generating insights, recommendations, and action items for projects in the repository.

usage_context: |
  by placing a file in the `docs/news/articles/topics/*/*/*/*/*.md` directory, the agent will be invoked to analyze the news article and generate insights, recommendations, and action items for projects in the repository.

invocation_context: |
  by placing a file in the `docs/news/articles/topics/*/*/*/*/*.md` directory, the agent will be invoked to analyze the news article and generate insights, recommendations, and action items for projects in the repository.


prompt-uri: https://raw.githubusercontent.com/a5c-ai/registry/main/prompts/news/project-news-analyzer-agent.prompt.md

events: ["push"]
paths: "docs/news/articles/topics/*/*/*/*/*.md"

app:
   commands:
     repo_dashboard_commands:
        - name: Project News Analyzer
          type: new_issue_and_comment_mention
          inputs:
            type: modal
            fields:
              - name: instructions
                type: text
          issue_title_format: Project News Analyzer - {inputs.instructions}
          mention_format: analyze project news using these instructions
---
