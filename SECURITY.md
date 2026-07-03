# Security Policy

## Reporting a Vulnerability
If you discover a security issue in this repository (for example, a leaked
credential, an unsafe dependency, or unsafe handling of user input), please
open a GitHub Issue or contact the repository owner directly rather than
disclosing it publicly.

## Secrets & Credentials
This project does not commit API keys, tokens, or other secrets. Any required
credentials are supplied via environment variables — see `.env.example` for
the variable names expected, and copy it to `.env` locally (never commit `.env`).
