<h1 align="center">Kavindu Fernando</h1>
<h3 align="center">Computer Vision Researcher — 3D Gaussian Splatting · Capture, Reconstruction &amp; Splat-to-Mesh</h3>

<p align="center">
AI Research Engineer at <a href="https://synra.ne.jp/">SYNRA Nep</a>, building the full chain from capture to geometry: phone video, LiDAR and laser scans in → 2DGS/3DGS reconstructions → simulation-grade meshes out. Previously research exchange at Shibaura Institute of Technology, Tokyo. B.Sc. (Hons) IT, University of Moratuwa.
</p>

<p align="center">
<a href="https://linkedin.com/in/fernando-kavindu"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
<a href="http://fernandokavindu.me/"><img src="https://img.shields.io/badge/Portfolio-000000?style=flat-square&logo=googlechrome&logoColor=white" alt="Portfolio"></a>
<a href="mailto:kavindufernando.official@gmail.com"><img src="https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white" alt="Email"></a>
<img src="https://img.shields.io/badge/Research-3D%20Gaussian%20Splatting-4B5563?style=flat-square" alt="Research area">
</p>

---

### Research focus

I work on **3D Gaussian Splatting**: specifically, the gap between splats as a *rendering* primitive and splats as a *simulation* primitive.

Gaussian splatting produces photorealistic novel views in minutes, but a cloud of anisotropic Gaussians is not something a physics engine, an acoustic solver, or a robotics simulator can consume. The standard answer is to extract a mesh, and the standard mesh-extraction metric is Chamfer distance. That is the wrong metric when the downstream consumer cares about watertightness, metric scale, and surface planarity rather than average point-to-surface error. A mesh with excellent Chamfer distance can still be unusable for simulation.

That gap is the through-line of everything below. So is how I run the work: experiments are pre-registered with go/no-go criteria before they run, and negative results get written down as carefully as positive ones.

---

### Active work

#### Splat → polygon without losing simulation fidelity

The core question: how do you convert a Gaussian representation into polygonal geometry that a simulator can actually trust? Current work covers 2DGS-based surface extraction, task-specific fidelity metrics (enclosure, volume and scale error, decimetre-scale planarity) as alternatives to Chamfer-only evaluation, and systematic ablation of the failure modes that break downstream simulation while leaving reconstruction metrics looking healthy: mesh leakage, scale drift, and material misassignment.

A side project, **splatmesh**, takes a pretrained 3DGS scene to a UV-mapped PBR mesh on Apple Silicon. It benchmarks Poisson, density-field (GOF/SuGaR-style) and 2DGS-TSDF extraction head-to-head, then bakes and differentiably refines textures from the splats. Two findings: Poisson beat TSDF on completeness by 2× (0.746 vs 0.371) at lower Chamfer, and texture refinement gained +8.05 dB on training views but only +2.37 dB held out. Both are measured against the source splats, not scanned ground truth.

#### Capture → isolated 3D asset, as a desktop app

This is a reproducible pipeline from a handheld orbit video of an object to an isolated, surface-normal-aware 2DGS asset. It runs in five stages (frame import with blur rejection → COLMAP → 2DGS training → object isolation → export). It is config-driven, resumable via stage fingerprints, and it pauses with an explicit event when a human decision is needed rather than guessing. Object isolation is a cascade of opacity, radius, colour, DBSCAN and statistical-outlier filters, aiming for clean isolation without per-object hand-tuning.

**Splat Studio** is the Tauri + React desktop GUI that drives it and hosts those decision points (shipped v0.3.0). Making it redistributable meant licence engineering as much as software. I built a GPL-free COLMAP (55 binaries, 157/157 tests passing), swapped in an LGPL ffmpeg verified pixel-identical (mean absolute difference 0.000), and cut the installer from 285 MB to 254 MB.

#### Multi-source capture: phone, LiDAR, and mobile laser scans

Three connected threads on getting better input data into reconstruction:

- **iOS LiDAR capture app.** A native iPhone 14 Pro Max app that records video, LiDAR depth, ARKit pose and IMU on one clock, with a live on-device coverage map. Bundle adjustment brings reprojection error on revisited views from 3–7 px down to ~0.85 px, within 0.92–1.12× of GLOMAP. A pre-registered kill test ruled out the simplest on-device solve, so final poses are refined server-side.
- **Progressive multi-clip capture.** Linking N short handheld clips into one reconstruction, and deciding *during* capture whether a new clip connects to the existing map without ever reporting a false link. The link rule combines inlier counts, rotation consensus and pose consistency. On the design set it accepted 12/12 true links and 0/420 cross-clip candidates, with ArUco markers placing six of eight reconstructions on a common metric scale to within ~1%. A pre-registered hold-out evaluation is next.
- **Scan → navigable splat.** Training walkable Gaussian scenes from mobile laser scans with 360° panoramas. Gaussians are seeded from the LiDAR cloud, panoramas are split into cube faces, and training uses a licence-clean gsplat build. A published densification strategy was re-implemented clean-room from the paper alone. Runs on a multi-GPU V100 DGX Station.

