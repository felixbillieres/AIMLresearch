# 04 — Adversarial ML & LLM Security

> **Phase:** 2 | **Timeline:** June 2026 | **Status:** ⬜ Not Started

## Objective
Master adversarial ML techniques applied to LLMs. Understand prompt injection, jailbreaks, data poisoning, model evasion. Map existing pentest expertise onto the MITRE ATLAS framework. Contribute to open-source red teaming tools.

## Curriculum

### Frameworks to Master
- **OWASP Top 10 for LLM Applications** — https://genai.owasp.org
- **MITRE ATLAS** — https://atlas.mitre.org

### Tools to Learn & Contribute To
- **Garak** (NVIDIA) — LLM vulnerability scanner — https://github.com/NVIDIA/garak
- **PyRIT** (Microsoft) — AI red teaming framework — https://github.com/Azure/PyRIT

### Essential Papers (read in order)
1. "Jailbroken: How Does LLM Safety Training Fail?" (Wei et al.)
2. "Universal and Transferable Adversarial Attacks on Aligned LLMs" (Zou et al.)
3. "Not what you've signed up for" (Greshake et al.) — indirect prompt injection
4. "Ignore This Title and HackAPrompt" (Schulhoff et al.)
5. "Sleeper Agents" (Anthropic, 2024)

### Project: LLM Red Teaming Tool (→ folder 07)
Build a Python tool that automates adversarial testing of LLM APIs.

## Success Criteria
- [ ] Can map any LLM attack to OWASP LLM Top 10 and MITRE ATLAS
- [ ] Read and summarized all 5 essential papers
- [ ] Used Garak on at least 2 different LLMs
- [ ] Submitted at least 1 PR to Garak or PyRIT
- [ ] LLM Red Team Tool v1 published
