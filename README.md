# Scott's AI Skills

This is where I share the skills I create to make working with AI agents a little more useful, thoughtful, and efficient.

These skills grow out of everyday work: noticing something an agent keeps getting wrong, finding a better approach, and writing it down so the next session starts a little wiser. I'm sharing them here in the hope that they help you, too.

Take a look around, try what fits your workflow, and make it your own. I'll add more as I create and refine them.

## Available skills

| Skill | What it helps with |
| --- | --- |
| [Bounded](bounded/SKILL.md) | Keeps tool output focused when an agent searches a repository, reads files, inspects logs, or runs commands. |

## Meet Bounded

A useful answer can get buried under thousands of lines of tool output. Bounded encourages agents to ask for the evidence they need, keep complete logs available, and expand their reading when correctness calls for it.

Its guiding idea is simple:

> Limit what enters the conversation, not the investigation.

That means finding the relevant function before reading a large file, keeping full test logs while reporting the result, and following up whenever an excerpt leaves an important question unanswered. Required reading stays required, and requested answers stay complete.

Bounded is a set of instructions, not an enforced token limit. Any savings depend on the task, the tools, and how well the agent follows the guidance.

Early results have been encouraging. In my own development sessions, the latest cumulative estimate showed about 14% less tool-output text across nearly 1,000 outputs compared with an earlier baseline. This is an informal comparison, not a controlled benchmark or a measurement of total token or billing savings.

## Getting started

1. Clone or download this repository.
2. Copy the entire folder for the skill you want, including its license, into your agent's skills directory.
3. Follow your agent's instructions for discovering or enabling skills.

Each skill uses the [Agent Skills format](https://agentskills.io/specification), with its instructions in `SKILL.md`. Installation locations and activation methods vary between tools.

For everyday use, add a short standing instruction to your agent's startup instructions, such as [AGENTS.md for Codex](https://learn.chatgpt.com/docs/agent-configuration/agents-md) or [CLAUDE.md for Claude Code](https://code.claude.com/docs/en/memory). That saves you from repeating the request in every prompt. Reference the installed skill rather than copying its full contents into the startup file.

For example, replace `<skills-directory>` with your actual installation path:

```text
Use the bounded skill at <skills-directory>/bounded/SKILL.md by default for
repository searches, file reads, tool discovery, and verbose commands.
Read the skill before applying it. Keep output focused, retain full logs
when needed, and expand your reading whenever correctness requires it.
```

You can also ask for Bounded in an individual prompt when you only want it for a particular task.

## Feedback

If you try a skill, I'd love to hear what worked and what felt awkward. [Open an issue](https://github.com/sedetweiler/skills/issues) with your feedback or an example that could make it better.

## License

Created and maintained by Scott E. Detweiler. Shared under the [MIT License](LICENSE).

You're welcome to use these skills, adapt them, and include them in your own projects, including commercial work. Keep the copyright and license notices with copies you share.
