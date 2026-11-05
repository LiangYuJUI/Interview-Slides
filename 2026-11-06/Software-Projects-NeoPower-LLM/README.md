# Software Engineering & System Simulation

Interview slides for Delta Electronics software roles and NVIDIA software / system-software roles. The deck connects production backend work at NeoPower with ongoing graduate research on energy-aware LLM serving across heterogeneous GPUs and HBM/HBF memory.

Presenter: Yu-Jui Liang, National Taiwan University, M.S. in Data Science, expected graduation June 2027.

Presentation date: November 6, 2026.

Target length: 7–8 minutes, 9 slides. Spoken rehearsal notes are in `speaker_notes.md` (Traditional Chinese). Those notes are not part of the compiled PDF.

## Slide organization

| # | Title | Role in the story | Time |
| --- | --- | --- | --- |
| 1 | Software Engineering & System Simulation | Cover | 20 s |
| 2 | NeoPower: Backend System Architecture | Production platform and where backend work sat | 55 s |
| 3 | NeoPower: Scenario-Based System Simulation | Why and how external behavior was simulated | 80 s |
| 4 | NeoPower: Testing & Production Reliability | Pre-deployment tests and observational field checks | 65 s |
| 5 | From Production Systems to GPU Simulation | Method bridge; safe to skip in a 5-minute cut | 25 s |
| 6 | LLM Serving: Heterogeneous GPU & Memory | Research question and the 2×3 profile matrix | 70 s |
| 7 | Research Methodology: Simulation Framework | Proposed system-level simulator | 90 s |
| 8 | Current Progress & Research Roadmap | Completed work versus the plan | 45 s |
| 9 | Thank You | Close | ~10 s |

Narrative: production backend engineering, then simulation used for reliability, then the same simulation discipline applied to GPU LLM serving.

## Compilation

From this directory, with pdfLaTeX:

```bash
latexmk -pdf main.tex
```

From the repository root:

```bash
cd 2026-11-06/Software-Projects-NeoPower-LLM
latexmk -pdf main.tex
```

Remove generated auxiliaries without deleting `main.pdf`:

```bash
latexmk -c main.tex
```

pdfLaTeX is intentional. This deck does not need XeLaTeX or an external font. Do not switch engines unless the source starts using Unicode text in the slides.

## How to edit figures and text

All diagrams are TikZ pictures in `main.tex`, so they stay editable without image exports.

- Colors, panel commands, and node styles are in the preamble under the Madrid-inspired identity block and the `Diagram styles` comment.
- HBM is blue (`AccentBlue` / `SoftBlue`). HBF is mint (`Accent` / `SoftMint`). Hybrid cells are drawn by `\hybridcell` as a split of those two fills. If you change `memcell` width or height, update the clip rectangle inside `\hybridcell` so the split cells stay the same size.
- Each slide has a comment banner. Search for `SLIDE 2`, `SLIDE 3`, and so on.
- Keep diagram text on explicit `\\` line breaks. A narrow node will otherwise hyphenate words such as "external" or "vendor".
- `figures/` is reserved for a future export. It is not used by the current build. `\graphicspath` already includes `./` and `figures/`.

After a layout change, rebuild and check `main.log` for `Overfull` boxes, then look at each PDF page. The 16:9 text block is about 15.3 cm wide.

## Reference presentations

Used only as sources. They were not modified.

- `../NV-Testing/main.tex` — visual identity, NeoPower service diagram, and the reliability workflow.
- `../Mapping-HBF-Project-15min/main.tex` — NeoPower custom-simulator wording, and the rule that HBF is modeled from published parameters rather than measured hardware.

## Known limitations and source assumptions

NeoPower

- The architecture diagram is the platform, not a claim that every service was personally designed. Personal scope on the slides is backend integration, simulation, testing, and debugging.
- Named technologies are only those already on the reference slides: Next.js, NestJS / TypeScript, MongoDB, Redis, Elasticsearch, external charging services, and background scheduling plus log export.
- Redis and Elasticsearch are grouped as data / messaging. This deck does not assign them a more specific role.
- Container isolation is stated without naming Docker, Compose, or Kubernetes.
- No protocol names, customer names, incident write-ups, load numbers, or reliability percentages are included, because the reference slides do not provide public figures for them.
- Post-deployment comparisons are observational: same site over time, and similar conditions across sites. They are not presented as a randomized experiment. An older deck used "A/B" more loosely; do not describe that work as a randomized trial.
- The custom simulator is limited to what the Mapping deck states: it reproduced operational workflows and error scenarios, alongside external vendor/client simulators.

LLM research

- The 2×3 matrix is a set of conceptual simulation profiles, not six commercial GPUs.
- HBF is not claimed as directly measured hardware. Capacity, latency, bandwidth, power, and endurance are trade-offs to model.
- LLMServingSim 2.0 (`https://github.com/casys-kaist/LLMServingSim`) and FlashLab HBFSim (`https://github.com/FlashLabAE/HBFSim`) are candidate frameworks. They are not integrated or validated here.
- Slide 7 is a proposed method. Slide 8 separates the survey, design space, and framework evaluation from implementation and results. No speedup, energy, or goodput number is shown.
- The deck does not claim that heterogeneous GPU/HBF scheduling has never been studied.
- System-level simulation is the target. Instruction-level GPU cycle simulation is out of scope, while memory-service contention still matters when it changes the result.
