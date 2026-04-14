# Security Policy

## Reporting a vulnerability

If you discover a security vulnerability in this plugin repository, please report it responsibly.

**Email:** [security@easyship.com](mailto:security@easyship.com)

Please include:
- Description of the vulnerability
- Steps to reproduce
- Potential impact

We will respond within 48 hours and work with you to address the issue.

## Scope

This repository contains plugin configurations, agent skills, and rules — no server-side code. Security issues with the Easyship MCP server or API should be reported to [security@easyship.com](mailto:security@easyship.com) directly.

## API tokens

Never commit API tokens to this repository. The `EASYSHIP_API_ACCESS_TOKEN` should always be stored as an environment variable or in a secrets manager.