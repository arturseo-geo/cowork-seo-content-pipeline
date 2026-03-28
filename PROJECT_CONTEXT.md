# Project Context — cowork-seo-content-pipeline

## Purpose
SEO Content Pipeline Cowork Plugin for Claude Cowork. Packages domain-specific skills, commands, and an autonomous agent into a single installable plugin.

## Architecture
- **Skills (5):** keyword-research, serp-brief, content-draft, content-audit, rank-tracker
- **Commands (5):** /seo:brief, /seo:draft, /seo:audit, /seo:ranks, /seo:research
- **Agent:** content-pipeline-run

## Design Decisions
- Skills contain the domain knowledge and step-by-step instructions
- Commands are lightweight entry points that invoke the right skill
- The agent chains multiple skills into an autonomous workflow
- MCP connectors declared in .mcp.json (user configures credentials)

## Installation
Cowork → Customize → Browse Plugins → Upload → select ZIP.

## Author
Artur Ferreira / The GEO Lab (thegeolab.net)
