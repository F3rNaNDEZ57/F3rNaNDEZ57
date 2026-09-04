<h1 align="center">Kavindu Fernando</h1>
<h3 align="center">AI Engineer — Production LLM Systems &amp; Agents</h3>

<p align="center">
Building the tool, context, and agent layer for an AI assistant live across 60+ enterprise accounts and 1,500+ users at <a href="https://www.velaris.io/">Velaris</a>. B.Sc. (Hons) IT, University of Moratuwa.
</p>

<p align="center">
<a href="https://linkedin.com/in/fernando-kavindu"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn"></a>
<a href="http://fernandokavindu.me/"><img src="https://img.shields.io/badge/Portfolio-000000?style=flat-square&logo=googlechrome&logoColor=white" alt="Portfolio"></a>
<a href="mailto:kavindufernando.official@gmail.com"><img src="https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white" alt="Email"></a>
<img src="https://img.shields.io/badge/Colombo%2C%20Sri%20Lanka-4B5563?style=flat-square&logo=googlemaps&logoColor=white" alt="Location">
</p>

---

### About

AI engineer at **Velaris**, a B2B customer success SaaS platform, shipping production software since October 2024 and owning LLM/agent engineering since December 2025. Joined during my third year of university and was promoted after 14 months. I own tool design, context management, and output quality for **Velaris Copilot**, and I'm graduating with a B.Sc. (Hons) in Information Technology from the University of Moratuwa in August 2026.

### What I've shipped

- 🧠 **Context management** — shipped rolling-history summarisation that took usable conversation depth from ~5 turns to 20–25 turns (4–5x), eliminating context-overflow errors. Verified across 100+ production conversations.
- 💸 **Cost reduction via fine-tuning** — rebuilt a key-point extraction pipeline on a fine-tuned Gemma model in place of Claude Haiku, cutting daily inference spend from ~$200 to ~$15/day (**92% reduction**) while holding 99% output agreement with the prior model.
- 🤖 **Autonomous agents** — built renewal/expansion agents that draft and send email replies with no human authoring step, adopted by ~50% of the customer base within a month of launch.
- 🔌 **MCP surface** — maintain the Velaris MCP client and a skill-based MCP server exposing Copilot tooling to external clients including Claude and ChatGPT.
- ⚡ **API efficiency** — redesigned a Salesforce sync around bulk operations, cutting API calls per sync from ~60,000 to ~300 (**99.5% reduction**) and eliminating recurring rate-limit failures.

### Research

**[VibeCheck](https://github.com/FYP-Epsilon/Vibe-Check/wiki)** — Post-hoc formal verification of LLM-generated code against BPMN specifications, catching semantic bugs that pass unit tests. Owned the Verified IR Extraction module: AST control-flow extraction, Z3 concolic execution, and differential tracing, backed by 246 automated tests. **99.5% genuine-bug detection** at a 5.9% false-alarm rate across 427 synthetic mutants; **100% structural extraction accuracy** on all 101 FLOW-BENCH programs.

### Tech stack

**LLM &amp; Agents**
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white) ![MCP](https://img.shields.io/badge/Model_Context_Protocol-000000?style=flat-square) ![FAISS](https://img.shields.io/badge/FAISS-4B5563?style=flat-square) ![RAG](https://img.shields.io/badge/RAG-4B5563?style=flat-square)

**Languages**
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black) ![Rust](https://img.shields.io/badge/Rust-000000?style=flat-square&logo=rust&logoColor=white) ![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white) ![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat-square&logo=postgresql&logoColor=white)

**Backend &amp; Frontend**
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white) ![Flask](https://img.shields.io/badge/Flask-000000?style=flat-square&logo=flask&logoColor=white) ![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white) ![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB) ![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=next.js&logoColor=white) ![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)

**Cloud &amp; Data**
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonaws&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white) ![Snowflake](https://img.shields.io/badge/Snowflake-29B5E8?style=flat-square&logo=snowflake&logoColor=white) ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) ![DuckDB](https://img.shields.io/badge/DuckDB-FFF000?style=flat-square&logo=duckdb&logoColor=black)

### Featured projects

| Project | Description |
|---|---|
| **[kapruka-agent](https://github.com/F3rNaNDEZ57/kapruka-agent)** | Multilingual shopping assistant (Sinhala + 140 languages) pairing a live e-commerce MCP server with an LLM agent for product discovery and ordering. NVIDIA NIM, Gemma 3 27B, Pydantic AI, FastAPI/SSE, React. Built for the Kapruka Agent Challenge 2026. |
| **[Ferrite](https://github.com/F3rNaNDEZ57/Ferrite)** | A memory-safe, Rust-native reimplementation of the Cheat Engine idea. |
| **[self-evolving-organism](https://github.com/F3rNaNDEZ57/self-evolving-organism)** | Experimental system exploring self-modifying/evolving program behaviour in Python. |
| **[GraphicsAlgoVisualizer](https://github.com/F3rNaNDEZ57/GraphicsAlgoVisualizer)** | Visualization tool for testing and demonstrating computer graphics algorithms. |
| **[VibeCheck](https://github.com/FYP-Epsilon/Vibe-Check/wiki)** | Formal verification pipeline for LLM-generated code — see Research above. |

### Awards

🏆 **TADHack 2024** — Global Top 10, 1st place in Sri Lanka
🥈 **Hackventure 2024** — 2nd place &amp; Most Innovative Team
🏅 **CodeRush 2023** — 4th place (intra-university competitive programming)
🎖️ Finalist — Enigma 2024, TADHack 2023, SLIIT Codefest

### GitHub stats

<p align="center">
<img src="https://github-readme-stats.vercel.app/api?username=F3rNaNDEZ57&show_icons=true&theme=default&hide_border=true&hide_title=true" alt="GitHub Stats" height="165">
<img src="https://github-readme-streak-stats.herokuapp.com/?user=F3rNaNDEZ57&hide_border=true" alt="GitHub Streak" height="165">
</p>

---

<p align="center"><sub>Open to applied AI / LLM engineering roles — reach out on <a href="https://linkedin.com/in/fernando-kavindu">LinkedIn</a>.</sub></p>
