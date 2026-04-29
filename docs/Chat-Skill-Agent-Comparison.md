# Copilot Interaction, Agent, and Skill Architecture

This page documents a comparison of Copilot Chat, Copilot Cowork Custom Skills, Agent Builder Agents, Declarative Agents in Copilot Studio, and Custom Agents in Copilot Studio.

The content reflects personal experience, hands-on experimentation, and individual interpretation of the current product behavior. It is not an official Microsoft reference and should not be treated as authoritative product documentation.

All observations are based on the author’s understanding at the time of writing and may evolve as the products change.

The focus is on:
- Functional capabilities
- Execution characteristics
- Governance and lifecycle boundaries
- Practical architectural usage

Copilot Cowork is currently a Frontier feature and is developing rapidly. Functionality, availability, and integration patterns may change quickly and without prior notice.

[Sources used, for you to read through yourself & dive deeper](sources.md)
Readers should treat official documentation as a necessary foundation, but validate assumptions against current product behavior, licensing, and tenant configuration before making design or governance decisions.

</br>
</br>

## Minimal Comparison

| Option | What it is | When to use |
|------|------------|-------------|
| Copilot Chat | One-off AI conversation | Single questions, drafting, summaries |
| Cowork Custom Skill | Executable capability | Personal repeatable actions |
| Agent Builder Agent | Instruction-driven assistant | Reusable assistant without governance |
| Declarative Agent (Studio) | Managed instruction-driven assistant | Enterprise assistant with lifecycle control |
| Custom Agent (Studio) | Orchestrated agent with logic | Deterministic processes and workflows |

If execution must be guaranteed → Custom Agent.  
If governance matters but execution is non-deterministic → Declarative Agent.  
If neither matters → Agent Builder Agent.

</br>
</br>

## Copilot Cowork Custom Skill Flow

A Copilot Cowork Custom Skill is not an agent and does not own conversation flow.

In the current product experience, Cowork Custom Skills are invoked through the Copilot Cowork agent, which acts as both the conversational surface and the orchestration layer.

The user interacts with the Copilot Cowork agent via a 1:1 chat. Based on the user input, the Cowork agent determines whether a specific custom skill should be executed.

The invocation flow is as follows:

1. The user interacts with the Copilot Cowork agent.
2. The Copilot Cowork agent interprets the intent.
3. A Cowork Custom Skill is selected and invoked with structured inputs.
4. The skill executes its internal instruction-defined or code-based logic.
5. A single result is returned to the Copilot Cowork agent.
6. The Copilot Cowork agent continues the conversation or presents the result.

Important properties:

- Cowork Custom Skills do not control conversation flow.
- Cowork Custom Skills do not decide what happens next.
- Cowork Custom Skills are stateless per invocation.
- Cowork Custom Skills do not provide retries, rollback, or persistence.
- Lifecycle, governance, and orchestration are owned by the Copilot Cowork agent.

Architectural clarification:

Cowork Custom Skills are architecturally designed as callable capabilities. However, based on current experience, they are surfaced exclusively through the Copilot Cowork agent and are not automatically available from other Copilot chat surfaces or agents.

Agents reason, decide, and orchestrate.  
Cowork Custom Skills execute discrete capabilities.

Skills extend Copilot functionality but never replace agents.

</br>
</br>


## Extended Comparison

