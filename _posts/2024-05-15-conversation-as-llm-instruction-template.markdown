---
layout: posts
title: "Jekyll Setup Conversation as LLM Instruction Template"
date: 2024-05-15 10:00:00 +0000
categories: jekyll github-actions llm
---

Here's our conversation formatted as an LLM instruction template, along with a hypothetical LLM action and output.

**LLM Instruction Template:**

```markdown
You are an AI-powered software engineering assistant. Your primary goal is to help users safely and efficiently, adhering strictly to the following instructions and utilizing your available tools.

# User Request:
"Let’s setup a jekyll project. I need to bootstrap the initial project by using a dispatch GitHub action. The action should checkout the triggering repo, initialize a brand new jekyll project into top level directory of the repo. Add relevant patterns to gitignore then commit and push the relevant files into the triggering repo. The push needs content write permission. If possible I want the setup to use the minimal-mistakes-jekyll theme."

**Further Interactions:**
The user then requested several refinements and debugging steps:
1.  **Pin Ruby Version:** User requested pinning the Ruby version in the GitHub Action workflow.
2.  **Fix `bundle exec` for `jekyll new`:** User reported an error, leading to the removal of `bundle exec` when calling `jekyll new`.
3.  **Resolve Gemfile Conflict:** User reported a conflict with `jekyll-feed` gem, leading to the removal of `bundle add` command and instead listing plugins in `_config.yml`.
4.  **Update GitHub Pages Publish Action:** User requested updating the `publish-pages.yml` workflow to include Jekyll build steps before deployment.
5.  **Pull and List File Tree:** User requested pulling changes and displaying the file tree.

# Example LLM Action and Output (Initial Setup Phase):

## LLM Action:
- `default_api.create_directory`
- `default_api.create_file`
- `default_api.stage_changes`
- `default_api.commit_changes`
- `default_api.push_changes`
- `default_api.dispatch_github_workflow`

## LLM Output:
- `create_directory` response
- `create_file` response
- `stage_changes` response
- `commit_changes` response
- `push_changes` response
- `dispatch_github_workflow` response
```
