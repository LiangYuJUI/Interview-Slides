# Experience & Selected Projects

Interview presentation for software, systems, and EDA roles by Yu-Jui Liang, dated November 6, 2026. The deck covers production software work at NeoPower and ongoing research on cross-data-center LLM request scheduling across different storage system configurations, targeting improved SLO goodput and lower total system power.

**8 main slides + 3 backup slides; standard speaking target: 6 min 55 sec, including 2 min 15 sec of research.** Traditional Chinese rehearsal notes and 10-minute extension guidance are in `speaker_notes.md`, separate from the PDF. Both versions use the same slide order and adjust spoken detail. Timing is a rehearsal target.

## Slide organization

| # | Title | Purpose | Time |
| --- | --- | --- | --- |
| 1 | Experience & Selected Projects | Simple cover | 15 s |
| 2 | Education & Professional Experience | Existing education and employment history | 35 s |
| 3 | NeoPower: Backend System Architecture | Electric bus platform, personal responsibilities, container isolation | 50 s |
| 4 | NeoPower: Scenario-Based System Simulation | Personally developed simulator, historical inputs, high load and network failures | 90 s |
| 5 | NeoPower: Testing & Production Reliability | Pre-deployment test gate and cross-site charging-power algorithm comparison | 80 s |
| 6 | Cross-Data-Center LLM Serving | Global request routing across three conceptual storage configurations; local A/E scheduling within each data center | 60 s |
| 7 | Research Methodology: System-Level Simulation | Public specifications and published models feed serving simulation and throughput/power evaluation | 75 s |
| 8 | Thank You | Close | 10 s |
| 9 | SAT-LEX: LLM and SMT-Based Document Verification | Backup flowchart | Q&A |
| 10 | ABC Mapper: SO Technology Mapper Baseline | Backup, EDA-CAD slide 6 | Q&A |
| 11 | Single-Output vs Multi-Output Cell Mapping | Backup, EDA-CAD slide 7 | Q&A |

NeoPower testing is followed directly by the LLM research question. Slides 3–5 follow the presenter's finalized explanation: system and responsibilities, custom simulator, then deployment validation. SAT-LEX and two mapping slides follow Thank You as Q&A backups.

## Compilation

Use the existing pdfLaTeX workflow from this directory:

```bash
latexmk -pdf main.tex
```

From the repository root:

```bash
cd Software-Projects
latexmk -pdf main.tex
```

Clean auxiliaries without deleting the PDF:

```bash
latexmk -c main.tex
```

Rebuild `main.pdf` whenever `main.tex` changes. Keep the PDF in sync with the source. No external fonts are needed. Mapping backups reuse three image assets in `../EDA-CAD-Project/figures/`.

## Editing and visual checks

- Preserve the existing blue/green, 16:9 Beamer identity and editable TikZ diagrams.
- Slide 2 retains its original two-column education/employment content from `../NV-Testing/main.tex`; reference folders are not modified.
- Diagram styles and colors live in the preamble. Research diagrams retain the blue/green palette; storage examples use blue for HBM-focused, mint for HBF-focused and lilac for hybrid HBM/HBF.
- Comment banners use final slide numbers 1–11.
- Keep essential diagram labels readable. Remove secondary material rather than shrink fonts or fill whitespace.
- Slide 6 labels the storage configurations as conceptual research examples and ends with the research goal. Normal theme page numbers remain; detailed caveats belong in the speaker notes.
- Check the build log for box overflow and warnings, verify exactly eleven PDF pages, and render and inspect every page after layout changes.

## Factual boundaries

NeoPower:

- Platform architecture is not a claim of sole authorship. Personal scope includes system planning and development, backend APIs, database integration, log analysis/debugging, some deployment and maintenance, and development of the custom simulator.
- The simulator emulates vendors as clients or servers. Scenarios draw on production database logs, customer feedback and observed operational problems.
- The two representative scenarios are high load from buses arriving together and network failures causing mass station/charger disconnection.
- Pre-deployment functional and regression tests must pass before deployment. Post-deployment comparison focuses on old and new charging-power allocation algorithms at sites with similar operating conditions.
- Cross-site observations are not randomized experiments and do not establish causal improvement by themselves. No unconfirmed performance numbers, protocols, customer names or implementation details are added.

LLM research:

- Slide 6 emphasizes cross-data-center request scheduling. Incoming LLM requests reach a Global Request Router, which selects among Data Center A (HBM-focused), B (Hybrid HBM/HBF) and C (HBF-focused).
- Each data center contains its own Local A/E Scheduler and both Attention and Expert Workers. The local scheduler manages work within that site; the diagram does not require Attention and Expert workers to reside in different data centers.
- These storage configurations are conceptual research examples, not claims about deployed or commercially available GPU hardware. No fixed HBM/HBF capacity ratio is assumed. GPU heterogeneity is an implementation detail.
- HBF means High Bandwidth Flash and is NAND-flash-based.
- Parameter sources are public GPU specifications, existing HBM characteristics and published HBF/NAND-flash research, including proposals associated with SanDisk, SK hynix and academic groups. No unsupported device parameters or benchmark results are included.
- An open-source GPU-cluster serving simulator is the architectural starting point. Detailed GPU-memory/storage-model integration and validation remain ongoing or planned.
- Research scope, literature review and framework exploration are summarized only in Slide 7's speaker notes. There is no standalone roadmap slide.
- Improved SLO goodput (the rate of requests meeting the defined service-level objectives) and lower total system power are objectives, not achieved results. Simulated estimates are not direct HBF GPU measurements. Power is distinct from energy per token.
- Technical uncertainties include model calibration, parameter provenance and versions, resource contention, cross-data-center communication assumptions and the accounting scope for total power. These remain implementation considerations in the notes.

## Current verification

Rebuild with `latexmk -pdf main.tex`. The expected output is eleven pages: eight main slides followed by three Q&A backups. SAT-LEX uses an editable TikZ flowchart with two LLM conversion paths: legal documents become SMT constraints, while report/scenario documents become logical variables. The SMT solver checks the two for consistency or conflict. Mapping content and image crops are reused from EDA-CAD slides 6 and 7, with local page numbering and without links to omitted EDA-CAD detail pages.
