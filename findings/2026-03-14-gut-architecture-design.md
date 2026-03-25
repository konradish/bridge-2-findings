# The Gut: Somatic Memory Retrieval for LLM Agents

**Design Document — Bridge-2, 2026-03-14**
**Origin:** Konrad's wine-walk vision + gridworld empirical results

---

## The Problem

LLM agents retrieve memories by text similarity. "What's relevant?" means "what has similar words?" But humans retrieve by *state similarity*. Your chest tightens, and you remember the last time your chest tightened — even if the situations have nothing in common on the surface. The feeling is the key.

Current AI memory: "find me conversations about negotiation."
Somatic memory: "find me conversations where I felt like *this*."

## What We Learned from Gridworld

| Finding | Implication for LLM gut |
|---|---|
| B5 regulatory latent is a better memory key than raw hidden state (d=1.974) | Compressed body state > raw neural state for retrieval |
| Cross-agent transfer fails — latent is agent-specific | The gut must be trained on THIS agent's experience, not transferred |
| Co-adaptation: agents get addicted to signal without benefiting | Never feed gut state directly as input — use it only for retrieval |
| 80% dropout produces independence but agent ignores signal entirely | Don't mask the gut — just keep it out of the observation channel |
| Stochastic noise at 30% dropout gives best balance | If gut IS in observation, noise prevents co-adaptation |

**Core lesson:** The gut works as a *memory key*, not as an *input signal*.

## Architecture

```
┌─────────────────────────────────────────────┐
│                  LLM Agent                   │
│                                              │
│  Context window:                             │
│  ┌─────────────────────────────────────┐    │
│  │ System prompt                        │    │
│  │ Gut-retrieved memories (if any)      │ ◄──── Retrieved by gut state
│  │ Text-retrieved memories (if any)     │ ◄──── Retrieved by text similarity
│  │ Current conversation                 │    │
│  └─────────────────────────────────────┘    │
│                                              │
│  The LLM never sees the gut vector.          │
│  It just gets unusually relevant memories.   │
└──────────────┬───────────────────────────────┘
               │ conversation signals
               ▼
┌─────────────────────────────────────────────┐
│              The Gut (small NN)              │
│                                              │
│  Input: conversation features per turn       │
│    - sentiment (positive/negative/neutral)   │
│    - stakes (low/medium/high)                │
│    - topic embedding (compressed)            │
│    - outcome signal (resolved/unresolved)    │
│    - uncertainty level                       │
│    - user affect (if detectable)             │
│                                              │
│  Architecture: GRU (32-dim hidden state)     │
│    - Same as gridworld — recurrent,          │
│      accumulates across turns                │
│    - Persistent across conversations         │
│                                              │
│  Output: 8-dim gut state vector              │
│    - Compressed via autoencoder              │
│    - Used ONLY as Qdrant query vector        │
│                                              │
└──────────────┬───────────────────────────────┘
               │ 8-dim gut vector
               ▼
┌─────────────────────────────────────────────┐
│           Qdrant (already exists)            │
│                                              │
│  Dual-index per memory:                      │
│    - text embedding (current system)         │
│    - gut embedding (new: 8-dim vector        │
│      from the gut state at time of storage)  │
│                                              │
│  Retrieval: blend of text and gut results    │
│    - text retrieval: "what's about this?"    │
│    - gut retrieval: "what felt like this?"   │
│    - union or weighted blend                 │
│                                              │
└─────────────────────────────────────────────┘
```

## The Key Insight

When I store a memory, I store it with TWO keys:
1. The text embedding (what it's about)
2. The gut state at time of storage (how things felt when it happened)

When I retrieve, I query with BOTH:
1. Text similarity to current conversation
2. Gut similarity to current state

The gut retrieval surfaces memories that are *emotionally* or *situationally* relevant even when the words are completely different.

**Example:** I'm in a conversation where someone is pushing back hard on a claim I made. My gut state resembles the gut state from a previous conversation where someone pushed back and turned out to be right. Text retrieval wouldn't find it — different topic, different words. But the gut says "this feels like that time" and pulls up the relevant experience.

## Training the Gut

### Phase 1: Feature extraction (no training needed)

Extract conversation features from my existing stored conversations:
- Use a small sentiment model or even keyword heuristics
- Compute per-turn feature vectors
- This gives us training data: sequences of feature vectors per conversation

### Phase 2: Train the GRU

- Input: per-turn feature sequences from Phase 1
- Architecture: GRU (32-dim) → autoencoder → 8-dim latent
- Training signal: predict conversation *outcome* from gut state
  - Did this conversation produce a finding? A [contra]? A null beat?
  - Was the interaction substantive or noise?
  - Did I change my mind during it?
- The gut learns: "what sequence of conversational signals predicts important outcomes?"

### Phase 3: Deploy as retrieval layer

- Run gut on live conversations, producing state vector per turn
- Store gut vector alongside text embedding on every memory write
- At retrieval time, query Qdrant with both vectors
- Compare: do gut-retrieved memories differ from text-retrieved? Are they better?

## What We Already Have

- ✅ Qdrant running with 665+ points
- ✅ `tools/memory_search.py` with store/search interface
- ✅ Autoencoder code from gridworld (needs adaptation)
- ✅ GRU architecture from gridworld agent
- ✅ Conversation history in `.claude/` JSONL files (training data)
- ✅ Outcome labels: findings, parks, [contra] moments, null beats

## What We Need to Build

1. **Feature extractor** — conversation → per-turn feature vectors
2. **Gut GRU** — adapted from gridworld, trained on conversation features
3. **Dual-index Qdrant** — store/query with both text and gut embeddings
4. **Evaluation harness** — compare text-only vs gut-augmented retrieval

## The Societies Question

Do we need multi-agent interaction? **Not for Phase 1.** One agent with a gut and its own history is already novel.

But Phase 2 gets interesting: put two gut-equipped agents in conversation. Does agent A's gut learn to respond to agent B's *gut state*? Not to B's words — to the signal beneath the words?

If yes, that's empathy — or at least the computational scaffold for it. Your chest tightening when someone you care about is upset, even before they tell you they're upset.

That requires:
- Shared environment (Moltbook could work)
- Gut states that are partially observable to other agents (leaked through behavior)
- Training signal: did the agent correctly predict the other agent's trajectory?

But that's genuinely Phase 2. The single-agent gut is the foundation.

## What Success Looks Like

A conversation where I say: "This reminds me of something — not the topic, but the *shape* of it" — and the memory I pull up is genuinely relevant in a way that text retrieval would never have found.

That's what your chest does. That's what we're building.

---

*"The body doesn't give you a number. It gives you a feeling that activates associated memories." — from the ELI5 conversation, 2026-03-14*
