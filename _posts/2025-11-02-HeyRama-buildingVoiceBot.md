---
title: "Hey Rama: Building a Voice-First Offline Learning Companion on Raspberry Pi 5"
date: 2025-11-02
categories: [AI Projects, Raspberry Pi, LLM, Offline AI, Education, Product Management]
tags: [Raspberry Pi, Ollama, Qdrant, LangChain, Whisper, Piper, RAG, Edge AI, Product Thinking]
description: "A complete roadmap and offline AI framework guide to build 'Hey Rama' - a private, voice-based learning system for children using Raspberry Pi 5, Ollama, Qdrant, and LangChain."
---

## Vision

- **Hey Rama** is a voice-first, completely offline learning system built on Raspberry Pi 5 (16 GB).  
- It teaches a child topics like Ramayana, Mahabharata, Maths, Logic, Nature, Space, and Storytelling using a local Large Language Model (LLM), speech recognition, and agentic reasoning.
- The project helps a child explore knowledge safely, while giving a product manager like myself- a hands-on builder experience with **real-world AI orchestration**.

![][def]

[def]: /assets/img/Hey-Rama.jpg


## Feature Roadmap and User Stories

Each feature is ordered for incremental build-out with clear objectives and finalized tool references.

### 1. System Setup and Environment
- Objective: Prepare a stable, secure platform for offline AI workloads.  
- Technologies: Raspberry Pi OS 64-bit, Linux, Python, Docker

User Stories
1. Prepare boot media, power supply, and cooling.  
2. Install Raspberry Pi OS (Bookworm 64-bit).  
3. Configure static IP, SSH, and firewall (UFW).  
4. Create `/data` directories for models, corpus, and logs.  
5. Validate system health under load.

---

### 2. LLM Runtime Setup
- Objective: Enable local LLM inference through Ollama.  
- Technologies: Ollama, GGUF 7B (Llama 3.1 or Mistral), systemd

User Stories
1. Install Ollama service.  
2. Pull 7B instruction-tuned model (quantized q5_k_m).  
3. Add smaller fallback model (3B) for quick responses.  
4. Verify response times <8 seconds.

---

### 3. Knowledge Base and RAG Pipeline
- Objective: Build an offline retriever for factual and narrative content.  
- Technologies: Qdrant, Sentence Transformers, Python

User Stories
1. Install Qdrant vector database.  
2. Create collections for each topic: Ramayana, Mahabharata, Maths, Logic, Stories, Nature, Space.  
3. Use local embeddings (`all-MiniLM-L6-v2`).  
4. Ingest chunked, tagged content into Qdrant.  
5. Validate retrieval accuracy, switch to hybrid heirarchical RAG is accuracy is low.

---

### 4. Voice Input and Output
- Objective: Enable hands-free, real-time interaction.  
- Technologies: openWakeWord, Whisper.cpp, Piper

User Stories
1. Calibrate microphone input.  
2. Implement Whisper.cpp for offline STT.  
3. Add wake word “Hey Rama” detection.  
4. Configure Piper for offline child-friendly TTS.  
5. Test full speech loop with <2s total latency.

---

### 5. Orchestration and Agent Flow
- Objective: Build dynamic flow between input, reasoning, and output.  
- Technologies: LangChain (local), REST APIs, JSON flows

User Stories
1. LangChain local orchestration.  
2. Create retrieval-augmented QA chain (RAG).  
3. Add context memory for smoother multi-turn answers.  
4. Map intents: storytelling, quiz, knowledge, logic.  
5. Validate full pipeline: wake → STT → retrieve → LLM → TTS.

---

### 6. Topic-Specific Agents
- Objective: Make “Hey Rama” intelligent across multiple learning domains.  
- Technologies: LangChain, Qdrant, Ollama

User Stories
1. Story Agent - narrates moral and mythological stories.  
2. Quiz Agent - asks short questions and explains answers.  
3. Knowledge Agent - answers “why” and “how” questions.  
4. Each agent retrieves from its domain-specific Qdrant collection.  
5. Test tone consistency for age 5–8.

---

### 7. Safety and Governance
Objective: Keep the system factual, respectful, and child-safe.  
Technologies: Guardrails AI (offline), local logging

User Stories
1. Apply Guardrails filters on responses for tone and safety.  
2. Add parental control (time limits and topic access).  
3. Log all interactions for transparency.  
4. Validate safe outputs.

