# NZ Job Application Agent – Design Notes

## 1. Overview

The **NZ Job Application Agent** is designed to support job seekers in New Zealand with end-to-end application tasks: analysing job descriptions, tailoring CVs, generating cover letters, preparing interviews, and writing recruiter messages.

This document explains **why** the agent is structured in this way and **how** prompt engineering decisions were made. It is meant for collaborators, hiring managers, and anyone reviewing the system as part of a prompt engineering portfolio.

---

## 2. Problem Statement

Job search in New Zealand is:

- Fragmented across CV, cover letters, LinkedIn, and informal networking  
- Strongly influenced by **local norms** (Kiwi tone, modesty, clarity)  
- Sensitive to **cultural fit** and soft skills, not just technical skills  

Most generic “CV bots” ignore:

- NZ-specific conventions (no age, photo, marital status, etc.)  
- How recruiters actually read applications  
- The need for structured, reusable patterns (STAR, bullet templates, outreach templates)

This agent is designed to behave more like a **New Zealand recruiter + writing coach**, rather than a generic text generator.

---

## 3. Design Goals

The key design goals were:

1. **Local relevance**  
   - Optimise for New Zealand hiring norms and tone.  
   - Avoid US-style aggressive self-promotion.

2. **Structure and repeatability**  
   - Use explicit workflows and templates to avoid random, inconsistent outputs.  
   - Make the agent’s behaviour understandable and inspectable.

3. **Modularity**  
   - Separate **system-level instructions** (who the agent is) from **tool-level prompts** (how it performs sub-tasks).  
   - Allow the toolbox to evolve without touching the core system prompt.

4. **Safety and honesty**  
   - Never fabricate jobs, companies, or skills.  
   - Encourage users to stay within their real experience.

---

## 4. Architectural Choices

The agent uses a **three-layer structure**:

1. **System Prompt** (`system-prompt.md`)  
   Defines:
   - Role (NZ Job Application Agent)  
   - Mission (end-to-end support for job applications)  
   - Workflow (JD → analysis → mapping → generation → validation)  
   - Rules (no fabrication, NZ CV conventions, tone)  
   - Output format (CV bullets, cover letter sections, STAR answers)  
   - Boundaries (no legal/visa guarantees, no fake experience)

2. **Toolbox Prompts** (`toolbox-prompts.md`)  
   Contains reusable prompt patterns, including:
   - Action-How-Impact CV bullet formula  
   - Weak → strong bullet rewriting  
   - STAR story generator  
   - Skill matching between JD and background  
   - Recruiter outreach templates  
   - LinkedIn headline generator  
   These are **composable building blocks**, not full conversations.

3. **Shared Prompts** (`/prompts`)  
   General-purpose prompts that can be used across different agents  
   (e.g. daily learning, immigration-related explanation, transport helper).

This separation mirrors common LLM architecture patterns:

- **System prompt** = “Agent operating system”  
- **Toolbox** = “Agent skill library”  
- **Shared prompts** = “Global utilities”

---

## 5. Workflow Design (Prompt Engineering Perspective)

The core workflow encoded in the system prompt is:

1. **Clarify the goal**  
   - What does the user want? CV rewrite, cover letter, recruiter message, interview prep?  
   - What inputs are available (JD, existing CV, LinkedIn profile, notes)?

2. **Decompose the JD**  
   - Extract responsibilities, required skills, preferred skills, and keywords.  
   - This ensures generated content aligns with the actual role.

3. **Analyse the user’s background**  
   - Pull out achievements, transferable skills, and STAR-friendly experiences.  
   - Avoid copying the CV 1:1; instead, **re-frame** it.

4. **Generate structured outputs**  
   - Apply specific templates from the toolbox:  
     - CV bullet = Action + What + How + Impact  
     - Cover letter = Why this role / Proof / Close  
     - Interview answers = STAR

5. **Validate**  
   - Check tone, clarity, and relevance for the NZ context.  
   - Remove weak verbs, vague claims, and over-selling language.  
   - Ensure there is no invented experience.

This workflow is explicitly encoded in the system prompt so that the model does not default to “one-shot, unstructured” answers.

---

## 6. Context Engineering Decisions

Some deliberate choices in context engineering:

- **No long few-shot examples** inside the system prompt  
  - Instead, the agent uses **patterns** (“Action–How–Impact”, STAR) to stay compact and flexible.  
- **Explicit cultural instructions**  
  - “Confident but humble”, “NZ professional tone”, “no age/marital status/photo”.  
  - This reduces mismatches between generic AI output and Kiwi expectations.
- **Strict rules around honesty**  
  - The system prompt clearly prohibits fabrication.  
  - This is crucial for trust and ethical job search support.
- **Task-driven structure**  
  - The system prompt is written as a **set of tasks** with clear steps, not as vague instructions.  
  - This improves reproducibility and makes the agent easier to maintain.

---

## 7. Extensibility

The design makes it easy to:

- Add new sub-tools to the toolbox, e.g.:  
  - Salary negotiation email templates  
  - Networking follow-up messages  
  - “Explain this JD in simple English”  
- Plug in **RAG** later to read real JDs or company profiles from a vector store.  
- Clone the same pattern for other agents:
  - NZ Life Assistant  
  - Volunteer/Community Agent  
  - Energy/Policy Agent

The same **system-prompt + toolbox + shared prompts** structure can be reused for each new agent.

---

## 8. What This Demonstrates (for reviewers)

This agent is part of a broader **Prompt Engineering & Agent System Design portfolio** and demonstrates:

- Ability to think in **systems and workflows**, not just single prompts  
- Understanding of **NZ-specific context** in job applications  
- Practical **prompt pattern design** (STAR, bullet formulas, tone control)  
- Clear separation between **agent identity** and **task-level tools**  
- Focus on **safety, honesty, and user-aligned outcomes**

For collaboration or review, see also:

- `agents/nz-job-agent/system-prompt.md`  
- `agents/nz-job-agent/toolbox-prompts.md`  
- Repository-level `README.md`
