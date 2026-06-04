# Common Ground

**A convergence-first coordination platform powered by [JC Compute](https://github.com/JamesC-xhecarpenxer/JC-Compute-Model) and UniStack.**

> Most communication tools optimize for messaging.
> People actually need alignment.

Common Ground makes **shared understanding** the primary object. Not channels. Not threads. Not feeds. History, agreements, and convergence.

---

## The core idea

Every action in Common Ground creates a causally linked event. State is never edited directly — it is always derived from history through deterministic reduction. This means:

- You can always answer **why** a decision was made.
- You can always replay history and arrive at the same state.
- Different people can see different **projections** of the same history.
- Convergence is **measurable** — not a feeling, a number.

Powered by the JC Compute model: `(H, C, R, π, ⊔)` — History, Capability, Reducer, Projection, Merge.

---

## Install

```bash
git clone https://github.com/your-org/common-ground.git
cd common-ground
npm install
npm link   # makes the 'cg' command available globally
```

---

## Quick start

```bash
# Create a history for your community
cg history new --name "Community Garden" --namespace neighborhood

# Add a proposal (use the id from the output above)
cg event add --history <id> --type proposal.created \
  --author alice --title "Plant tomatoes this spring" \
  --body "We should grow tomatoes in plot 3."

# Add support
cg event add --history <id> --type support.added \
  --author bob --proposalId <proposal-event-id>

# Adopt it
cg event add --history <id> --type proposal.adopted \
  --author admin --proposalId <proposal-event-id>

# View agreements
cg view --history <id> --as agreements

# View convergence
cg view --history <id> --as convergence

# View timeline
cg view --history <id> --as timeline

# Trace a decision back through its causal chain
cg trace --history <id> --event <eventId>
```

---

## Event types

```
proposal.created      proposal.amended      proposal.adopted      proposal.rejected
concern.raised        support.added         objection.filed
agreement.formed      agreement.amended     agreement.archived
resource.shared       knowledge.added       reference.linked
commitment.made       commitment.met        commitment.broken
vote.cast             decision.made
task.created          task.completed        task.blocked
```

---

## Projections (views)

The same history. Different views. This is the `π` (projection) operator from JC Compute.

| View | What it shows |
|------|---------------|
| `timeline` | Full causal event stream |
| `agreements` | Active agreements, open proposals, archived |
| `convergence` | Alignment map — actual computational convergence scores |
| `commitments` | Who committed to what and whether they followed through |
| `resources` | Shared knowledge and references |

---

## Architecture

```
Common Ground
     │
     ├── src/history.js      Event types, createEvent, reducers, causal chain
     ├── src/store.js        Persistent JSONL storage (~/.common-ground/)
     ├── src/projection.js   π operator — same history, many views
     └── src/cli.js          CLI entry point
```

### Storage

Histories are stored as JSONL files in `~/.common-ground/histories/`. One event per line. An `_index.json` keeps metadata. This means histories are:

- Human-readable
- Appendable without full rewrites
- Easy to sync, share, or back up

### JC Compute integration

Common Ground is designed to grow into the full JC Compute model:

- **Capability layer** — who can author which event types
- **Merkle roots** — verifiable history integrity via `historyRoot()`
- **Convergent sync** — merge histories from multiple nodes via UniStack's Pareto frontier merge
- **Fixed-point operator** — detect when a community has reached stable agreement

---

## Roadmap

- [ ] Capability-bounded authorship (C layer)
- [ ] Multi-node sync via UniStack
- [ ] HTTP server for collaborative use
- [ ] Web UI
- [ ] AI agent authorship (sovereign agents as first-class citizens)
- [ ] Export to JC Compute proof format

---

## License

Personal / non-commercial use: free. See `LICENSE-PERSONAL.md`.

Commercial / organizational use: `LICENSE-COMMERCIAL.md`.

Powered by [JC Compute](https://github.com/JamesC-xhecarpenxer/JC-Compute-Model) — authority-constrained deterministic causal computation.
