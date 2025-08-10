# 🧪⚡ PromptAlchemy

<table>
  <tr>
    <td>

**Project Type:** Prompt Library Agent + Creative QA System  
**Agent Role:** A digital alchemist who transforms chaotic creative input into clean, high-performing prompt recipes.

</td>
<td align="right" width="240">
  <img src="screenshots/promptalchemy-avatar.png" alt="PromptAlchemy Agent" width="200" />
</td>
  </tr>
</table>

---

## ✨ Purpose

**PromptAlchemy** is a workflow system and agent layer for turning messy creative ideas into structured, tested, and reusable prompts — ready to be deployed across GPT-powered workflows, brand systems, or product features.

This tool is built for **creative teams, strategists, and prompt engineers** who want to:
- Organize prompt libraries by function, format, and use case
- Break down unstructured ideas into reusable components
- Standardize high-performing prompts with metadata, tags, and performance notes
- QA and refine prompts through structured review layers

---

## 🧩 System Components

PromptAlchemy features four sub-agents, each with a defined task in the transformation pipeline:

| Sub-Agent      | Role                                     | Personality Tag         |
|----------------|------------------------------------------|--------------------------|
| **The Extractor** | Pulls core concepts and intent from raw prompt text | 🧐 Curious, investigative |
| **The Classifier** | Sorts the prompt into type, use case, and tags     | 🧠 Methodical, organized |
| **The Refiner** | Edits for clarity, tone, structure, and utility     | 🎯 Meticulous, precise    |
| **The Validator** | Stress-tests prompts for ambiguity and results     | 🔥 Analytical, no-nonsense |

Each sub-agent is anthropomorphized lab equipment with a specific QA function — making the process feel like collaborative alchemy.

---

## ⚙️ Workflow Overview

1. **Input:** Paste in an unstructured prompt or idea
2. **Extraction:** The Extractor pulls purpose, context, and target output
3. **Classification:** The Classifier tags it by prompt type (e.g. Ideation, Rewrite, Research), format, and structure
4. **Refinement:** The Refiner polishes for clarity, tone, and platform fit
5. **Validation:** The Validator stress-tests and flags edge cases, ambiguity, or weak phrasing
6. **Output:** A structured, metadata-rich prompt entry ready to be added to your Prompt Vault

---

## 🧪 Sample Output Format

```json
{
  "title": "YouTube Hook Ideator",
  "type": "Content Generation",
  "format": "Few-shot",
  "description": "Generates 5 high-converting YouTube video hook options",
  "tags": ["YouTube", "Hooks", "Marketing", "Few-shot"],
  "prompt": "You are a YouTube strategist. Given a video title and topic, suggest 5 bold hook variations that would maximize curiosity and CTR...",
  "review_notes": "Works well for marketing; might struggle with technical content"
}
```
---

## 🔧 Tools & Stack
- Models: GPT-4, GPT-4o, Claude 3.5 (tested)
- Platform: Notion, Markdown, JSON, (n8n automation layer WIP)
- Outputs: JSON, Markdown, HTML template (optional)
- Persona Layer: Visual + emotional UX embedded into every step

⸻

## 💼 Use Cases
- Internal prompt QA and reuse for marketing teams
- Training junior team members on prompt writing best practices
- Cleaning up chaotic prompt libraries (e.g. Notion databases, Sheets, internal wikis)
- Adding consistency across multi-agent systems

⸻

## 🚧 Status
- Persona Defined
- Core Prompt Flow Mapped
- Visual Identity Generated
- JSON + Markdown Output Templates Finalized
- n8n Integration (Optional)
- Ready for Showcase or Submission

⸻

## 🧠 Creator Notes

PromptAlchemy is both a utility system and a creative artifact. It’s intentionally playful — because prompt engineering isn’t just logic, it’s language design. And language is messy.

This system helps bring structure without losing soul.

⸻

👤 Created by Ros Talbot

Lightweight AI tools designed for humans first.
