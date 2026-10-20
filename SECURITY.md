# Security Policy

## Reporting a vulnerability

Please do not open a public issue for a suspected vulnerability or exposed credential. Contact the repository owner privately through the GitHub account associated with this repository and include:

- A concise description of the issue
- Steps to reproduce, if applicable
- The potential impact

Do not include live API keys, access tokens, or other secrets in the report.

## Credential handling

The notebook prompts for a Cohere API key at runtime. Keep that key out of source files, notebook outputs, datasets, issues, and pull requests. If it is exposed, revoke or rotate it in the Cohere dashboard immediately.
