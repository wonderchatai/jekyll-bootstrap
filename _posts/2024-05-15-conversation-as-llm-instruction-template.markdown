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
```python
# Initial directory creation for GitHub workflows
print(default_api.create_directory(path=".github/workflows"))

# Creation of the jekyll_setup.yml workflow
print(default_api.create_file(content="""
name: Jekyll Setup

on:
  workflow_dispatch:

permissions:
  contents: write

jobs:
  setup-jekyll:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v4

    - name: Set up Ruby
      uses: ruby/setup-ruby@v1
      with:
        ruby-version: '3.x'
        bundler-cache: true

    - name: Install Jekyll and Bundler
      run: |
        gem install jekyll bundler

    - name: Initialize Jekyll project with minimal-mistakes-jekyll theme
      run: |
        bundle exec jekyll new . --force --skip-bundle
        echo "theme: minimal-mistakes-jekyll" >> _config.yml
        echo "remote_theme: "mmistakes/minimal-mistakes@4.24.0"" >> _config.yml
        bundle add jekyll-feed jekyll-include-cache jekyll-paginate jekyll-sitemap jekyll-archives jekyll-redirect-from jekyll-seo-tag jekyll-toc jemoji kramdown-parser-gfm rouge --group "jekyll_plugins"
        bundle install
      working-directory: ${{ github.workspace }}

    - name: Add relevant patterns to .gitignore
      run: |
        echo "_site/" >> .gitignore
        echo ".jekyll-cache/" >> .gitignore
        echo ".sass-cache/" >> .gitignore
        echo "vendor/" >> .gitignore
        echo ".bundle/" >> .gitignore
        echo "*.gem" >> .gitignore
        echo "*.log" >> .gitignore
        echo ".DS_Store" >> .gitignore
        echo "Gemfile.lock" >> .gitignore
        echo "node_modules/" >> .gitignore
        echo ".vscode/" >> .gitignore
        echo ".idea/" >> .gitignore

    - name: Git config
      run: |
        git config user.name "github-actions[bot]"
        git config user.email "github-actions[bot]@users.noreply.github.com"

    - name: Stage changes
      run: git add .

    - name: Commit and push changes
      run: |
        git commit -m "feat: Initial Jekyll project setup with minimal-mistakes-jekyll theme"
        git push
""", filename=".github/workflows/jekyll_setup.yml"))

# Staging, committing, pushing, and dispatching the workflow
print(default_api.stage_changes())
print(default_api.commit_changes(message="feat: Add GitHub Actions workflow for Jekyll setup"))
print(default_api.push_changes())
print(default_api.dispatch_github_workflow(workflow_id="jekyll_setup.yml"))
```

## LLM Output:
```text
{"create_directory_response": {"results": ["{\"funcname\":\"create_directory\",\"message\":\"Directory '.github\\/workflows' created successfully.\",\"status\":\"success\"}"]}}
{"create_file_response": {"results": ["{\"status\":\"success\",\"funcname\":\"create_file\",\"path\":\".github\\/workflows\\/jekyll_setup.yml\",\"message\":\"File `.github\\/workflows\\/jekyll_setup.yml` created successfully.\"}"]}}
{"stage_changes_response": {"results": ["{\"status\":\"success\",\"funcname\":\"stage_changes\",\"message\":\"All changes have been staged.\"}"]}}
{"commit_changes_response": {"results": ["{\"funcname\":\"commit_changes\",\"message\":\"Changes committed successfully.\",\"status\":\"success\"}"]}}
{"push_changes_response": {"results": ["{\"remote_url\":\"https:\\/\\/github.com\\/wonderchatai\\/jekyll-bootstrap.git\",\"status\":\"success\",\"message\":\"Changes pushed successfully to origin.\",\"funcname\":\"push_changes\"}"]}}
{"dispatch_github_workflow_response": {"results": ["{\"status\":\"success\",\"funcname\":\"dispatch_github_workflow\",\"message\":\"Successfully dispatched GitHub workflow 'jekyll_setup.yml' on ref 'main'.\"}"]}}
I've set up the Jekyll project by dispatching a GitHub Actions workflow. You can monitor its progress in the 'Actions' tab of your repository.
```
