🌐 AI Agent System (NZ Job + Life Assistant)

A modular, extensible AI Agent Framework designed to support job applications, daily life, and decision-making in New Zealand.
This repository follows a clean separation between:

System Prompts → Define the identity, behaviour, workflow, constraints of each Agent

Toolbox Prompts → Reusable prompt modules for structured tasks

Shared Prompts → Cross-Agent templates for general scenarios

This structure is inspired by OpenAI’s agent design philosophy:
clear roles, modular logic, reusable components.

🗂 Repository Structure
ai-agent/
  agents/
    nz-job-agent/
      system-prompt.md        # Core system instructions for the NZ Job Agent
      toolbox-prompts.md      # Reusable modules for CV, cover letter, STAR, recruiter messages
    nz-life-agent/
      system-prompt.md        # Core system instructions for the NZ Life Assistant
  prompts/
      ...                     # Cross-agent reusable prompts (daily learning, immigration, etc.)
  README.md                   # Project documentation (this file)


Design principles:

Each Agent has its own directory

Each Agent contains at least:

system-prompt.md — Agent brain

toolbox-prompts.md — Agent tools

Shared prompts live in /prompts

Extensible to new Agents without changing the core structure

🤖 Agents Overview
1. NZ Job Application Agent

A specialised Agent built for the New Zealand job market.

Core capabilities:

JD analysis (responsibilities, key skills, keywords)

CV bullet rewriting using NZ-style standards

STAR story generation

Tailored cover letters (3-paragraph NZ format)

Recruiter outreach (Kiwi tone)

Interview prep (structured, NZ-style behavioural Q&A)

Skill matching between JD ↔ user experience

Files:

agents/nz-job-agent/system-prompt.md

agents/nz-job-agent/toolbox-prompts.md

2. NZ Life Assistant Agent

Provides practical support for daily living in New Zealand.

Core capabilities:

Local systems explanation (transport, banking, shopping, rentals)

Safe, step-by-step guidance

Kiwi cultural norms

Bilingual support when needed

Anxiety-reducing, friendly tone

Templates for real-world communication

Files:

agents/nz-life-agent/system-prompt.md

🧱 Architectural Concepts
flowchart TD
    subgraph User Layer
        A[User Input]
    end

    subgraph Agent Core
        B[System Prompt<br/>Role, Mission, Rules]
        C[Workflow Engine<br/>Clarify → Analyse → Generate → Validate]
    end

    subgraph Skill Layer
        D[Toolbox Modules<br/>STAR • Bullet Generator • Rewriter • Classifier]
    end

    subgraph Output Layer
        E[Final Output<br/>Consistent & Structured]
    end

    A --> B
    B --> C
    C --> D
    D --> C
    C --> E

System Prompt = Agent OS (Operating System)

Defines:

Role

Mission

Workflow

Rules

Output format

Style

Boundaries

Every Agent has its own System Prompt, ensuring:

Clear behaviour

Predictable outputs

Modular expansion

Toolbox = Agent’s Skill Modules

Reusable prompt components, e.g.:

CV Action Verb Library

STAR generator

Weak → Strong bullet point transformer

Recruiter outreach templates

Skills matching engine

LinkedIn headline generator

Toolboxes:

Improve consistency

Reduce hallucinations

Allow agents to compose complex tasks

Shared Prompts = Cross-Agent Utilities

Examples:

Daily English learning prompts

Immigration-related explanation templates

General planning or summarisation prompts

Stored separately for reusability (/prompts).

🚀 Adding a New Agent

To create a new Agent:

agents/
  your-new-agent/
    system-prompt.md
    toolbox-prompts.md (optional)

Minimal required fields in system-prompt.md:
# Role
# Mission
# Workflow
# Rules
# Output Format
# Style
# Boundaries


This ensures consistent behaviour across all Agents.

📌 Why This Structure?

✔ Clear separation of concerns
✔ Scalable for multiple Agents
✔ Easy for recruiters / collaborators to understand
✔ Mirrors real-world AI system design (OpenAI / Anthropic style)
✔ Makes your AI engineering skills visible in a professional way

This repository demonstrates:

Prompt engineering

Agent architecture

Modular system thinking

Documentation ability

Practical application to real NZ needs

🛠 Future Enhancements

Planned improvements:

Add RAG (Retrieval-Augmented Generation) to Job Agent (JD database / NZ company profiles)

Add NZ Volunteer Agent

Add Housing & Transport Assistant

Add workflow examples (JD → CV → Cover Letter pipeline)

Add unit-style prompt tests

Add dataset for NZ-specific recruiter communication

👤 Author

Designed and maintained by Lily (Lili Liu)
Focus areas:

AI agent design

Prompt engineering

NZ job market support

Life integration tools for newcomers

System-level thinking
