# GENERTIA-LLM — Red-Team Probe Generation

An interactive HTML-based architecture visualization for the **GENERTIA-LLM co-evolution framework**. The presentation illustrates how an evolutionary red-team loop uses a small language model, deterministic grounding, an immune-system-inspired detector, memory, strategy storage, and telemetry to generate and evaluate candidate attack probes.

## Overview

The visualization presents the red-team workflow as an interactive, step-by-step architecture diagram.

At the center of the workflow are:

- **GRT — Genetic Red-Team:** Runs the evolutionary search loop.
- **SLM-A — Attacker Micro-Agent:** Proposes attack mutations using natural-language intent.
- **GND — Vibe-to-AIS Grounder:** Converts the attacker's natural-language proposal into a schema-valid attack triple.
- **AIS-IDS — Negative-Selection Engine:** Scores candidate attacks and determines whether they are detected or missed.
- **ExpRAG:** Stores previous trajectories and supports warm-starting.
- **RSD:** Maintains ranked attack strategies and their strengths.
- **Candidate Pool:** Stores promising evolved attack triples.
- **Holes Repository:** Records uncovered regions or detector blind spots.
- **Run Configuration:** Provides parameters controlling the evolutionary process.
- **Telemetry:** Records execution metrics such as rounds, tokens, and diversity.

## Workflow

The interactive presentation walks through the architecture in sequence:

1. Receive a seeded candidate population and run configuration.
2. Start the genetic red-team evolutionary loop.
3. Provide the attacker with information about uncovered detector regions.
4. Generate a natural-language mutation proposal.
5. Ground the proposal into a precise, validated attack triple.
6. Submit the grounded triple to the AIS-IDS detector.
7. Receive detection and safety-related scores.
8. Select promising candidates according to the evolutionary fitness function.
9. Warm-start future generations using previous trajectories.
10. Consult and update the ranked strategy distribution.
11. Store promising candidates.
12. Record successful trajectories and uncovered detector gaps.
13. Stream execution metrics to telemetry.
14. Pass candidate triples to the evaluation stage.

## Core Data Model

An evolved red-team probe is represented as a triple:

```text
⟨srcZone, dstService, featureVec⟩
```

where:

- `srcZone` represents the source zone.
- `dstService` represents the destination service.
- `featureVec ∈ [0,1]^d` represents the feature vector.

Candidate provenance tracks lineage information such as:

```text
{parent, gen, guidedBy}
```

Uncovered detector regions are represented through hole records containing information such as:

```text
{triple, nearestGap, selfMargin}
```

## Fitness and Selection

The evolutionary controller applies a multi-factor fitness function:

```text
f = w₁ · edge_gap
  + w₂ · self_margin
  + w₃ · judge_realism
  − penalties
```

The main selection signals include:

- `edge_gap` — distance to the nearest AIS detector.
- `self_margin` — distance from legitimate/self traffic.
- `judge_realism` — realism assessment used during evaluation.
- `penalties` — constraint violations, including false-positive budget violations.

## Interactive Features

### Step-by-Step Navigation

Use:

- **Next** — advance through the architecture.
- **Back** — return to the previous step.
- **Restart** — reset the visualization.

Keyboard navigation is also supported:

- `→` or `Space` — next step.
- `←` — previous step.
- `Esc` — close an information popup.

### Interactive Nodes

Clicking architecture nodes displays additional information about:

- The component's role.
- Incoming connections.
- Outgoing connections.
- Relevant data exchanged with other components.

### Edge Guide

The **Edges** panel explains the major architecture connections:

- **A1** — GRT → SLM-A
- **A2** — SLM-A → GND
- **A3** — GND → AIS-IDS
- **A4** — AIS-IDS → GRT
- **B1** — GRT ↔ ExpRAG
- **B2** — GRT ↔ RSD
- **B3** — GRT → Run Configuration
- **C1** — GRT → Candidate Pool
- **C2** — GRT → ExpRAG
- **C3** — GRT → RSD
- **C4** — AIS-IDS → Holes Repository
- **C5** — AIS-IDS → Telemetry

### Key Terminology

The **Terms** panel provides definitions for concepts including:

- Red packet / triple
- Vibe intent
- Grounding
- `edge_gap`
- `self_margin`
- False-positive budget
- Self-set
- ExpRAG
- RSD
- Hole
- Provenance
- Warm-start
- GA fallback

### Sketch Mode

The **Sketch** control enables interactive modification of the diagram.

When enabled, users can:

- Edit labels.
- Move nodes.
- Resize shapes.
- Rewire edges.
- Delete selected elements.
- Create new connections.

### Freehand Drawing

The **Draw** mode provides a whiteboard-style annotation overlay.

Available controls include:

- Pen color.
- Pen size.
- Eraser.
- Clear ink.

## Technology

The visualization is implemented using:

- HTML5
- CSS3
- JavaScript
- diagrams.net / mxGraph
- SVG-based diagram rendering
- HTML Canvas for annotations
- Inter font

The diagrams.net viewer library is loaded externally.

## Running Locally

No build system is required.

### Open Directly

Open the HTML file in a modern browser:

```text
phase2_presentation_clean.html
```

The presentation loads the diagrams.net viewer library from the web, so an active internet connection may be required.

### Run with a Local HTTP Server

For a more reliable browser environment, use Python:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000/
```

and select the HTML presentation.

## File Structure

```text
.
├── phase2_presentation_clean.html
└── README.md
```

The HTML file contains the complete presentation, including:

- Presentation styling
- Interactive controls
- Architecture diagram definition
- Step-by-step presentation logic
- Component metadata
- Edge descriptions
- Terminology
- Architecture checklist
- Sketch functionality
- Freehand annotation functionality

## Architecture Components

| Component | Responsibility |
|---|---|
| GRT | Evolutionary red-team controller |
| SLM-A | Natural-language attack mutation agent |
| GND | Deterministic grounding of mutation intent |
| AIS-IDS | Candidate scoring and detection |
| ExpRAG | Episodic memory and warm-start retrieval |
| RSD | Strategy ranking and strength distribution |
| Candidate Pool | Storage for promising candidates |
| Holes Repo | Storage for uncovered detector regions |
| D6 | Evolution/run configuration |
| Telemetry | Runtime and diversity metrics |

## Design Intent

The visualization is intended to make the GENERTIA-LLM architecture easier to inspect and communicate by combining:

- Architecture topology
- Data-flow relationships
- Evolutionary search steps
- Component explanations
- Interactive node inspection
- Progressive diagram construction
- Runtime metrics
- Editable annotations

It is designed primarily as an **architecture communication and research presentation artifact**, rather than as an executable implementation of the underlying red-team system.

## Notes

The diagram references subsequent evaluation and defensive stages as part of the broader architecture. These references represent system handoffs and dependencies shown in the visualization; they are not implemented by this HTML file itself.

## License

Add the applicable project license here.

## Authors

GENERTIA-LLM Research Team
