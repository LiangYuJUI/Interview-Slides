# Software Engineering & System Simulation

Software engineering interview presentation by Yu-Jui Liang, dated November 6, 2026. The deck covers production software work at NeoPower and ongoing research on cross-data-center Prefill/Decode scheduling across heterogeneous GPU clusters with HBM/HBF memory configurations, targeting higher aggregate serving throughput and lower total system power.

**8 slides; standard speaking target: 7 min 40 sec, including 2.5–3 minutes of research.** Traditional Chinese rehearsal notes and 10-minute extension guidance are in `speaker_notes.md`, separate from the PDF. Both versions use the same slide order and adjust spoken detail. Timing is a rehearsal target.

## Slide organization

| # | Title | Purpose | Time |
| --- | --- | --- | --- |
| 1 | Software Engineering & System Simulation | Simple cover | 15 s |
| 2 | Education & Professional Experience | Existing education and employment history | 35 s |
| 3 | NeoPower: Backend System Architecture | Electric bus platform, personal responsibilities, container isolation | 50 s |
| 4 | NeoPower: Scenario-Based System Simulation | Personally developed simulator, historical inputs, high load and network failures | 90 s |
| 5 | NeoPower: Testing & Production Reliability | Pre-deployment test gate and cross-site charging-power algorithm comparison | 80 s |
| 6 | Heterogeneous GPU LLM Serving Across Data Centers | Global Prefill/Decode scheduling across heterogeneous clusters; three memory configurations | 105 s |
| 7 | Research Methodology: System-Level Simulation | Public specifications and published models feed serving simulation and throughput/power evaluation | 75 s |
| 8 | Thank You | Close | 10 s |

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
- Diagram styles and colors live in the preamble. Research diagrams retain the blue/green palette; memory examples use blue for Full-HBM, mint for Full-HBF and lilac for hybrid.
- Comment banners use final slide numbers 1–8.
- Keep essential diagram labels readable. Remove secondary material rather than shrink fonts or fill whitespace.
- No bottom explanatory captions or disclaimers. Normal theme page numbers remain; caveats belong in the speaker notes.
- Check the build log for box overflow and warnings, verify exactly eight PDF pages, and render and inspect every page after layout changes.

## Factual boundaries

NeoPower:

- Platform architecture is not a claim of sole authorship. Personal scope includes system planning and development, backend APIs, database integration, log analysis/debugging, some deployment and maintenance, and development of the custom simulator.
- The simulator emulates vendors as clients or servers. Scenarios draw on production database logs, customer feedback and observed operational problems.
- The two representative scenarios are high load from buses arriving together and network failures causing mass station/charger disconnection.
- Pre-deployment functional and regression tests must pass before deployment. Post-deployment comparison focuses on old and new charging-power allocation algorithms at sites with similar operating conditions.
- Cross-site observations are not randomized experiments and do not establish causal improvement by themselves. No unconfirmed performance numbers, protocols, customer names or implementation details are added.

LLM research:

- Slide 6 presents a conceptual architecture with multiple data centers and different GPU compute and HBM/HBF capacity profiles. Both centers can run either Prefill or Decode; the scheduler chooses suitable clusters.
- Full-HBM is the conventional baseline. Full-HBF and hybrid HBM/HBF are modeled configurations, not claims of available commercial GPUs. Full-HBF replaces HBM as principal memory without assuming that all buffering or data management disappears.
- HBF means High Bandwidth Flash and is NAND-flash-based. The hybrid 50/50 capacity split is one research example, not a universal requirement.
- Parameter sources are public GPU specifications, existing HBM characteristics and published HBF/NAND-flash research, including proposals associated with SanDisk, SK hynix and academic groups. No unsupported device parameters or benchmark results are included.
- An open-source GPU-cluster serving simulator is the architectural starting point. Detailed GPU-memory/storage-model integration and validation remain ongoing or planned.
- Research scope, literature review and framework exploration are summarized only in Slide 7's speaker notes. There is no standalone roadmap slide.
- Higher aggregate serving throughput and lower total system power are objectives, not achieved results. Simulated estimates are not direct HBF GPU measurements. Power is distinct from energy per token.
- Technical uncertainties include model calibration, parameter provenance and versions, resource contention, cross-data-center communication assumptions and the accounting scope for total power. These remain implementation considerations in the notes.

## Current verification

The revised PDF was built with `latexmk -pdf` / pdfLaTeX and contains eight pages. Every rendered page was visually inspected for clipping, overlap and diagram readability. The compilation log contains no overfull/underfull box warnings. Slides 1–5 retain identical frame source; only the automatic total-page denominator changes. The PDF matches the revised LaTeX source. Speaking durations are rehearsal targets, not measured delivery times.
