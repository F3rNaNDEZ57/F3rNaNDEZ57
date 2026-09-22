<h1 align="center">Kavindu Fernando</h1>
<h3 align="center">Computer Vision Researcher — 3D Gaussian Splatting · Real-Time Capture &amp; Reconstruction</h3>

<p align="center">
AI Research Engineer at <a href="https://synra.ne.jp/">SYNRA Nep</a>, working on radiance-field reconstruction: 2DGS/3DGS, real-time Gaussian capture, and converting splats into simulation-grade geometry. Previously research exchange at Shibaura Institute of Technology, Tokyo. B.Sc. (Hons) IT, University of Moratuwa.
</p>

<p align="center">
<a href="https://linkedin.com/in/fernando-kavindu"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
<a href="http://fernandokavindu.me/"><img src="https://img.shields.io/badge/Portfolio-000000?style=flat-square&logo=googlechrome&logoColor=white" alt="Portfolio"></a>
<a href="mailto:kavindufernando.official@gmail.com"><img src="https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white" alt="Email"></a>
<img src="https://img.shields.io/badge/Research-3D%20Gaussian%20Splatting-4B5563?style=flat-square" alt="Research area">
</p>

---

### Research focus

I work on **3D Gaussian Splatting** — specifically the gap between splats as a *rendering* primitive and splats as a *simulation* primitive.

Gaussian splatting produces photorealistic novel views in minutes, but a cloud of anisotropic Gaussians is not something a physics engine, an acoustic solver, or a robotics simulator can consume. The standard answer is to extract a mesh, and the standard mesh-extraction metric is Chamfer distance — which is the wrong metric when the downstream consumer cares about watertightness, metric scale, and surface planarity rather than average point-to-surface error. A mesh with excellent Chamfer distance can still be unusable for simulation.

That gap is the through-line of everything below.

---

### Active work

#### Splat → polygon without losing simulation fidelity

The core question: how do you convert a Gaussian representation into polygonal geometry that a simulator can actually trust? Current work covers 2DGS-based surface extraction, task-specific fidelity metrics (enclosure, volume and scale error, decimetre-scale planarity) as alternatives to Chamfer-only evaluation, and systematic ablation of the failure modes — mesh leakage, scale drift, material misassignment — that break downstream simulation while leaving reconstruction metrics looking healthy.

#### Gaussian splatting for blind and low-vision assistance

An applied direction with two coupled halves:

- **A map you can ask questions of** — a persistent, language-embedded Gaussian map of a venue, queried in natural language. Because answers come from the map rather than the current frame, they work beyond field of view and around corners.
- **Rendering a room as sound** — 2DGS → watertight mesh → material assignment → geometric acoustics → binaural audio. Doorways become beacons; walls audibly occlude them.

The two compose: the language field supplies semantically labelled points to place sound at, and the extracted geometry determines how that sound travels. A beacon that sounds *muffled because there is a wall in the way* is not something a geometry-blind navigation system can produce. The acoustic layer models the static shell only — people and temporary obstacles are invisible to it — so it is designed as an enrichment layer, never a safety-critical one.

Early stage; running feasibility experiments on RIR simulation error and spatial-audio localization accuracy before committing to the full design.

#### Real-time capture guidance for 3DGS
*Research exchange, Shibaura Institute of Technology, Tokyo — Sep–Oct 2025*

A real-time system that steers a user toward coverage-complete scans instead of letting them discover gaps after training. A 12-bin angular coverage ring driven by optical-flow motion tracking, with live coaching thresholds for blur, exposure drift, and motion parallax — cutting redundant frames while preserving reconstruction coverage. Validated RGB-only feasibility on a consumer smartphone with no depth sensor (iPhone 14 Pro Max), scoped a drone-based autonomous capture path-planning extension, and presented at an internal review.

---

### Research code & publications

