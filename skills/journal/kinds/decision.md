# decision

The case file for a choice with consequences: the path taken, the alternatives rejected, and
why. Under debate it is `status: provisional`; once committed, `confirmed`.

Worth capturing - include what applies, and anything else that matters:

- what forced the choice
- what was chosen
- the alternatives rejected, and why they lost - usually the most valuable part, it survives
  nowhere else
- consequences already foreseen

Keep one decision per entry - one loser, one choice. If a session settles several choices, that
is several `decision` entries, because `supersedes` reverses a whole file: a bundle cannot have
one choice reversed without orphaning the others that are still true.

A reversal later is a new `decision` with `supersedes`; a consequence that surfaces later is a
new entry with `consequence-of`.
