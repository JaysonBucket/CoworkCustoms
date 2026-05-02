[Back to main page](../Readme.md)

## Side observation: how Cowork "remembers" things

Two questions I had about Copilot Cowork that aren't obvious from the docs —
and the answers I worked out hands-on. Sharing in case it saves someone else
the same head-scratching.

### 1. Does Cowork have memory like Copilot Memory?

**It has its own memory, separate from Copilot Memory.**

Two things to keep apart:

- **Copilot Memory** is the tenant-level Microsoft feature. Content is added
  through explicit user input or confirmed prompts — the user stays in the
  loop on what is stored.
- **Cowork's memory** is workspace-scoped and file-based. The assistant
  writes notes to local markdown files when the user asks it to remember
  something, or confirms that a piece of context should be kept. Those notes
  survive across sessions in the same workspace.

From hands-on observation, the two are not connected: what Cowork stores in
its workspace files does not appear in Copilot Memory, and vice versa. Treat
them as two separate stores with different scopes.

Practical implications:
- Cowork's memory is *not* shared across every Cowork conversation you have.
  It belongs to a workspace.
- You can ask to **see, edit, or delete** what's stored — it's just markdown
  files. No hidden state.
- Plain-language requests work: "please remember X", "show me what you have
  on me", "forget Y". No special syntax needed.
- Nothing is written without you triggering it. Memory is a deliberate,
  user-initiated step, not a background process.

Where to put what:
- **Copilot Memory** → context that should be available across your regular
  Copilot Chat experiences (Word, Outlook, Teams Chat, etc.).
- **Cowork memory** → context tied to a specific project or working style
  inside a Cowork workspace.

These two stores do not bridge automatically. If something needs to be
present in both places, it needs to be saved in both places.

### 2. Is there a context limit like normal AI chats?

**Yes, but you don't hit a wall.**

There is a context window, but the system **compresses older parts of the
conversation** before the window fills up. So:

- The conversation doesn't end abruptly when it gets long.
- Very early *verbatim* detail gets condensed into a summary over time.
  The gist stays, the exact wording fades.
- **Memory files survive compression.** Anything you actually want to keep
  long-term should be saved there, not relied on from the chat flow.

Translation for daily use: if a fact, preference, or piece of context
matters beyond the current session, ask the assistant to save it to memory.
The chat itself is short-term storage; memory is long-term — and you decide
what goes in.

---

*Frontier feature, observations from hands-on use, expect this to evolve.*
