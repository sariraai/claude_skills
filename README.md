# Claude Code Skills

Open-source skills for [Claude Code](https://claude.ai/claude-code), Anthropic's CLI tool for AI-assisted development and writing.

## What Are Skills?

Skills are instruction files that teach Claude Code how to perform specialized tasks. Drop a skill into your project's `.claude/skills/` directory and Claude learns the capability — no coding required.

## Available Skills

### copy-editor

Evidence-based copyediting for grammar, punctuation, usage, and consistency. Runs three passes on your prose:

1. **Usage** — Catches word-level errors (affect/effect, it's/its, comma splices, malaprop pairs)
2. **Grammar** — Catches sentence-level errors (subject-verb agreement, dangling modifiers, pronoun case)
3. **Consistency** — Catches document-level drift (terminology variations, formatting inconsistencies)

**What makes this different from "check my grammar":**
- Won't enforce zombie rules (split infinitives, sentence-ending prepositions, singular they)
- Distinguishes hard errors from contested usage from judgment calls
- Preserves your voice — fixes mechanics without changing how you sound
- Shows its reasoning for every flag

**Output:** A summary of issues found, plus your full text with `==highlighted==` annotations showing what to fix and why.

## Installation

1. Navigate to your project folder
2. Create the skills directory if it doesn't exist:
   ```bash
   mkdir -p .claude/skills
   ```
3. Copy the skill folder into it:
   ```bash
   cp -r copy-editor .claude/skills/
   ```
4. Run Claude Code:
   ```bash
   claude
   ```
5. Use the skill:
   ```
   /copy-editor path/to/your-document.md
   ```
   Or just say: "Copy edit this chapter" / "Proofread this file"

## Requirements

- [Claude Code](https://claude.ai/claude-code) (requires Claude Pro or Max subscription)
- That's it

## Attribution

The copy-editor skill is based on the principles in Steven Pinker's *The Sense of Style* (2014), particularly the framework for distinguishing genuine errors from zombie rules through evidence, logic, and historical awareness. The skill was developed by [Sixnatures Publishing](https://sixnatures.com) as part of our editorial pipeline and released as open source for the community.

## Contributing

We welcome contributions. Here's how you can help:

**Add coverage for issues the skill misses:**
- Run the skill on your own writing
- If it misses something that a good copyeditor would catch, open an issue describing the error type
- Bonus: propose the check with examples (wrong, right, test) following the format in the existing tables

**Improve existing checks:**
- If the skill flags something it shouldn't (false positive), open an issue with the passage and why the flag is wrong
- If the confidence level feels off (flagged as HARD ERROR but should be JUDGMENT), let us know

**Add new skills:**
- Fork the repo and add your own skill to a new folder
- Follow the SKILL.md format: frontmatter with name/description, clear instructions, examples
- Submit a PR with a brief description of what your skill does

**Style guide variants:**
- The current disputed usage stances reflect Pinker's evidence-based positions
- If you work in a field with different conventions (legal, medical, academic), consider contributing a style-guide overlay that adjusts the house stances

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — use, share, and adapt freely. Just give credit to Sixnatures Publishing.

## Author

Developed by [Sixnatures Publishing](https://sixnatures.com)

Follow the development on [Sarira Substack](https://sarira.substack.com)