| Work | Description |
|---|---|
| **[2D Gaussian Splatting](https://github.com/F3rNaNDEZ57/2d-gaussian-splatting)** | Working fork of 2DGS (SIGGRAPH '24), used as the surface-extraction backbone for the splat→mesh experiments above. |
| **[VibeCheck](https://github.com/FYP-Epsilon/Vibe-Check/wiki)** | Post-hoc formal verification of LLM-generated code against BPMN specifications, catching semantic bugs that pass unit tests. I owned the Verified IR Extraction module: AST control-flow extraction, Z3 concolic execution, and differential tracing, backed by 246 automated tests. **99.5% genuine-bug detection** at a 5.9% false-alarm rate across 427 synthetic mutants; **100% structural extraction accuracy** on all 101 FLOW-BENCH programs. |
| **[GraphicsAlgoVisualizer](https://github.com/F3rNaNDEZ57/GraphicsAlgoVisualizer)** | Visualization tool for testing and demonstrating computer graphics algorithms. |

---

### Tech stack

**3D &amp; Vision**
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![CUDA](https://img.shields.io/badge/CUDA-76B900?style=flat-square&logo=nvidia&logoColor=white) ![3DGS](https://img.shields.io/badge/3D_Gaussian_Splatting-4B5563?style=flat-square) ![2DGS](https://img.shields.io/badge/2D_Gaussian_Splatting-4B5563?style=flat-square) ![COLMAP](https://img.shields.io/badge/COLMAP-4B5563?style=flat-square) ![Open3D](https://img.shields.io/badge/Open3D-4B5563?style=flat-square) ![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white) ![Blender](https://img.shields.io/badge/Blender-E87D0D?style=flat-square&logo=blender&logoColor=white)

**Languages**
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white) ![Rust](https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white)

**LLM &amp; Agents**
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white) ![MCP](https://img.shields.io/badge/Model_Context_Protocol-000000?style=flat-square) ![FAISS](https://img.shields.io/badge/FAISS-4B5563?style=flat-square) ![RAG](https://img.shields.io/badge/RAG-4B5563?style=flat-square)

**Infrastructure**
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black) ![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)

---

### Engineering background

Before moving to research full time, I spent two years shipping production LLM systems at [Velaris](https://www.velaris.io/), a B2B customer success platform — owning tool design, context management, and output quality for Velaris Copilot across 60+ enterprise accounts and 1,500+ users.

- 🧠 **Context management** — shipped rolling-history summarisation that took usable conversation depth from ~5 turns to 20–25 turns (4–5x), eliminating context-overflow errors. Verified across 100+ production conversations.
- 💸 **Cost reduction via fine-tuning** — rebuilt a key-point extraction pipeline on a fine-tuned Gemma model in place of Claude Haiku, cutting daily inference spend from ~$200 to ~$15/day (**92% reduction**) while holding 99% output agreement with the prior model.
- ⚡ **API efficiency** — redesigned a Salesforce sync around bulk operations, cutting API calls per sync from ~60,000 to ~300 (**99.5% reduction**) and eliminating recurring rate-limit failures.

Other things I've built: **[kapruka-agent](https://github.com/F3rNaNDEZ57/kapruka-agent)** (multilingual shopping assistant, NVIDIA NIM + Gemma 3 27B + Pydantic AI), **[Ferrite](https://github.com/F3rNaNDEZ57/Ferrite)** (memory-safe Rust reimplementation of the Cheat Engine idea), and **[self-evolving-organism](https://github.com/F3rNaNDEZ57/self-evolving-organism)** (experiments in self-modifying program behaviour).

---

### Awards

🏆 **TADHack 2024** — Global Top 10, 1st place in Sri Lanka
🥈 **Hackventure 2024** — 2nd place &amp; Most Innovative Team
🏅 **CodeRush 2023** — 4th place (intra-university competitive programming)
🎖️ Finalist — Enigma 2024, TADHack 2023, SLIIT Codefest

---

### GitHub stats

<p align="center">
<img src="https://github-readme-stats.vercel.app/api?username=F3rNaNDEZ57&show_icons=true&theme=default&hide_border=true&hide_title=true" alt="GitHub Stats" height="165">
<img src="https://github-readme-streak-stats.herokuapp.com/?user=F3rNaNDEZ57&hide_border=true" alt="GitHub Streak" height="165">
</p>

---

<p align="center"><sub>Open to research collaboration on Gaussian splatting, neural reconstruction, and simulation-grade 3D — reach out on <a href="https://linkedin.com/in/fernando-kavindu">LinkedIn</a>.</sub></p>
