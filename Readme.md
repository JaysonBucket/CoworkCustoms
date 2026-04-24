Content freshness: 24.04.2026

## What's it about
- personal space to collect information and examples about Copilot Cowork Custom Skills
- my laboratory, happy if it helps anyone else - interested in or would like to xchange? Reach out.
- you could basically directly ask Copilot // Cowork itself to walk you through, this is just the extract of my journey

## Resources and Learning

- [CoWork Announcement](https://www.microsoft.com/en-us/microsoft-365/blog/2026/03/09/copilot-cowork-a-new-way-of-getting-work-done/?msockid=10bdb884f6126c7c175eae73f2126783)
- [CoWork Overview](https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/)
- [CoWork FAQ](https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/cowork-faq?EntityRepresentationId=19d2a7d3-fe20-4a75-9592-8cb07d6fe4c2)
- [CoWork OOTB Skills](https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/use-cowork#cowork-skills)


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