#### Gaussian splatting for blind and low-vision assistance

An applied direction with two coupled halves, currently at the planning and scoping stage:

- **A map you can ask questions of.** A persistent, language-embedded Gaussian map of a venue, queried in natural language. Because answers come from the map rather than the current frame, they work beyond field of view and around corners.
- **Rendering a room as sound.** 2DGS → watertight mesh → material assignment → geometric acoustics → binaural audio. Doorways become beacons, and walls audibly occlude them.

The two compose. The language field supplies semantically labelled points to place sound at, and the extracted geometry determines how that sound travels. The acoustic layer models the static shell only; people and temporary obstacles are invisible to it. It is therefore designed as an enrichment layer, never a safety-critical one. An evaluation protocol and paper plan are drafted, and the first step is feasibility experiments on RIR simulation error and spatial-audio localization accuracy.

#### Real-time capture guidance for 3DGS
*Research exchange, Shibaura Institute of Technology, Tokyo, Sep–Oct 2025*

A real-time system that steers a user toward coverage-complete scans instead of letting them discover gaps after training. It uses a 12-bin angular coverage ring driven by optical-flow motion tracking, with live coaching thresholds for blur, exposure drift and motion parallax, cutting redundant frames while preserving reconstruction coverage. I validated RGB-only feasibility on a consumer smartphone with no depth sensor (iPhone 14 Pro Max), scoped a drone-based autonomous capture path-planning extension, and presented at an internal review.

#### Research infrastructure

**dgx-console** is a single-user control plane for a shared multi-GPU DGX Station. It is driven over SSH, with a CLI and a Textual TUI, a GPU job queue, auditable retry lineage, and direct Drive → DGX data transfer. It exists because long training runs fail silently: it caught a job stalled for 334 minutes with zero frames written that manual review had missed.

<sub>Most of the reconstruction work above lives in private research repos; happy to walk through it on request.</sub>

---

### Research code &amp; publications

