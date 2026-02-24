# 06 — Cyber RL Environment 🏗️

> **Phase:** 2 | **Timeline:** July 2026 | **Status:** ⬜ Not Started
> **Type:** Flagship Project

## Objective
Build a custom Gymnasium environment simulating cyber attack/defense scenarios, then train RL agents on it. This is THE differentiating project for the Anthropic Cybersecurity RL Research Engineer position.

## Concept
An RL environment where:
- **Offensive agent** learns to discover and exploit vulnerabilities in a simulated network
- **Defensive agent** learns to detect and respond to intrusions
- Configurable network topologies, vulnerability types, and defense mechanisms

## Architecture
```
cyber-rl-env/
├── envs/
│   ├── network_env.py      # Main Gymnasium environment
│   ├── network_config.py   # Network topology definitions
│   └── actions.py          # Action space (scan, exploit, pivot, etc.)
├── agents/
│   ├── attacker.py         # Offensive RL agent
│   └── defender.py         # Defensive RL agent
└── utils/
    ├── visualization.py    # Network state visualization
    └── metrics.py          # Evaluation metrics
```

## References
- CyberBattleSim (Microsoft): https://github.com/microsoft/CyberBattleSim
- NASim: https://github.com/jaromiru/NASimEmu
- Paper: "LLM Agents can Autonomously Hack Websites" (Fang et al.)

## Success Criteria
- [ ] Working Gymnasium environment with render
- [ ] At least 2 different network scenarios
- [ ] Agent trained with PPO achieving meaningful reward
- [ ] Documentation with architecture diagrams
- [ ] Blog post explaining the project
