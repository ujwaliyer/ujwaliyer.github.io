---
title: "Unpacking toddler persona & AI-ML solutions for an AI Voice Bot"
date: 2025-11-06
categories: [AI Projects, Product Management, Raspberry Pi, Learning by Building]
tags: [AI Voicebot, Toddler Persona, .NET, Llama3, RAG, Qdrant, SymSpell, ONNX, LlamaGuard, Coqui TTS, Product Thinking, Hands-on AI, Raspberry Pi 5, Edge AI, Family Tech]
description: "How a Dad, who's a Product Manager is learning AI hands-on by building a safe, voice-only LLM companion for his child - blending parenting, product thinking, and technology."
---

As a Senior Product Manager, I’ve spent years obsessing over user personas, friction points, and success metrics. But nothing prepared me for my newest and toughest customer: my five-year-old toddler. 

He doesn’t just ask questions. He fires rapid, chaotic queries at bedtime.  
“Appa, why Rama go to forest?” (where to start- because his Dasharatha told him so, or because he promised Kaikeyi that he will grant her boon when the time came?)
“Why did Krishna help Arjuna but not Duryodhana?” (tough to explain righteousness/dharma)  
“Why gas fire blue but diya fire red?” (I still don't know!)  

This blog will focus on pure user research, and suggest AI frameworks and subsequent solutions of the pain point faced by me.  

---

## 1. Persona Deep Dive: “The Curious toddler”

### Who he is
- Age: 5 years  
- Context: bilingual (English + Tamil)  
- Hardware: Raspberry Pi 5, 16GB  
- Interface: Voice only - no screen, no keyboard  

### Behavior Traits
- Speaks in short, broken english  
- Has a 20-second patience window hence easily distracted - responses longer than 20 seconds are lost  
- Emotionally reactive - cannot have wrong tone or scary words

---

## 2. Jobs-to-be-Done + Pain/Gain Matrix

| Job | Current Workaround | Pain (1–5) | Gain if Solved (1–5) |
|------|--------------------|-------------|------------------------|
| Understand epic stories in his own words | Parents explain manually | 4 | 5 |
| Ask science “why” questions safely | YouTube Kids or Khan Academy | 3 | 5 |
| Stay engaged for short bursts | Cartoons | 5 | 4 |
| Speak naturally and be understood | Speech-to-text confusion | 4 | 5 |

---

## 3. Friction Heatmap

| Stage | Friction | Severity (1–5) | Fix Priority |
|--------|-----------|----------------|---------------|
| Voice to Text | Broken grammar | 5 | High |
| Query Understanding | Needs semantic rewriting | 5 | High |
| Answer Generation | Too long / too abstract | 4 | High |
| Response Filtering | Unsafe/adult/violent content | 5 | Critical |
| Text-to-Speech | Must sound friendly, excited, high-pitch, and child-like | 3 | Medium |

---

## 4. Success Metrics

- Attention Retention: responses under 20 seconds  
- Understanding Score: answers correctly paraphrased by child  
- Safe Response Ratio: age-safe answers  
- Latency: TTS response delivered under 2 seconds

---

## 5. Technical Blueprint: AI Concepts to solve Friction & Jobs to be done

Here’s the system I designed for now:

| Step | Who Handles It | Why |
|------|----------------|-----|
| Speech-to-Text Cleanup | SymSpell | Fast spelling and grammar correction |
| Prompt Rewriting | Llama 3.1 7B (Quantized) | Reformulates prompts so a chunked vector matches correctly |
| Vectorize Content | ONNX MiniLM | Transformer based embeddings |
| Storage/Retrieval | Qdrant | Scalable vector DB and similarity search |
| Answer Generation | Llama 3.1 7B again | Generates short, story-like responses |
| Kiddy Guardrails | LlamaGuard | Filters complex or violent content before TTS |
| Text-to-Speech (TTS) | Coqui TTS or System.Speech | Produces warm, human-like voice output |

Each component runs locally on the Raspberry Pi, respecting privacy and keeping everything offline.  
No cloud calls, no hidden data drift - just pure, safe, curious AI for a curious child.  

---

## 6. Why .NET Makes It Possible

I chose .NET not just out of nostalgia, but also because the AI ecosystem quietly supports all of this:  

- STT + TTS → System.Speech namespace or Coqui integration via C#  
- Qdrant Vector DB → Official .NET client with REST bindings  
- ONNX Runtime → Runs MiniLM embeddings natively on CPU  
- Llama 3.1 7B (GGUF) → Compatible via llama.cpp bindings for .NET  
- SymSpell.NET → Lightweight typo and grammar fixer  
- LLamaSharp → C# binding for llama.cpp so can load LlamaGuard model  

---

### Watch this space  
I’ll be sharing the step-by-step build of this **AI Toddler Explorer** soon - from RAG pipelines to voice tuning - all on a humble Raspberry Pi 5.  
Follow my journey at [ujwaliyer.com](https://ujwaliyer.com) - where bedtime questions meet machine learning.