# Woobeen Back

**I make LLMs run well on small devices, and I have been building AI products since high school.**

On-device AI · LLM compression · MLOps · Mobile AI

📍 Seoul, Korea · remote · UTC-aligned hours
📧 [woobin3069@gmail.com](mailto:woobin3069@gmail.com) · 💼 [LinkedIn](https://linkedin.com/in/woobeen-back-a29ba5259) · 🗂 [c11.kr/woobeen_portfolio](https://c11.kr/woobeen_portfolio)
🟢 Looking for full-time remote roles in on-device / edge LLM inference, model compression, or mobile AI (available after military discharge, Feb 2027).

---

## Highlights

- **Shipped on-device AI to the public.** On a 4-person team I owned all AI and MLOps for [Ollie](https://apps.apple.com/kr/app/ollie-private-ai-talk/id6740768187), an on-device chatbot that reached Product Hunt *Product of the Week #3*.
- **Led a team as a first-year student.** At Eighty 8 Nine I led 4 engineers to launch Noodle4, covering VQA, LLM work, and deployment.
- **Kept building through Army service.** Vollie is an on-device LLM runtime layer on llama.cpp that adapts to each phone's cores, memory, and heat, with a measured performance report that includes what did not work.
- **Presented research.** Poster at AI4F (1st Workshop on LLMs and Generative AI for Finance, held with ACM ICAIF 2024) on LLMs for portfolio rebalancing timing.

```
2020 Latitude / AI Dungeon (volunteer) → 2023 Noodle4 lead (UK) → 2024 Peekaboolabs AI Lead (Korea) → 2025–27 Army service, building Vollie
```

---

## Experience

### Mandatory Military Service — Republic of Korea Army · Aug 2025 – Feb 2027
- Built internal automation tools for an artillery brigade, used by 30+ personnel.
- Won an Army Ideathon award (2026); completed the KAIST SW Education Center AI-SW course for ROKA (2026).

### AI Lead — Peekaboolabs · Dec 2024 – Jul 2025 · Seoul, on-site
*4-person seed-stage startup. Accepted to Smilegate's Orange Planet (Apr 2025). A ₩500M seed round was announced in Oct 2025, after my departure.*

- Owned every AI model, all MLOps, and model compression for the company's on-device products.
- Converted open models to GGUF/GGML or TFLite and tested them on real phones (e.g. EXAONE 3.5, Gemma 3, Llama 3.2, Mistral 7B), and compressed the originals with several techniques.
- Compressed open models for phones with **mixed-precision GGUF quantization**:

  | Model | Size vs. public Q8_0 | Perplexity change |
  |---|---|---|
  | EXAONE 3.5 2.4B | **35% smaller** (1.84 GB vs 2.84 GB) | +2.4% English, +3.2% Korean |
  | Gemma 3 1B | **25% smaller** | +2% English, +7% Korean |

  llama.cpp perplexity on WikiText-2 and a Korean Wikipedia sample. Scripts and results: [hoeio/test-ondevice](https://github.com/hoeio/test-ondevice).
- Used usage data from the live on-device app to see that demand was strongest among users on modest phones without NPU support, so I targeted models under 2–3 GB. Ollie came out of that.
- Worked on Core ML and NPU (Snapdragon, Exynos) optimization.
- Ran models on-device across every project: ONNX Runtime (first, in a mobile photo-editing app), then GGUF with llama.cpp after moving to Flutter, plus Core ML on iOS and LiteRT on Android.
- Shipped **[Ollie](https://apps.apple.com/kr/app/ollie-private-ai-talk/id6740768187)**, an on-device AI chatbot — [Product Hunt](https://www.producthunt.com/products/lora-2) Product of the Week #3.
- Open-sourced **[Lora-SDK](https://pub.dev/packages/lora_sdk)**, the on-device LLM SDK behind Ollie, as a Flutter package (few packages could run on-device models in Flutter).
- Built **[Carve](https://web.archive.org/web/20250622214924/https://carve.peekaboolabs.ai/)** (site as of Jun 2025), an on-device AI optimization platform: 100+ waitlist, "BBB" technology rating from KIBO (Korea Technology Finance Corporation).
- Worked with Intel and LG on on-device AI projects.
- Part of the Korea University Startup Station (KUBS) and Seoul Startup Hub × 500 Global expansion program cohorts.
- Hired after a freelance project with the founder.

### Freelance AI Engineer · Aug – Dec 2024 · remote
- **Livestock monitoring** — YOLO-based vision system that flags abnormal animal behavior. *Working system.*
- **On-device personalization** — fine-tuned Stable Diffusion on a user's selfies with several LoRA approaches to generate images on the phone. *Prototype.*
- **Screen agent** — a vision model finds UI elements on a computer screen and Selenium clicks them. *Working system.*

### Lead AI Engineer — Eighty 8 Nine · Feb 2023 – Aug 2024 · remote, UK (later Technical Adviser)
*Full-time alongside university studies.*

- Led 4 engineers to launch **[Noodle4](https://web.archive.org/web/20240430172023/https://www.noodle4.com/)** (site as of Apr 2024), an AI service that matches brands with influencers and reviews submitted video ads.
- Owned VQA and LLM development and MLOps deployment, working with 3 frontend/backend engineers.
- Researched newer Llama-based VQA approaches and put them into production.
- Built Noodle4's content-review system with ViLT, LLaVA, and qllama (VQA was the main challenge); added a basic defense against influencers gaming the review (inserting content or other tricks to pass the AI check or inflate scores); deployed on AWS.

### Volunteer contributor (unpaid) — Latitude / AI Dungeon · Jul 2020 – Nov 2021 · remote, US
*While in high school.*
- Joined by sending the team a technical proposal; ran model-compression experiments (distillation, quantization, pruning).

---

## Personal Project: Vollie — on-device LLM runtime tuning
*Built during military service · Android · Qwen3.5 4B · not launched yet (store/repo links, more devices and models, GPU numbers, and a comparison against llama.cpp's own benchmark are still to come)*

- Chooses CPU cores, thread counts, context size, and cache format per phone at runtime, and backs off as the phone heats up, instead of shipping one fixed setup.
- On a Snapdragon 888 it sustains **5.4–5.9 tok/s**, against ~4.5 tok/s for a default llamadart setup once the phone is hot, and uses **14% less energy per token** (1.67 vs 1.93 J).
- Diagnosed three blockers that kept the Adreno 660 GPU from loading (an OpenCL 2.0 mismatch, lost native logs, a kernel-compiler bug) and resolved them, with a self-check that falls back to the CPU if a driver misbehaves.
- Saves the model's state after each reply, so a follow-up in a 2,000-token chat is read in ~3 s instead of ~110 s (calculated from measured read speed, not measured end-to-end).
- Wrote up the experiments that did not help (speculative decoding, n-gram lookup, a smaller quantization) next to the ones that did.
- *Note: much of the C/C++ was written with an AI coding assistant; I directed the work and ran the on-phone tests that found the problems.*

---

## Research

- **AI4F — 1st Workshop on LLMs and Generative AI for Finance, ACM ICAIF 2024 (Nov 14, 2024), poster accepted** ([OpenReview](https://openreview.net/forum?id=av3zeO8K7h)): *Enhancing Portfolio Rebalancing Timing Using GPT: A Macroeconomic Indicator Approach.* Combined an LLM with a quantitative pipeline to read macroeconomic indicators and time portfolio rebalancing, with asset-allocation backtesting. Second author.
- **Korean Data Analysis Society, Summer 2024 conference:** *Time-lag Prediction Using Language Models for Events Leading to the U.S. Presidential Election* — a language-model framework that predicts the time lag between linked political events, using NLP to find temporal patterns and causal relationships in political timelines.
- **[SKKU LAMDA Lab R&E (2021–2022)](https://web.archive.org/web/20261031145539/https://sites.google.com/site/hyoh79/research), as a high school student:** Hybrid Attention Unet++, SNN-Transformer, NFT abuse detection.

---

## Awards — 13 AI & data competition awards, 2020–2023

| Year | Award |
|---|---|
| 2020 | Data Creator Camp — Grand Prize |
| 2020 | Gyeonggi-do Data Industrial Manpower Training Project — Grand Prize |
| 2020 | Seoul National Univ. TCE × AI Code Fair — Excellence Prize |
| 2021 | Data Creator Camp — Top Prize |
| 2021 | Hanyang Univ. Artificial Intelligence Task — Grand Prize |
| 2021 | Yonam Institute of Technology Prediction Contest, High School League — Grand Prize |
| 2021 | Gaion New Business Using Trading Big Data — Award |
| 2021 | Korea Power Exchange Public Data Application — Award |
| 2022 | Intflow Creative Hackathon, NIA75 AI Contest — Gold Prize (livestock estrus-sign detection) |
| 2022 | Korea Univ. Pediatric X-ray Data Assignment — Grand Prize |
| 2022 | Quantum Computing AI SW Development Competition — Award |
| 2023 | Small Business Data Analysis and Utilization Contest, Service Development — Award |
| 2023 | KIMFT Innovation Idea Contest — Award |

*Rank names are English translations of the Korean originals.*

---

## Education

- **Kyung Hee University** — Industrial and Management Systems Engineering (2023–). On leave for mandatory military service (completes Feb 2027).
  - 1:1 Mentoring Program (2023–) · KHU Ambassador for CES (2023–2024)
- **Korea Digital Media High School** — Dept. of Hacking Defense (2020–2022)
  - Student Mentor, Machine Learning course (2021–2022) · Leader of a beginner ML study group (2022)
  - Mentor for AI development club "Fregic" (2021–2022) · AI advisor (NPC AI) for game development club "Cracker" (2021)

## Clubs & extracurriculars

- Rendezvous, AI research club — member and free-club leader (2020–2021) · Fregic, AI development club (2022)
- KISTI Cyber Guardians (2021) · National Management Strategy Institute, Youth National Finance Master (2023–2024) · KAIST SW Education Center Military Personnel AI-SW course (2026)

---

## Skills

- **On-device & model work:** llama.cpp, GGML/GGUF, KV-cache quantization, ONNX Runtime, LiteRT, Core ML, model compression (quantization, distillation, pruning), LoRA fine-tuning, VQA, YOLO, Stable Diffusion
- **Stack:** Python, JavaScript, Flutter, PyTorch, TensorFlow, GCP, AWS

## Press

- [Peekaboolabs career site — company history (KO, archived)](https://web.archive.org/web/20261031150434/https://career.peekaboolabs.ai/history): how the founder met and hired me as its first team member, AI Lead.
- [Wowtale, Apr 2025 (EN)](https://wowtale.net/2025/04/25/240348/): Peekaboolabs accepted to Smilegate's Orange Planet.
- [Platum (KO)](https://platum.kr/archives/262349): Peekaboolabs selected for a global expansion program.
- [AI Times (KO)](https://www.aitimes.com/news/articleView.html?idxno=148418): Intflow NIA75 AI Contest award, livestock estrus-sign detection.

---

📧 [woobin3069@gmail.com](mailto:woobin3069@gmail.com) · 💼 [LinkedIn](https://linkedin.com/in/woobeen-back-a29ba5259) · 🗂 [Portfolio](https://c11.kr/woobeen_portfolio)
