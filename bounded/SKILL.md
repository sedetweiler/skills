---
name: bounded
description: Keep tool results small when inspecting large files, searching repositories, discovering tools, or running verbose commands. Use to prevent context flooding while retaining complete evidence and following up on omitted results. Does not shorten requested deliverables or replace required reading.
license: MIT
metadata:
  author: Scott E. Detweiler
---

# Bounded output

Limit what enters the conversation, not the investigation. This skill guides tool
use; it is not a runtime hook or an enforced token limit.

## Before a call

- Decide what fact the result must establish. Request only the fields, files, or
  lines that can answer it.
- Start around 2,000 output tokens where the tool supports that limit; otherwise
  start with 150-200 lines or a few kilobytes. Increase for necessary context.
  Shrink individual budgets when batching, aiming around 4,000 tokens combined.
  Include results bundled by orchestration code in that total. Tool caps are a
  backstop, not a substitute for narrowing the command itself.
- Batch independent reads, but give each result a budget. Do not combine several
  long documents into one response that truncates before the later documents.

## Choose the smallest useful result

- **Search:** scope `rg` to likely paths and file types. Use `rg --files -g 'pattern'` for names,
  `rg -l` for files containing a match, and `rg -n` for relevant lines. Remember
  `rg -m` limits matches per file, not the entire result. Narrow further or save
  large result sets locally and inspect them in pages.
- **Files:** locate the symbol or section, then read a numbered range with enough
  surrounding context to understand it. Read small files directly. Expand across
  function boundaries, callers, and error paths when needed for correctness.
  Line limits do not bound minified code, single-line JSON, or encoded payloads;
  select fields or use a clearly labeled character-bounded preview instead.
- **Diffs/history:** start with scoped `git diff --stat` or `--name-only` and
  bounded `git log -n N --oneline` queries. Read per-file diffs next. A complete
  review still covers the entire changed surface, in pieces when necessary.
- **Tool discovery:** first filter tool names and short metadata. Print the full
  description/schema only for selected tools. Never dump an entire registry just
  because many descriptions contain a broad keyword.
- **Structured responses:** select necessary fields and paginate. For full issue
  histories or other required snapshots, retain the complete response locally
  and inspect current scope plus relevant changes. Do not print the whole object.
- **Tests/builds/logs:** capture verbose output to a private temporary log when
  practical. Report the command's actual exit status, summary, and relevant error
  excerpts. Preserve that status when redirecting output. Do not pipe a running
  test or build into `head`; it can terminate the producer or hide its failure.
  For shell-side capture, `if command > "$log" 2>&1; then rc=0; else rc=$?; fi`
  retains failure status even with `set -e`; report or exit with `$rc` afterward.
- **Counts/status/polling:** compute counts or existence locally instead of printing
  every item. Distinguish no matches from command failure (`rg`: 1 versus 2).
  For long-running work,
  return new output or changed status rather than replaying the accumulated log.

## Completeness and recovery

- Mandatory bootstrap, policy, and skill reading still means reading the required
  content. Split long documents into consecutive ranges and track completion;
  a truncated response or summary is not a completed read.
- Treat truncation as missing evidence. Retrieve the missing portion or narrow
  the query before making a conclusion. Never call a preview exhaustive or infer
  absence from omitted matches, pages, or log lines.
- Keep exact source evidence for edits and debugging. Do not introduce a model
  summarizer, extra agent, or repeated command run merely to shorten output.
- When an excerpt omits relevant material, state its scope and retain the full
  evidence path if one was created. Avoid storing credentials or unnecessarily
  duplicating sensitive content. Use existing approved snapshots where possible.
- Stop fetching when the question is answered and required checks are complete.
  These defaults do not limit the user's requested report, code, or explanation.
