# Software Engineering & System Simulation

Software engineering interview presentation by Yu-Jui Liang, dated November 6, 2026. The deck covers production software work at NeoPower and ongoing research on energy-aware LLM serving across heterogeneous GPUs with HBM/HBF memory configurations.

**9 slides; standard speaking target: 7 min 55 sec.** Traditional Chinese rehearsal notes and 5-minute / 10-minute guidance are in `speaker_notes.md`, separate from the PDF. All three versions use the same slide order and adjust spoken detail.

## Slide organization

| # | Title | Purpose | Time |
| --- | --- | --- | --- |
| 1 | Software Engineering & System Simulation | Simple cover | 15 s |
| 2 | Education & Professional Experience | Existing education and employment history | 35 s |
| 3 | NeoPower: Backend System Architecture | Electric bus platform, personal responsibilities, container isolation | 50 s |
| 4 | NeoPower: Scenario-Based System Simulation | Personally developed simulator, historical inputs, high load and network failures | 90 s |
| 5 | NeoPower: Testing & Production Reliability | Pre-deployment test gate and cross-site charging-power algorithm comparison | 80 s |
| 6 | LLM Serving: Heterogeneous GPU & Memory | Scheduling question and conceptual 2 × 3 compute/memory matrix | 65 s |
| 7 | Research Methodology: Simulation Framework | Proposed profiling/modeling, serving simulation and evaluation architecture | 85 s |
| 8 | Current Progress & Research Roadmap | Completed exploration versus planned implementation and evaluation | 45 s |
| 9 | Thank You | Close | 10 s |

NeoPower testing is followed directly by the LLM research question. Slides 3–5 follow the presenter's finalized explanation: system and responsibilities, custom simulator, then deployment validation. No additional projects are included.

## Compilation

Use the existing pdfLaTeX workflow from this directory:

```bash
latexmk -pdf main.tex
```

From the repository root:

```bash
cd 2026-11-06/Software-Projects-NeoPower-LLM
latexmk -pdf main.tex
```

Clean auxiliaries without deleting the PDF:

```bash
latexmk -c main.tex
```

Rebuild `main.pdf` whenever `main.tex` changes. Keep the PDF in sync with the source. No external fonts or image assets are needed.

## Editing and visual checks

- Preserve the existing blue/green, 16:9 Beamer identity and editable TikZ diagrams.
- Slide 2 retains its original two-column education/employment content from `../NV-Testing/main.tex`; reference folders are not modified.
- Diagram styles and colors live in the preamble. HBM is blue, HBF is mint; `\hybridcell` draws the split fill. Its geometry must match `memcell`.
- Comment banners use final slide numbers 1–9.
- Keep essential diagram labels readable. Remove secondary material rather than shrink fonts or fill whitespace.
- No bottom explanatory captions or disclaimers. Normal theme page numbers remain; caveats belong in the speaker notes.
- Check the build log for box overflow and warnings, verify exactly nine PDF pages, and render and inspect every page after layout changes.

## Factual boundaries

NeoPower:

- Platform architecture is not a claim of sole authorship. Personal scope includes system planning and development, backend APIs, database integration, log analysis/debugging, some deployment and maintenance, and development of the custom simulator.
- The simulator emulates vendors as clients or servers. Scenarios draw on production database logs, customer feedback and observed operational problems.
- The two representative scenarios are high load from buses arriving together and network failures causing mass station/charger disconnection.
- Pre-deployment functional and regression tests must pass before deployment. Post-deployment comparison focuses on old and new charging-power allocation algorithms at sites with similar operating conditions.
- Cross-site observations are not randomized experiments and do not establish causal improvement by themselves. No unconfirmed performance numbers, protocols, customer names or implementation details are added.

LLM research:

- The 2 × 3 matrix contains conceptual profiles, not commercial products. Hybrid colors do not imply a 50/50 memory capacity split.
- HBF is modeled, not directly measured. Hardware trade-offs and optional metric definitions stay in speaker notes.
- Slide 7 is a proposed framework, not an implemented or validated simulator.
- Slide 8 marks literature review, problem/design-space exploration and candidate-framework evaluation as completed. Baseline reproduction, GPU profiling, HBF integration and scheduling experiments remain planned.
- No experimental results or claims of guaranteed energy savings are included.

## Current verification

The revised PDF was built with `latexmk -pdf` / pdfLaTeX and contains nine pages. Every rendered page was visually inspected for clipping, overlap, diagram readability and unwanted bottom commentary. The compilation log contains no overfull/underfull box warnings. Speaking durations are rehearsal targets, not measured delivery times.
