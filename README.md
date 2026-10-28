# VehicleGPT

**Teliport S4 · Case Study 5 (TBU) — Natural Language Vehicle Information using On-Device SLM/LLM**

An on-device language assistant for software-defined vehicles. It reads CAN/CAN-FD, SOME/IP, Android VHAL, QNX logs, ADAS and diagnostic data, keeps weeks of searchable history, and answers natural-language questions — offline, inside ~2 GB RAM and 2 ARM A5x-class cores, in under 2 seconds for common queries.

This repo holds the **research** behind the design: the evidence, open-source building blocks, papers, and the architecture they point to. It is not the implementation — that comes later.

## Contents

- [`docs/vehiclegpt-research-dossier.html`](docs/vehiclegpt-research-dossier.html) — the research dossier. Open it locally in a browser, or enable [GitHub Pages](https://pages.github.com/) on this repo (Settings → Pages → Deploy from `main` / `docs`) to view it as a page at `https://akash-ainapur.github.io/VehicleGPT/vehiclegpt-research-dossier.html`.

The dossier covers:

- The core design idea — a small on-device model routes questions to deterministic tools; it never computes numbers itself
- System architecture, with the AI kept in its own read-only partition isolated from safety-critical functions
- Vehicle data collection per protocol (CAN, SOME/IP, VHAL, QNX/DLT, ADAS, diagnostics), normalised to COVESA VSS
- SLM selection rationale and candidate models
- Search & retrieval workflow, with a latency budget
- Historical storage design (tiered, flash-aware, weeks of retention)
- Trend/anomaly/cause analytics
- Edge deployment sizing and the scaling path from reference board to vehicle HPC
- User interaction design for drivers, service engineers, and fleet/validation teams
- Safety, security and privacy design
- Simulation and validation strategy
- A table of hidden-gem open-source repos, key papers, and the industry landscape, each sourced

## Project constraints (from the brief)

| Requirement | Constraint |
|---|---|
| Compute | ~2 GB RAM, ~2 ARM Cortex-A5x cores |
| Latency | < 2 s for common queries |
| Connectivity | No cloud dependency |
| History | Searchable for several weeks |
| Safety | Isolated from safety-critical functions |
| Sources | CAN/CAN-FD, SOME/IP, Android VHAL, QNX, ADAS, camera, diagnostics |

Design principle: **the real production solution the brief describes, not one shaped by whatever demo hardware happens to be on hand.**

## Status

- [x] Research complete
- [ ] Reference implementation
- [ ] Benchmarks on A55-class cores
- [ ] Fine-tuned router
