# plan

An ordered set of phases for a large change, captured while the work is still in flight. The plan
is self-contained - it is the executor's prompt, meant to be run with nothing else in hand. Always
`status: provisional` - it is a proposal until it is run, superseded when it lands (a development
`summary`) or is abandoned (a `tombstone`). It consolidates decisions already made into a runnable
order; it does not re-make them.

A plan is only a plan when its phases carry criteria: each phase states how it is known to be done,
so the work can advance, and what makes it stop and return to the operator. Without those it is a
bare task list, which belongs in a tracker, not the journal - reclassify or do not write it.

Because it runs itself, the plan carries its execution rules - the standing instructions to
whoever runs it, written into the document so nothing else is needed in hand:

- work the phases in order
- advance to the next phase only once the current phase's done-when is met
- do not pause between phases unless a stop-when fires
- on a stop-when, stop and return to the operator; the operator resolves any plan-versus-reality
  conflict, not the agent
- keep the codebase working between phases
- capture what surfaces while running as journal entries - a finding as a `reminder`, a forced
  choice as a `decision`, a killed approach as a `tombstone` - each referencing the plan
- run the manual test at the end and hand it to the operator
- close the plan with a development `summary` that supersedes it

Worth capturing across the whole plan - include what applies, and anything else that matters:

- the goal in a line, and the architecture in a few sentences
- the constraints that hold for every phase, and what the plan will not touch - its blast radius
- the green baseline it starts from - the tests or checks that must stay passing throughout
- the decisions it consolidates, referenced by path, not re-argued

Each phase (the shape is the agent's, not a template):

- its intent, in a line
- what it touches, and what it must not
- what it needs from earlier phases, and what later phases rely on from it
- done-when: a measurable, verifiable condition, fixed before the phase runs, not "looks right"
- stop-when: the conditions that break the phase and return it to the operator, naming what was
  touched so it can be reversed - on a plan-versus-reality conflict the operator decides, not the agent
- how the phase is undone, leaving the codebase working between every phase

Every plan contains a manual test - how its result gets checked by hand at the end. This is not
one of the phases and carries no done-when or stop-when; it is the plan's standing promise that a
human verifies the outcome, not the agent. Give the operator a concrete scenario to run; their
notes return into the development `summary`, or stand as a cited `source` when the raw report is
worth keeping whole.

Keep out what goes stale or lives elsewhere: no code, pseudo-code, or algorithms - a snippet that
is itself a decision belongs in that `decision` entry, cited `path@sha`; no copied documentation or
interface definitions - reference them by path, inline only what is short enough not to flood; no
live progress or status - that is the tracker's job, not the record's.

A plan lives through what its execution emits, not by being rewritten - the entries it spawns while
running (see the execution rules) are its real trace. It closes on a hinge: the development
`summary` that `supersedes` it records what happened phase by phase, the outcome, and the
operator's test notes, while the threads it opened live on as the entries it points to.

Before writing a plan the agent may interview the operator, but only for what the code and the
journal cannot answer: explore first, then ask one question at a time, each with a recommended
answer, and only when offered - never to fill a form.
