# Jekyll Bootstrap with LLM-Assisted Setup

**Built with [WonderChat AI](https://wonderchat.dev).**

<a href="https://apps.apple.com/us/app/wonderchat-ai/id6752497385" target="_blank">
  <img src="https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg" alt="Download on the App Store" height="50">
</a>

## Technical Summary

This entire blog was bootstrapped using WonderChat AI and GitHub Actions, all managed from a phone. The LLM-assisted setup process involved prompting the AI to create the site structure, configuration, and deployment workflows.

## Architecture

This repository contains a static site built with GitHub Actions workflows that were set up using WonderChat AI assistance.

### GitHub Actions Workflows
1. **jekyll_setup.yml** - Bootstraps the project with:
   - Ruby 3.2 setup
   - Project initialization
   - Custom configuration
   - Dependency management

2. **publish-pages.yml** - Deploys the site when tags are pushed with:
   - Ruby environment setup
   - Build process
   - GitHub Pages deployment

### Key Features
- Responsive design with mobile-optimized code blocks
- Custom CSS for rendering conversation logs (user prompts in blue, LLM responses in green)
- Automated dependency management

### Documentation
The main post (`_posts/2024-05-15-conversation-as-llm-instruction-template.markdown`) contains the complete conversation log with the LLM that was used to set up this entire project, making this a self-documenting bootstrap process.

## Usage

This repository serves as both:
1. A functional static site
2. A demonstration of AI-assisted development workflows
3. A template for others to replicate the LLM-assisted setup process

## How to Replicate

To replicate this setup process:
1. Create a new GitHub repository
2. Use the jekyll_setup.yml workflow to bootstrap your project
3. The LLM will handle the configuration and setup process
4. Use the publish-pages.yml workflow to deploy your site

## Technologies Used
- GitHub Actions
- Ruby/Bundler
- Markdown