# source

A verbatim external artifact - an email, call transcript, incoming spec, client feedback, or
task - received, not authored. Kept unedited so other entries can cite it; it is the root of the
reference graph. Default `status: confirmed`.

Beyond the shared frontmatter, a source carries:

- `medium` - email | call-transcript | spec | feedback | task | message
- `origin` - who or where it came from
- `received` - the date the artifact arrived

Worth capturing - include what applies, and anything else that matters:

- a line of context: what this is and what it feeds
- the artifact itself, pasted verbatim - never summarize, paraphrase, or tidy it

Redact secrets and PII before saving, marking each cut. A summary of the artifact is a separate
entry that carries `sourced-from` back here; a revised version is a new `source` that supersedes
this one.
