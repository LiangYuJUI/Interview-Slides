# Experience & Selected Projects

Interview presentation for software, systems, and EDA roles by Yu-Jui Liang. The deck presents NeoPower software engineering, simulation and validation experience, followed by the research direction **Carbon- and Power-Aware Multi-Tier KV Cache Management for Heterogeneous GPU LLM Serving**. The research scope is a single server with heterogeneous GPUs and KV cache tiers spanning HBM, host DRAM and SSD.

The deck has **10 main slides, including the closing slide, followed by 3 backup slides**. The LLM research section is designed for about **3 minutes**; the complete main presentation is about **7–8 minutes**. Traditional Chinese speaker scripts and technical notes are in `speaker_notes.md` and are not embedded in the PDF.

## Slide organization

| # | Title | Purpose |
| --- | --- | --- |
| 1 | Experience & Selected Projects | Cover |
| 2 | Education & Professional Experience | Education and employment history |
| 3 | NeoPower: Backend System Architecture | Platform architecture and personal engineering scope |
| 4 | NeoPower: Scenario-Based System Simulation | Custom simulator and representative scenarios |
| 5 | NeoPower: Testing & Production Reliability | Deployment gate and operational validation |
| 6 | Heterogeneous GPU LLM Serving | Single-server architecture and multi-tier KV cache motivation |
| 7 | Fine-Grained Performance & Power Modeling | Planned operation-level modeling across heterogeneous GPUs |
| 8 | Research Methodology: System-Level Simulation | Proposed discrete-event simulation framework and evaluation |
| 9 | Performance-Constrained Resource Optimization | Cache configuration variables, objectives, constraints and research question |
| 10 | Thank You | Close |
| 11 | SAT-LEX: LLM and SMT-Based Document Verification | Backup flowchart |
| 12 | ABC Mapper: SO Technology Mapper Baseline | EDA backup |
| 13 | Single-Output vs Multi-Output Cell Mapping | EDA backup |

Slides 2–5 and the original backup-slide content and layout are preserved. The former research section has been expanded from two slides to four. The previous deck is archived as `main-old.tex`, `main-old.pdf`, `README-old.md` and `speaker_notes-old.md`; the archived PDF is an exact copy of the prior PDF.

## Research scope and status

The project studies workload- and hardware-aware resource management for LLM inference in a single-server heterogeneous GPU environment. It includes workload characterization, fine-grained performance and power modeling, multi-tier KV cache management, system-level discrete-event simulation, hardware profiling and benchmarking, and performance, energy and carbon trade-off analysis.

Completed research analysis includes an initial literature survey, research problem definition and preliminary framework analysis. Modeling architecture design, framework feasibility evaluation and experimental design are ongoing. Simulator implementation and integration, complete hardware profiling, validated GPU performance and energy models, final optimization algorithms and final evaluations remain planned or in progress. The slides present no fabricated results or hardware measurements.

Operational carbon is evaluated from energy use and electricity carbon intensity. Allocated embodied carbon is an accounting measure and does not imply reduced manufacturing emissions from logical cache allocation. Energy accounting should avoid component double counting. Higher KV cache hit rate is a question to evaluate, since reuse can avoid computation while retention, storage I/O and data movement also consume energy. Comparisons should use comparable workloads, completed service volume and common performance constraints. Goodput is the rate of requests that satisfy the defined service-level objectives.

## Compilation

Compile from this directory with the existing pdfLaTeX workflow:

```bash
latexmk -pdf main.tex
```

From the repository root:

```bash
cd Software-Projects
latexmk -pdf main.tex
```

The mapping backup slides reuse image assets in `../EDA-CAD-Project/figures/`. Keep `main.pdf` in sync with `main.tex`.

## Visual and factual checks

- Preserve the 16:9 Madrid-inspired Beamer style, palette, typography and editable TikZ diagrams.
- Slide 6 describes a conceptual single-server architecture and does not assume a particular interconnect or direct GPU-to-SSD access.
- Slide 7 separates Prefill Attention, Prefill FFN, Decode Attention and Decode FFN as modeling categories, not physically separated workers.
- Slide 8 describes proposed system-level discrete-event simulation, not cycle-accurate GPU simulation. Calibration and validation are planned activities.
- Slide 9 distinguishes logical cache allocation from physical hardware provisioning and frames cache-hit energy behavior as a research question.
- Check for exactly 13 pages, overflow warnings, missing images and visual defects after rebuilding. Render and inspect the four research slides, cover, close and backup slides.
