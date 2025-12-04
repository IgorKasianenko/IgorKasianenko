# If you are using coding assistants, you should know this. 

LLMs don't have state. Every time you start a new chat - it needs all the content you can provide. Andrii Vysotskyi inspired me to share some key findings about copilot behaviour in Warp, Claude Code and GitHub Copilot. 

If you get a feeling "finally the AI gets me and does what I imagined to do" - usually it is somewhere after 5 follow up questions when every request. Writing a big system prompt with all your preferences is good, but sometimes it is not enough. 

Remember the basics - LLMs predict the next token based on all previous input. On your first question all it gets - system prompt (if you created one), assistant specific instructions like `CLAUDE.md`, your question. Enhancing it with context files changes everything.

## What actually works

Create `CLAUDE.md` in your repo root. Put your architecture there. Your conventions. Your "why we did it this way" decisions. Reference it first thing in every conversation.

Same goes for Warp workflows and amp system files. These tools read specific files to understand your project. Use them.

Split your context into focused files:
- `CLAUDE.md` - Core project context
- `docs/architecture.md` - System design
- `docs/conventions.md` - Code standards
- `.github/ai-context.md` - Workflow patterns

## The pattern

The first message should be "read CLAUDE.md and help me with X". Not just "help me with X". That one file reference can save you 5 rounds of back and forth.

Your context files should answer:
- What stack we use
- How we structure code
- What patterns we follow
- What we explicitly avoid

Update them when you make architectural decisions. Keep each under 2000 words. Make them scannable.

## Bottom line

LLMs are stateless. Your context files are the state. Build them once, reference them always. Your first AI response will be better than your fifth used to be.

Stop reexplaining your codebase every session. Write it down once. Reference it every time.