| Work | Description |
|---|---|
| **[2D Gaussian Splatting](https://github.com/F3rNaNDEZ57/2d-gaussian-splatting)** | Working fork of 2DGS (SIGGRAPH '24), used as the surface-extraction backbone for the splat → mesh experiments above. |
| **[VibeCheck](https://github.com/FYP-Epsilon/Vibe-Check/wiki)** | Final-year research project (three-person team, University of Moratuwa): post-hoc formal verification of LLM-generated workflow code against BPMN specifications, catching semantic bugs that pass unit tests. I owned the Verified IR Extraction module: AST control-flow extraction, Z3 concolic execution and differential tracing, backed by 246 automated tests. **99.5% genuine-bug detection** at a 5.9% false-alarm rate on a 427-mutant corpus, **164/164** bugs caught in real LLM generations, and **100% structural extraction accuracy** on all 101 FLOW-BENCH programs. |
| **[GraphicsAlgoVisualizer](https://github.com/F3rNaNDEZ57/GraphicsAlgoVisualizer)** | Visualization tool for testing and demonstrating computer graphics algorithms. |

---

### Open source &amp; side projects

| Project | Description |
|---|---|
| **[mathcast](https://github.com/F3rNaNDEZ57/mathcast)** | Claude Code plugin that turns maths and science material (PDFs, notes) into narrated Manim animations: ingest → plan → script → render → self-repair loop → frame inspection → MP4 with subtitles, with local TTS. Narration timing is predicted to within ~4% from word count. |
| **[Ferrite](https://github.com/F3rNaNDEZ57/Ferrite)** | Memory-safe Rust reimplementation of the Cheat Engine idea, now at v1.1.2 across 7 releases, with 145 tests and green CI. |
| **[WorldForge](https://github.com/F3rNaNDEZ57/worldforge)** | Self-hostable worldbuilding wiki (Next.js + SQLite): templates, `[[wiki-links]]` with backlinks, a link graph and interactive maps. |
| **[kapruka-agent](https://github.com/F3rNaNDEZ57/kapruka-agent)** | Multilingual shopping assistant (English / Sinhala / Tanglish, with voice) on NVIDIA NIM + Gemma 3 27B + Pydantic AI, with FastAPI, React, Supabase RAG and an end-to-end test suite. |
| **[self-evolving-organism](https://github.com/F3rNaNDEZ57/self-evolving-organism)** | Experiments in self-modifying program behaviour. |

---

### Tech stack

**3D &amp; Vision**
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat-square&logo=pytorch&logoColor=white) ![CUDA](https://img.shields.io/badge/CUDA-76B900?style=flat-square&logo=nvidia&logoColor=white) ![3DGS](https://img.shields.io/badge/3D_Gaussian_Splatting-4B5563?style=flat-square) ![2DGS](https://img.shields.io/badge/2D_Gaussian_Splatting-4B5563?style=flat-square) ![gsplat](https://img.shields.io/badge/gsplat-4B5563?style=flat-square) ![COLMAP](https://img.shields.io/badge/COLMAP-4B5563?style=flat-square) ![GLOMAP](https://img.shields.io/badge/GLOMAP-4B5563?style=flat-square) ![Open3D](https://img.shields.io/badge/Open3D-4B5563?style=flat-square) ![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white) ![ARKit](https://img.shields.io/badge/ARKit_+_LiDAR-000000?style=flat-square&logo=apple&logoColor=white) ![Blender](https://img.shields.io/badge/Blender-E87D0D?style=flat-square&logo=blender&logoColor=white) ![Three.js](https://img.shields.io/badge/Three.js-000000?style=flat-square&logo=threedotjs&logoColor=white)

**Languages**
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white) ![Rust](https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white) ![Swift](https://img.shields.io/badge/Swift-F05138?style=flat-square&logo=swift&logoColor=white) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white)

**LLM &amp; Agents**
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white) ![Pydantic AI](https://img.shields.io/badge/Pydantic_AI-E92063?style=flat-square&logo=pydantic&logoColor=white) ![MCP](https://img.shields.io/badge/Model_Context_Protocol-000000?style=flat-square) ![Claude Code](https://img.shields.io/badge/Claude_Code_plugins-D97757?style=flat-square&logo=anthropic&logoColor=white) ![FAISS](https://img.shields.io/badge/FAISS-4B5563?style=flat-square) ![RAG](https://img.shields.io/badge/RAG-4B5563?style=flat-square)

**Apps &amp; Infrastructure**
![Tauri](https://img.shields.io/badge/Tauri-24C8DB?style=flat-square&logo=tauri&logoColor=white) ![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) ![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white) ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black) ![NVIDIA DGX](https://img.shields.io/badge/NVIDIA_DGX-76B900?style=flat-square&logo=nvidia&logoColor=white) ![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)

---

### Engineering background

Before moving to research full time, I spent two years shipping production LLM systems at [Velaris](https://www.velaris.io/), a B2B customer success platform. I owned tool design, context management and output quality for Velaris Copilot across 60+ enterprise accounts and 1,500+ users.

- 🧠 **Context management.** Shipped rolling-history summarisation that took usable conversation depth from ~5 turns to 20–25 turns (4–5x), eliminating context-overflow errors. Verified across 100+ production conversations.
- 💸 **Cost reduction via fine-tuning.** Rebuilt a key-point extraction pipeline on a fine-tuned Gemma model in place of Claude Haiku, cutting daily inference spend from ~$200 to ~$15/day (**92% reduction**) while holding 99% output agreement with the prior model.
- ⚡ **API efficiency.** Redesigned a Salesforce sync around bulk operations, cutting API calls per sync from ~60,000 to ~300 (**99.5% reduction**) and eliminating recurring rate-limit failures.

---

### Awards

🏆 **TADHack 2024**: Global Top 10, 1st place in Sri Lanka
🥈 **Hackventure 2024**: 2nd place &amp; Most Innovative Team
🏅 **CodeRush 2023**: 4th place (intra-university competitive programming)
🎖️ Finalist: Enigma 2024, TADHack 2023, SLIIT Codefest

---

### GitHub stats

<p align="center">
<img src="https://github-readme-stats.vercel.app/api?username=F3rNaNDEZ57&show_icons=true&theme=default&hide_border=true&hide_title=true" alt="GitHub Stats" height="165">
<img src="https://github-readme-streak-stats.herokuapp.com/?user=F3rNaNDEZ57&hide_border=true" alt="GitHub Streak" height="165">
</p>

---

<p align="center"><sub>Open to research collaboration on Gaussian splatting, neural reconstruction, and simulation-grade 3D. Reach out on <a href="https://linkedin.com/in/fernando-kavindu">LinkedIn</a>.</sub></p>
