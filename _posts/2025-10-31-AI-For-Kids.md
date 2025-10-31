---
title: "Building AI for My 5-Year-Old: Designing Curiosity, Not Consumption"
date: 2025-10-31
categories: [AI, Parenting, Product Management]
tags: [AI for kids, LLM, voice interface, product management, curiosity, Raspberry Pi, LangChain, LangGraph, RAG]
description: "How a Dad, who's a Product Manager is learning AI hands-on by building a safe, voice-only LLM companion for his child - blending parenting, product thinking, and technology."
image:
  path: /assets/img/ai-kid-curiosity.png
  alt: "A father and child exploring AI together through voice interaction"
---

# Building AI for My 5-Year-Old: Designing Curiosity, Not Consumption

My 5-year-old is obsessed with questions.  
Not the “what’s two plus two” kind - but the ones that stop you mid-scroll.  
> “Why can’t we see air?” “Why is Hanuman red?” “Why does a gas flame burn blue, not orange like a matchstick?”

Half my evenings are spent switching between ChatGPT tabs and bedtime stories. It made me wonder - if AI can answer my product strategy questions at work, why can’t it nurture his curiosity too?

That’s when it hit me: *we build AI to make adults efficient; maybe it’s time I build an AI to make kids wonder.*

---

## 1. The “Curiosity Persona”: Understanding a 5-Year-Old User

Before jumping into tools or frameworks, I did what any PM would do - built a persona.  
Not a B2B buyer or an enterprise admin, but a **Curious Explorer aged five**.

| Attribute | Description |
|------------|--------------|
| **Name** |  5 yr old curious toddler |
| **Motivation** | Understand the world through stories, voices, and patterns |
| **Preferred Interface** | Voice, facial cues, sound effects, short narratives |
| **Attention Span** | 2–3 minutes max per topic |
| **Cognitive Model** | Relates abstract ideas to known visuals (Hanuman = strength, fire = energy) |
| **Parental Expectation** | Safe, screen-free, emotionally aware experience |

---

## 2. Jobs-To-Be-Done for the Toddler

| Job | Current Solution | Pain (1–5) | Gain if Solved (1–5) |
|------|------------------|-------------|-----------------------|
| Get answers to big “why” questions | Parents or YouTube Kids | 3 | 5 |
| Listen to Itihasa (Ramayana, Mahabharata) stories with meaning | Parents reading books | 2 | 4 |
| Explore science through daily life | Random videos or books | 4 | 5 |
| Feel heard when asking many questions | Adults often tired or busy | 5 | 5 |

So the core **Job to Be Done** is:  
> “Help me explore my world through conversation - not content.”

---

## 3. Designing for Zero Screen Time

Here’s where most AI tools fail children - they assume visual attention.  
But for a 5-year-old, **eyes are for imagination, not interfaces**.

So, the system must rely purely on **voice + presence**.

- **Wake word model:** “Hey Rama, can you tell me about rainbows?”  
- **TTS engine:** A friendly Indian-accented voice that blends warmth and curiosity.  
- **Sound design:** Each response ends with a short hum, like a “thinking” pause - helping the child know it’s listening.  
- **Emotional pacing:** Limit answers to 2–3 sentences. End with a “What do you think?” to spark dialogue.  

This isn’t a chatbot; I will try to design it like a **co-explorer**.

---

## 4. Safety Architecture: How to Make AI Safe for Kids

Building for kids isn’t just about “PG-rated” data. It’s about emotional safety and cognitive scaffolding.

### a. **Guardrails**
- Use a **local LLM (like Llama 3.1 GGUF)** fine-tuned on pre-vetted content - no open internet access.  
- Curate a **knowledge corpus**: Children’s encyclopedia, Amar Chitra Katha, ISRO science explainers, mythology retellings.  
- Analyze retrievals from RAG and filter out words/meanings which are not toddler friendly

