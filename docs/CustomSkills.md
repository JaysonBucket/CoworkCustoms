[Back to main page](../Readme.md)

Important: You can create custom skills right from Cowork itself. 
- Just use the **/skill** skill 😄 it guides you through the process and helps setting things up.  
- You might nevertheless want to set up your own SKILL.md and additions, that's why I had a closer look on it
- learnign about it's structure and logic might also help in deepening understanding
- [check in here for the two options to add custom skills and run quality checks for accuracy](AddCustomSkills.md)

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
```

Folder name must match the name: field exactly
Use kebab-case (letters, digits, hyphens)
description should include the phrases that trigger it

</br>
</br>

### Custom Skills: Copilot Cowork vs. Claude Cowork

**Be warned:**
- ClaudeCowork tools/skills and Copilot Cowork Custom Skills are built for fundamentally different orchestration, security, and lifecycle models
- a 1:1 reuse is neither technically nor conceptually possible

Anthropic skills are model‑oriented extensions.  
Copilot Cowork Custom Skills are platform‑oriented extensions.  

</br>

Claude skills and Cowork: The model is the orchestrator
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

## Worked Example – Porting an Anthropic Skill to a Copilot Cowork Custom Skill

This example illustrates how a typical Anthropic (Claude) skill needs to be adapted before it can be used as a Copilot Cowork Custom Skill.

The goal is not identical behavior, but a safe and functional equivalent that fits Copilot Cowork’s orchestration, security, and lifecycle model.

### Example Scenario

Original use case:
A skill that retrieves customer information, validates it, and summarizes the status for the user.

### Anthropic Skill (Conceptual)

In an Anthropic-based implementation, the skill is designed with the following assumptions:

- The language model decides when to call the skill.
- The model may call the skill multiple times.
- The model interprets partial results and decides next steps.
- The skill may combine multiple responsibilities.

Typical behavior:
- Input is loosely structured.
- The skill fetches data, applies logic, and formats a user-friendly response.
- Errors are described in natural language and rely on the model to retry or recover.

Example responsibility set:
- Lookup customer by name or ID
- Validate customer status
- Handle missing data
- Produce a conversational summary

### Problems When Porting Directly

If this skill is reused as-is, several issues arise:

- Copilot Cowork Custom Skills are not called directly by the model.
- The skill cannot decide whether it should retry or branch.
- Conversational formatting inside the skill overlaps with agent responsibility.
- User identity and permissions are not enforced implicitly.

As a result, the skill must be restructured.

### Copilot Cowork Custom Skill (Ported Version)

The ported skill is reduced to a single, clearly bounded capability:

Ported responsibility:
- Retrieve customer record by a provided identifier and return normalized data.

What changes:

Input:
- Explicit parameters (for example: customerId).
- No reliance on conversational context.

Execution:
- Single operation.
- No branching or retries.
- No conversational output.

Output:
- Structured result (for example: status code and customer fields).
- No user-facing explanation.

The Copilot Cowork agent now owns:
- Deciding when to invoke the skill.
- Handling missing or invalid input.
- Determining follow-up steps.
- Communicating results to the user.

### Resulting Flow

1. User asks the Copilot Cowork agent about a customer.
2. The Cowork agent determines that customer data is required.
3. The Cowork Custom Skill is invoked with a structured identifier.
4. The skill retrieves and returns the customer record.
5. The Cowork agent:
   - Interprets the result
   - Applies additional reasoning if needed
   - Presents a response to the user

### Key Takeaways from the Example

- The Anthropic skill performed both reasoning and execution.
- The Copilot Cowork Custom Skill performs execution only.
- Decision-making and conversation move to the agent.
- The skill becomes smaller, simpler, and more predictable.

This pattern repeats for most real-world porting efforts:
successful ports reduce scope, externalize decisions, and accept tighter execution boundaries.
Max 50 skills per user