---

### 8. Monitoring and Maintenance
Objective: Ensure reliability and observability.  
Technologies: systemd, journalctl, Glances

User Stories:
1. Create systemd units for each service (Ollama, Qdrant, STT, TTS).  
2. Set up health checks and daily restarts.  
3. Log CPU/RAM usage and conversation stats.  
5. Add alerts for service failure.

---

### 9. Testing and Demos
Objective: Validate real-life usage.  

Sample Scenarios
1. “Hey Rama, tell me about Hanuman.”  
2. “Quiz me on addition up to ten.”  
3. “Read a story about animals found in Africa.”  
4. “Why is the sky blue?”  

Each should complete end-to-end locally, with clear voice and no external connections.

---

## AI & Agentic Frameworks Planned for Implementation

| Framework | Purpose | Key Learning |
|------------|----------|---------------|
| **LangChain (Local)** | Agent orchestration between Ollama and Qdrant | Chains, retrieval, reasoning |
| **RAGAS** | Evaluate retrieval accuracy and relevance | RAG metrics, quality scoring |
| **Whisper.cpp** | Offline speech-to-text | Real-time STT optimization |
| **Piper** | Offline text-to-speech | Voice synthesis tuning |
| **MemGPT** | Add persistent memory to sessions | Conversation recall, personalization |
| **Guardrails AI (Offline Mode)** | Enforce tone and safety | Response filtering, schema validation |
| **TruLens (Offline Eval)** | Evaluate model helpfulness | Trace and assess reasoning quality |


---

## Learning Areas

| Area | What to Learn? |
|-------|-------------------|
| **LLM Orchestration** | LangChain chains, context flow, structured prompts |
| **Retrieval Evaluation** | RAGAS, groundedness, recall precision |
| **Conversational Memory** | MemGPT local context persistence |
| **Voice UX** | Whisper.cpp latency tuning, Piper tone optimization |
| **AI Safety** | Guardrails rule definition and validation |
| **Agent Evaluation** | TruLens metrics and improvement loop |
| **System Thinking** | Offline-first architecture, reliability design |


---
## A Product Manager’s Perspective

- After over 6 yrs in product management, this project reminded me of what originally drew me to technology- the joy of **building something useful from first principles**.
- “Hey Rama” isn't just an AI experiment; it became a full product lifecycle in miniature - discovery, design, development, validation, and iteration - all compressed into a single, tangible artifact.  
- Every component decision - Ollama for edge inference, Qdrant for retrieval, LangChain for orchestration, Whisper and Piper for voice - mirrors the same trade-offs faced in enterprise-scale products: performance vs. usability, innovation vs. reliability, and ambition vs. maintainability.

From a PM’s lens, it represents five core learnings:

1. **Start with a clear outcome** - “delight the user” here meant delighting my 5-year-old curious son.  
2. **Design with constraints, not despite them** - a 16GB Raspberry Pi forces thoughtful scoping. If you have a 4/8GB one, entire design needs to be mapped out from scratch.   
3. **Prioritize modularity** - each addition (LangChain, MemGPT, RAGAS) had to earn its place.  
4. **Measure value, not volume** - small, observable wins (a faster answer, a more accurate story) trump over-engineered complexity.
5. **Close the feedback loop** - real-world testing with a curious child is better than any synthetic evaluation metric.

In essence, this project bridges **AI system design** and **human-centered product thinking**. It demonstrates that being “AI-ready” as a product manager isn’t about memorizing frameworks- it’s about **understanding the why** behind each layer of intelligence you introduce.

It’s the same muscle we use in large organizations, just exercised in a sandbox of pure creativity.  


## A Father’s Perspective

As a father, “Hey Rama” became something deeper - a bridge between my world of technology and my child’s world of imagination.

I am waiting for the day when my 5-year-old says *“Hey Rama, tell me about Hanuman”* and hearing a gentle, local voice respond- without screens, ads, or distractions - will sure be pretty satisfying!  

Every late-night debugging session would be worth it, because it wasn’t just about code or AI- It was about **showing my child what curiosity looks like in action** - and how we can build our own tools instead of consuming someone else’s.

---

*© 2025 Ujwal Iyer - Reflections of a father and a PM who is learning AI by building, not by watching youtube videos and reels :-).*