| Aspect | Copilot Chat | Copilot Cowork Custom Skills | Agent Builder Agent | Declarative Agent (Copilot Studio) | Custom Agent (Copilot Studio) |
|-------|--------------|------------------------------|---------------------|------------------------------------|--------------------------------|
| What it is | General-purpose AI chat | User-scoped executable skill | Instruction-driven agent | Instruction-driven agent | Orchestrated agent with execution model |
| Primary purpose | Ad-hoc assistance | Execute a repeatable capability | Reusable expert assistant | Reusable expert assistant | Execute end-to-end business processes |
| Interaction model | Free-form conversation | Skill invocation | Free-form conversation | Free-form conversation | Logic- and flow-driven interaction |
| Conversation flow control | None | None | Soft, instruction-driven | Soft, instruction-driven | Explicit, deterministic |
| Flow enforcement mechanism | None | None | Instructions and step ordering | Instructions and step ordering | Topics, conditions, agent flows |
| Workflow logic | None | Instruction-defined steps | Instruction-defined steps | Instruction-defined steps | Workflow and execution engine |
| Business logic | None | Instruction-level logic | Instruction-level logic | Instruction-level logic | Explicit logic and conditions |
| Knowledge grounding | Microsoft 365 data | Microsoft 365 data | Microsoft 365 data | Microsoft 365 data | Microsoft 365 data |
| Tools & connectors | None | Microsoft 365 actions | Tool invocation | Tool invocation | Tool invocation |
| State handling | Session-based | Stateless per invocation | Session-based | Session-based | Persistent, multi-session |
| Reusability scope | Not reusable | Per user | Tenant-scoped | Tenant- and environment-scoped | Environment-scoped |
| Publishing step | No | No | No | Yes | Yes |
| Versioning | No | File versioning | No | Solution versioning | Solution versioning |
| Environment separation | No | No | No | Dev / Test / Prod | Dev / Test / Prod |
| CI/CD support | No | No | No | Power Platform pipelines | Power Platform pipelines |
| Governance and audit | Platform only | None | Limited | Full Copilot Studio governance | Full Copilot Studio governance |
| Intended usage | Individual productivity | Individual productivity | Individual or team productivity | Enterprise-managed assistant | Enterprise automation platform |

</br>
</br>

## Extended Decision Tree (Functional Boundary)

Agent Builder Agent and Declarative Agent (Copilot Studio) share identical functional decision profiles.  
They differ only by lifecycle and governance.

Custom Agent (Copilot Studio) is selected strictly based on execution-risk criteria.

</br>
</br>


| Decision Requirement | Copilot Chat | Copilot Cowork Custom Skills | Agent Builder Agent | Declarative Agent (Copilot Studio) | Custom Agent (Copilot Studio) |
|----------------------|--------------|------------------------------|---------------------|------------------------------------|--------------------------------|
| Conversational interaction | Yes |  | Yes | Yes | Yes |
| Reasoning-driven interaction | Yes |  | Yes | Yes | Yes |
| Execution-driven interaction |  | Yes |  |  | Yes |
| Instruction-defined workflow logic |  | Yes | Yes | Yes |  |
| Guaranteed execution order |  |  |  |  | Yes |
| Deterministic branching |  |  |  |  | Yes |
| Retry / rollback handling |  |  |  |  | Yes |
| Persistent state across sessions |  |  |  |  | Yes |
| Tool invocation required |  | Yes | Yes | Yes | Yes |
| Enterprise publishing required |  |  |  | Yes | Yes |
| Versioning required |  |  |  | Yes | Yes |
| Multiple environments required |  |  |  | Yes | Yes |
| CI/CD required |  |  |  | Yes | Yes |
| Centralized governance required |  |  |  | Yes | Yes |
| Execution auditability required |  |  |  |  | Yes |
| Acceptable non-determinism | Yes | Yes | Yes | Yes |  |

</br>
</br>

## When to Upgrade

Upgrade from Agent Builder Agent  
→ Declarative Agent (Copilot Studio) IF:
- Multiple users depend on the agent
- Versioning or rollback is required
- Environments (Dev/Test/Prod) are required
- Admin governance is required

Upgrade from Declarative Agent (Copilot Studio)  
→ Custom Agent (Copilot Studio) IF:
- Step execution must be guaranteed
- Branching must be deterministic
- Tool calls must not be skipped
- Failures require retries or rollback
- State must persist across sessions
- Auditability of execution is required

Do NOT upgrade if:
- The difference is only conversational quality
- The agent is advisory only
- Errors are tolerable and reversible
