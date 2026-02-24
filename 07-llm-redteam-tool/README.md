# 07 — LLM Red Teaming Tool 🏗️

> **Phase:** 2 | **Timeline:** June 2026 | **Status:** ⬜ Not Started
> **Type:** Portfolio Project

## Objective
Build a Python tool that automates adversarial testing of LLM APIs. Combines techniques from HTB path, OWASP LLM Top 10, and research papers into a practical red teaming framework.

## Features (Planned)
- Automated prompt injection testing (direct + indirect)
- Jailbreak attempt library with success tracking
- Output analysis for information leakage
- Results mapped to MITRE ATLAS techniques
- Clean CLI interface
- JSON/HTML reporting

## Tech Stack
- Python 3.11+
- Click (CLI)
- httpx (async API calls)
- Rich (terminal output)
- pytest (testing)

## Design Principles
- Clean, well-documented, production-grade Python (Anthropic standard)
- Modular architecture (easy to add new attack modules)
- Responsible use: includes disclosure guidelines

## Success Criteria
- [ ] Works against at least 3 different LLM APIs
- [ ] 10+ attack techniques implemented
- [ ] MITRE ATLAS mapping for each technique
- [ ] 80%+ test coverage
- [ ] Published on GitHub with proper README
