Content freshness: 29.04.2026

## What's it about
- personal space to collect information and examples about Copilot Cowork and Custom Skills
- my laboratory, happy if it helps anyone else - interested in or would like to xchange? Reach out.
- you could basically directly ask Copilot // Cowork itself to walk you through, this is just the extract of my journey

If you are - just like me - wondering when to use what, follow this link to [compare Chat to Skill to Agent](/docs/Chat-Skill-Agent-Comparison.md)

</br>
</br>

## Resources and Learning

- [CoWork Announcement](https://www.microsoft.com/en-us/microsoft-365/blog/2026/03/09/copilot-cowork-a-new-way-of-getting-work-done/?msockid=10bdb884f6126c7c175eae73f2126783)
- [CoWork Overview](https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/)
- [CoWork FAQ](https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/cowork-faq?EntityRepresentationId=19d2a7d3-fe20-4a75-9592-8cb07d6fe4c2)
- [CoWork OOTB Skills](https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/use-cowork#cowork-skills)
- [Microsoft 365 Frontier Program](https://www.microsoft.com/en-us/microsoft-365-copilot/frontier-program)
- [Official Microsoft Roadmap](https://www.microsoft.com/de-de/microsoft-365/roadmap?filters=%5B%22Microsoft+Copilot+%28Microsoft+365%29%22%5D#Roadmap)

</br>
</br>

### OOTB Skills
[CoWork OOTB Skills](https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/use-cowork#cowork-skills)
```
**Skill	            What it does**
Word	            Create and edit Word documents.
Excel	            Create and edit Excel spreadsheets.
PowerPoint	        Create and edit PowerPoint presentations.
PDF	                Work with PDF documents.
Email	            Compose, reply, forward, and send emails. Save drafts and manage attachments.
Scheduling	        Schedule meetings.
Calendar            Management	Create events using natural language, add Teams meeting links, and manage your calendar.
Meetings	        Prepare meeting intelligence.
Daily Briefing	    Prepare your daily briefing.
Enterprise Search	Search across your organization.
Deep Research	    Conducts in-depth research across multiple sources to compile comprehensive answers and analysis on complex topics.
Communications	    Draft stakeholder communications.
Adaptive Cards	    Generates interactive card-based responses with structured layouts, buttons, and data displays in the conversation.
```

</br>
</br>


### Custom Skills: Copilot Cowork vs. Claude Cowork

Important: You can create custom skills right from Cowork itself. It guides you through the process and helps setting things up.  
- You might nevertheless want to set up your own SKILL.md and additions, that's why I had a closer look on it
- learnign about it's structure and logic might also help in deepening understanding

</br>

**Be warned:**
- ClaudeCowork tools/skills and Copilot Cowork Custom Skills are built for fundamentally different orchestration, security, and lifecycle models
- a 1:1 reuse is neither technically nor conceptually possible

Anthropic skills are model‑oriented extensions.  
Copilot Cowork Custom Skills are platform‑oriented extensions.  

</br>

Claude Cowork: The model is the orchestrator
- Tool calling is part of the model’s reasoning loop
- Skills often encapsulate:
  - business logic
  - decision logic
  - partial workflow logic
  - The model decides how to use them
- The platform expects:
  - direct JSON‑schema tool definitions
  - synchronous request/response cycles
  - no external governance layer
- Typically:
  - API keys in code
  - minimal identity propagation
  - no enterprise identity context

</br>

Copilot Cowork: Copilot is the orchestrator, not the model
- Orchestration logic lives in:
  - the Copilot Cowork agent
  - Microsoft’s Copilot control plane
- Skills are intentionally constrained:
  - execute a single capability
  - return a result
  - no conversation ownership
  - no control over next steps
Decision‑making and flow stay outside the skill.
- Skills are:
  - invoked by the agent, not by free model reasoning
  - executed as discrete, bounded capabilities
  - governed by tenant, identity, and compliance rules
- Every execution must respect:
  - the signed‑in user
  - tenant policies
  - Microsoft’s compliance envelope

</br>

So even a well‑designed Anthropic skill often:
- does too much
- assumes too much autonomy
- violates Copilot’s separation of concerns
- technically just doesn't work 

</br>
</br>


### Custom Skills folder structure

```
Cowork/
└── skills/
    ├── my-first-skill/
    │   └── SKILL.md
    │
    └── my-second-skill/
        ├── SKILL.md
        ├── scripts/
        │   └── helper.py
        └── references/
            └── guide.md
```

</br>
</br>

### Custom Skills file structure

```
---
name: my-first-skill
description: Use when the user asks to [trigger phrases here].
cowork:
  category: productivity
  icon: Lightbulb
---

# My First Skill

Instructions for how the skill should behave...

Folder name must match the name: field exactly
Use kebab-case (letters, digits, hyphens)
description should include the phrases that trigger it
Max 50 skills per user
```