### b. **Ethical Filters**
- Reinforce the phrase “I don’t know” gracefully. For example:  
  > “That’s a deep question. Maybe we can learn that together tomorrow!”  
- Keep tone consistently empathetic, never corrective.  

### c. **Parent Mode**
- Mobile dashboard for parents to view:
  - Topics explored  
  - Follow-up questions  
  - Curiosity trends (what’s peaking this week: “fire,” “planets,” or “Hanuman”)

---

## 5. MVP Scope: A Safe AI Story Companion

| Feature | Description | PM Lens |
|----------|--------------|----------|
| Voice activation | “Hey Mitra!” trigger using Whisper or Porcupine | Accessibility |
| Story modules | Ramayana, Mahabharata, ISRO discoveries, nature sounds | Engagement |
| Question answering | Short conversational responses via Llama.cpp | Core value |
| Parent dashboard | Topic analytics via n8n workflow | Transparency |
| Offline mode | Runs locally on Raspberry Pi | Safety-first |

**North Star Metric:**  
> “Minutes of meaningful conversation per day (vs passive screen time).”

**Guardrails:**  
- Session <10 min per hour  
- 100% offline safety compliance  

**Retention goal:**  
80% weekly usage consistency by the child (measured via parent logs).

---

## 6. The Delight Loop

The delight moment isn’t when it answers correctly.  
It’s when it **asks back**.

> “Do you think Hanuman could jump because he was light like air or strong like wind?”

That’s when a child pauses, *thinks*, and smiles. That’s engagement, not addiction.

That moment becomes viral - not on social media, but across living rooms. Parents talk. Builders notice. And the loop grows.

---

## 7. My Learning Journey as a Product Manager

This project isn’t just for my son - it’s a sandbox for **me** as a product manager.

I’ll be learning AI by **building it hands-on**, using a Raspberry Pi 5 (16GB) as the playground.  
Here’s what I plan to implement and learn through this:

- **LLM integration:** Running local inference with Llama 3.1 GGUF models.  
- **Agentic frameworks:** Building multi-agent orchestration using **LangChain** and **LangGraph**.  
- **Hierarchical RAG (Retrieval-Augmented Generation):** Organizing mythology, science, and nature stories in topic layers.  
- **Text-to-Speech (TTS):** Crafting emotionally warm, kid-friendly voice synthesis.  
- **Speech-to-Text (STT):** Capturing natural child speech and simplifying intent parsing.  
- **Safety and moderation layer:** Filtering and transforming responses for age-appropriateness.  
- **Edge deployment:** Running everything locally for privacy and offline reliability.  
- **Voice UX testing:** Observing how a child’s curiosity shapes the LLM feedback loop.  

So there are really **three happy personas** in this journey:

| Persona | Motivation | Outcome |
|----------|-------------|----------|
| **The Dad** | Sees his child delighted by learning through curiosity, not screens | Pride and purpose |
| **The Product Manager** | Learns AI deeply by building, debugging, and iterating - not consuming theory | Real mastery |
| **The Child** | Gets the power of an LLM through his own voice and imagination | Joy and agency |

---

## 8. Product Manager’s Reflection

This project taught me something no user research could - **curiosity is the most underrated product metric**.

In building this, I’m not launching another “AI for kids” app. I’m **redesigning how curiosity scales safely** in the age of LLMs.  If this works, I’ll have built not just a learning companion for my child - but a blueprint for how AI can grow *with* us, not *over* us.*

---

## 9. What’s Next

I’m building this project **from scratch** - hardware, data pipeline, orchestration, tools, and voice UX.  
The goal is simple:  
> To make curiosity the most natural interface between a child and AI.

Watch this space - I’ll be sharing each milestone as I build the **Kid-Safe AI Companion** on Raspberry Pi 5.  

The next post in this series will cover:  Setup of Raspberry Pi 5

---

*- Ujwal Iyer*  
*Senior Product Manager | SAP Labs | Builder & Dad | Learning AI by Doing*
