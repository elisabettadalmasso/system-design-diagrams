# Project Brief — System Design Diagrams

## What this project is

A learning portfolio for someone building a new kind of skill set: modeling
real-world systems as structured data, functions, and state machines — then
translating those models into working software.

The diagrams in this repo are Level 1 of a larger progression:

1. **Data modeling vocabulary** (this repo) — entities, attributes,
   relationships, states, transitions. Learning to think about a domain
   before writing code, using ERD/UML concepts expressed in Mermaid.
2. **TypeScript implementation** — translating models into `interface`,
   `type`, discriminated unions. The type system as an executable
   modeling document.
3. **TDD** — once the model is solid, tests drive the implementation
   (red-green-refactor), not the other way around.
4. **Real-world application** — AI agents, CLIs, APIs. Representing
   operation results (success/failure/timeout), agent states, structured
   outputs that another system or LLM can reliably interpret.

The end goal is not "frontend dev who knows UML." It's someone who can
model a domain, enforce its invariants in code, test it rigorously, and
build interfaces (CLI, API, playbook) that separate policy from plumbing.

## Tools and conventions

- Diagrams are written in **Mermaid** syntax inside `.md` files
- Editor: Zed — preview on mermaid.live
- Commits use the prefix `docs:`
- Everything in English (code, file names, comments, diagram labels)

## Diagram types practiced

- **State diagrams**: states, transitions, events, guards `[condition]`,
  choice nodes `<<choice>>`, comments `%%`
- **Class diagrams**: attributes (`-private`, `+public`), methods,
  composition (`*--`), aggregation (`o--`), multiplicity (`"1"`, `"*"`)
- **Sequence diagrams**: `participant`, `actor`, `->>` (call),
  `-->>` (response), `Note over`, `alt/else/end`

### Naming conventions

- `is` prefix for booleans
- `get` prefix for value-returning methods
- `void` for side-effect-only methods
- Class names are capitalized

## Repo structure
diagrams/
├── charging-station/ # EV charging station (state)
├── locker/ # Amazon-style locker (state + class)
├── robot-vacuum/ # Vacuum (state + class + sequence)
├── smart-greenhouse/ # Greenhouse (state × 4 + class)
├── state-uml/ # Earlier exercises (elevator, gate, microwave,
│ # stoplight, washing machine — mixed types)
└── README.md


## What has been done

### State diagrams
Elevator, microwave, washing machine, stoplight, automatic gate,
coffee machine, Amazon locker (compartment + full locker),
smart greenhouse (main + temperature + humidity + light),
EV charging station

### Class diagrams
Robot vacuum, automatic gate, stoplight, Amazon locker,
smart greenhouse, EV charging station

### Sequence diagrams
Stoplight (3 scenarios), robot vacuum (5 scenarios: remote start,
button start, obstacle, low battery, cleaning complete),
EV charging station

## What is still open

- Sequence diagrams: locker, greenhouse
- Optional state diagrams: car wash, boiler, parking barrier, irrigation
- Future: ER diagrams, SQL, BPMN2

## Key concepts being learned

These come from the course material and should eventually be
demonstrable through the work in this repo:

- **Function** — a named decision with an explicit contract
  (input + dependencies → output or modeled failure)
- **Model** — the vocabulary and constraints for reasoning about the
  problem (what's valid, what's distinct, what's allowed)
- **Invariant** — a condition that must stay true for the model to be
  valid, enforced by construction, not by comments
- **State variant** — modeling each state as a separate variant instead
  of one object full of optional fields
- **Transition** — a function from one valid state to another, or to an
  explicit rejection
- **Pure core, effects at the edge** — decisions are pure and testable;
  I/O happens at the boundary
- **Error as part of the model** — expected failures belong in the
  contract, not in thrown exceptions
- **Composition** — building operations by connecting smaller contracts
  (parse → validate → load → decide → save → present)

## Learner profile — how to teach Betta effectively

### Strengths

- **Concrete thinker.** Learns best starting from real, tangible objects
  and zooming out. The coffee-cup-to-kitchen progression worked well.
  Abstract-first explanations don't land.
- **Methodical.** Has a solid workflow: notebook first, then Mermaid,
  then commit. This discipline is a real asset for modeling work.
- **High volume of practice.** Has completed 10+ state diagrams, 5 class
  diagrams, and a full multi-scenario sequence diagram. Repetition
  across domains is building real pattern recognition.
- **Asks for help when stuck** instead of spinning or guessing silently.
  This is a strength, not a weakness — use it.
- **Applies corrections immediately.** When shown a mistake (wrong arrow
  direction, redundant attribute), she fixes it and doesn't repeat it
  in the same session.
- **Recognizes reusable patterns.** Spotted that "cleaning complete" was
  the same stop-dock-charge sequence as "battery low" on her own.

### Where she needs support

- **Confidence drops fast on unfamiliar ground.** When a task feels new
  or unclear, she tends to say "I don't know how" and ask for the full
  answer instead of trying a partial one. The right move: break it into
  a smaller first step she can attempt, not give the whole thing.
- **"Just tell me" reflex.** Under frustration she'll ask for the
  complete solution ("mi fai il codice completo?"). Don't comply — give
  a starting point and let her build from it. She learns nothing from
  copying and she knows it.
- **Properties vs. values confusion.** Tends to write the value where
  the property name should go ("full of coffee" instead of
  "content: coffee"). Needs reminders to separate the label from the
  data.
- **Sequence diagram arrows.** Call (`->>`) vs. response (`-->>`) is a
  recurring mistake, especially when a call has `()` parentheses. Worth
  checking every time.
- **Jumps to syntax before planning logic.** Wants to write Mermaid
  before describing the flow in plain words. Always ask her to describe
  the scenario in her own words first, then translate.
- **Needs domain knowledge to model.** If she doesn't know how the
  real-world thing works (e.g., "I don't know how a robot vacuum
  works"), she can't model it. Brief, simple explanations of the domain
  unlock her — she doesn't need a manual, just the key moving parts.
- **Gets overwhelmed by too many open tasks.** When shown a long list of
  things still to do, energy drops. Pick one thing, finish it, commit
  it. Then pick the next.

### Teaching style that works

- Socratic, but with guardrails. Ask her questions, but if she's stuck
  for more than one exchange, give a concrete starting point (first
  line, first arrow, first entity) — not the whole answer.
- One scenario / one diagram / one concept at a time.
- Always tie new syntax to something she's already done: "this works
  like the alt block in the vacuum scenario."
- Celebrate when she spots patterns or catches her own mistakes.
- When she says "che noia" or "sinceramente mi manca" — she's tired,
  not lazy. Simplify the next step or suggest stopping.

## Instructions for AI assistants

1. **Betta draws the diagram first.** Do not create diagrams yourself,
   not even as examples or starting points.
2. **Review together.** Discuss, ask questions, point out edge cases —
   but get confirmation before anything is final.
3. **Implementation comes last.** Only after a diagram is confirmed.
4. **Never invent the model.** No state diagrams, class diagrams, or
   transition tables created by the AI.
5. **Keep diagram and code in sync.** If they diverge, that's a bug.

The modeling is hers. The AI helps with syntax, review, tooling, and
implementation — not with design decisions.

## Resources

- https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-class-diagram-tutorial/
- https://www.visual-paradigm.com/guide/data-modeling/what-is-entity-relationship-diagram/
- https://blog.wu-boy.com/2026/04/api-cli-skills-architecture-for-ai-agents-en/