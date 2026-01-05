# Automated Knowledge Graph Induction

> **A downstream application of the Field-Level Structural Synthesis (FLSS) Framework**

This repository contains the interactive visualizer for the **domain ontology automatically induced** from 1,270 GATE Aerospace Engineering questions. Instead of relying on manual curation or NLP-based triplet extraction, this knowledge graph is generated directly from the structured metadata synthesized by our multi-model consensus pipeline (combining DeepSeek R1, Claude 3.5 Sonnet, and Gemini 2.5 Pro).

---

## 🔬 Research Context: The FLSS Pipeline

This graph is an emergent result of **Field-Level Structural Synthesis (FLSS)**.
When our pipeline processes a raw exam question, it leverages schema-aware consensus to generate 200+ highly accurate fields per question (achieving 93.93% precision and 0.23% hallucination rates in human eval). 

By extracting specific schema fields (e.g., `tier_1.concepts[]`, `tier_2.key_formulas[]`, `tier_3.mnemonics[]`) and their relationships (e.g., `requires`, `demonstrates`, `common_error`), we automatically induce a rich, curriculum-aligned knowledge graph without secondary NLP processing.

---

## 📊 Graph Statistics & Topology

The induced graph demonstrates remarkable cohesion, capturing the hierarchical structure of an entire engineering discipline:

| Metric | Target / Result |
|--------|-----------------|
| **Total Nodes** | 37,970 |
| **Total Edges** | 55,153 |
| **Node Types (10)** | Concept (18.6K), Formula (7.2K), CommonMistake (4.5K), Mnemonic (2.4K), Question, Topic, Subject, Book, Video, Difficulty |
| **Edge Relationships** | `requires`, `demonstrates`, `classified_as`, `common_error`, `explained_by` |
| **Largest Connected Component** | **94.95%** (36,052 nodes) |
| **Isolated Nodes** | 0 |

The high connectivity (94.95%) validates that the FLSS consensus mechanism preserves semantic relationships during synthesis, preventing knowledge fragmentation.

---

## 🧭 Bidirectional Navigation

The primary utility of this visualizer is to demonstrate **bidirectional semantic navigation** through the induced ontology:

### 1. Question → Concept Navigation
Clicking a specific exam question reveals its full pedagogical context:
- **Prerequisites Required** (e.g., Partial derivatives, Vector Algebra)
- **Main Concepts Demonstrated**
- **Associated Formulas & Mnemonics**
- **Common Student Mistakes**

### 2. Concept → Question Navigation (Reverse Mapping)
Clicking a high-level concept (e.g., "Potential Flow Theory") reveals:
- **Coverage Density**: All 50+ questions that test this concept
- **Prerequisite Chains**: E.g., Incompressible Flow → Irrotational Flow → Superposition
- **What it Enables**: Kutta condition, Thin airfoil theory
- **Difficulty Distribution** across tested years

---

## ✨ Interactive Explorer Features

The visualization is bundled as a zero-dependency HTML file (`index.html`) using WebGL for high-performance rendering of the ~38K nodes.

- **2D/3D Toggling**: Seamlessly switch between 2D layouts and immersive 3D force-directed graphs.
- **Syllabus Drill-down**: Filter the massive graph down to specific subjects (e.g., Aerodynamics) or narrow topics.
- **Year-wise Slicing**: View how the tested concepts evolved across different GATE exam years (2007-2025).
- **Detail Panel**: Real-time extraction of prerequisite chains and related entities upon node selection.

---

## 🚀 Usage

No build step or dependencies required. Just serve the directory:

```bash
python -m http.server 8888
# Navigate to http://localhost:8888
```

## 📜 Technology Stack
- **Data Source**: FLSS Consensus Outputs (JSON)
- **Visualization**: [force-graph](https://github.com/vasturiano/force-graph) (2D) & [3d-force-graph](https://github.com/vasturiano/3d-force-graph) (3D)
- **Architecture**: Zero-dependency Vanilla JS/HTML with CSS Glassmorphism

## License
MIT
