# Contributing to Awesome AI Code Agents

Please take a moment to read through this document if you plan to submit something for recommendation.

> [!WARNING]
> Due to aggressive spamming of the repository's recommendation system, strict measures are in place to ensure that submissions are made according to the requirements stated in this document. The penalties are harsh, but compliance is very easy, and any well-meaning user who reads this document is unlikely to be affected.

- I am very grateful to receive recommendations from the visitors to this list. But be aware that there is no formal submission/review process at the moment. My responsibility is to share links to awesome things. One way I find out about awesome things is via the repo's issues, and I'm very grateful to everyone who shares their amazing work. But it's not the only way, and creating an issue does not represent any sort of contract.
- Bear in mind that the point of an Awesome List is to be *selective* — I cannot recommend every single resource that is submitted.
- This list covers resources for **all major LLM-powered coding tools** — Claude Code, OpenAI Codex / ChatGPT, Gemini, GitHub Copilot, Cursor, Windsurf, Cline, Aider, Continue, and more. Resources that are LLM-agnostic (work with any provider) are especially welcome.
- I'm constantly trying to improve the way in which recommendations can be submitted, and to provide clear guidance to users who wish to share their work. Here are some of those guidelines:
    - Security is of the utmost importance. I'm unlikely to install any software unless I have high confidence that it is free of malware, spyware, adware, or bloat. If a resource involves executing a shell script, for example, it is recommended to supply clear and thorough comments explaining exactly what it does.
    - If your library makes any network calls except to the intended AI provider API; modifies shared system files; involves any form of telemetry; or requires dangerous permission bypass modes, this must be stated very clearly.
    - Do not submit resources that do not comply with the licensing rights of other developers. Make sure you understand what OSS licenses require.
    - I value _focused_ resources with a clear purpose and use value. Even if you have a marketplace full of awesome plugins, you are encouraged to select one, or a small subset.
    - Claims about what a resource does have to be evidence-based — and you should not expect me, or probably any user, to do the work of proving it themselves. Provide instructions for validating the claims made in the description, and make them as detailed as possible.
    - Put a tiny bit of time and effort into your README.

## Supported Categories

Resources can be submitted under any of the following categories:

| Category | Description |
|----------|-------------|
| **Agent Skills** | Model-controlled files/scripts enabling specialized agent tasks |
| **Workflows & Knowledge Guides** | Tightly coupled sets of agent-native resources |
| **Tooling** | Applications built on top of AI coding agents |
| **Multi-LLM Tools** | Tools that work across multiple LLM providers |
| **Prompt Engineering** | Prompt libraries, templates, and techniques for any LLM |
| **Status Lines** | Status bar configurations for AI coding agents |
| **Hooks** | Lifecycle hooks for AI coding agent events |
| **Slash-Commands** | Custom command prompts for AI coding agents |
| **CLAUDE.md Files** | Context/instruction files for Claude Code |
| **Agent Configuration Files** | `AGENTS.md`, `.cursorrules`, Copilot instructions, and similar files for other LLMs |
| **Alternative Clients** | Alternative UIs and front-ends for LLMs |
| **Official Documentation** | Official docs from AI providers |

## How to Recommend a Resource

**NOTE: ALL RECOMMENDATIONS MUST BE MADE USING THE WEB UI ISSUE FORM TEMPLATE, OR YOU RISK BEING BANNED FROM INTERACTING WITH THIS REPOSITORY TEMPORARILY OR PERMANENTLY.**

First, make sure you've read the above information. Second, make sure you've read, and agree with, the [Code of Conduct](./CODE_OF_CONDUCT.md). Then:

### **[Click here to submit a new resource](https://github.com/hesreallyhim/awesome-claude-code/issues/new?template=recommend-resource.yml)**

Do not open a PR. Just fill out the form. If there are any issues with the form, the bot will notify you.

> [!Warning]
> It is **not** possible to submit a resource recommendation using the `gh` CLI.

Although resources themselves may be partially or entirely written by a coding agent, resource recommendations must be created by human beings.

### The Recommendation Process

The entire recommendation process is managed via automation — even the maintainer does not use PRs to add entries to the list. The bot is really good at it. Here's what happens when you submit a resource for recommendation:

```mermaid
graph TD
    A[📝 Fill out recommendation form] --> B[🤖 Automated validation]
    B --> C{Valid?}
    C -->|❌ No| D[Bot comments with issues]
    D --> E[Edit your submission]
    E --> B
    C -->|✅ Yes| F[Awaits maintainer review]
    F --> G{Decision}
    G -->|👍 Approved| H[Bot creates PR automatically]
    G -->|🔄 Changes requested| I[Maintainer requests changes]
    G -->|👎 Rejected| J[Issue closed]
    I --> E
    H --> K[PR merged]
    K --> L[🎉 Resource goes live!]
    L --> M[You receive notification]
```

### What the Bot Validates

When you submit a resource, the bot checks:

- All required fields are filled
- URLs are valid and accessible
- No duplicate resources exist
- License information (when available)
- Description length and quality

The bot's validation is not any sort of review. It's merely a formal check.

## Other Contributions

### Suggesting Improvements

For suggestions about the repository structure, new categories, or other enhancements:

1. **[Open a general issue](https://github.com/hesreallyhim/awesome-claude-code/issues/new)**
2. Describe your suggestion clearly
3. Explain the benefit to the community

Or, alternatively, start a thread in the [Discussions](https://github.com/hesreallyhim/awesome-claude-code/discussions) tab. All opinions are welcome in this repo so long as they are expressed in accordance with the Code of Conduct. It's very nice to interact with people who visit the list.

## Badges

If your submission is approved, you are invited to add a badge to your project's README:

[![Mentioned in Awesome AI Code Agents](https://awesome.re/mentioned-badge.svg)](https://github.com/hesreallyhim/awesome-claude-code)

```markdown
[![Mentioned in Awesome AI Code Agents](https://awesome.re/mentioned-badge.svg)](https://github.com/hesreallyhim/awesome-claude-code)
```

Or the flat version:

[![Mentioned in Awesome AI Code Agents](https://awesome.re/mentioned-badge-flat.svg)](https://github.com/hesreallyhim/awesome-claude-code)

```markdown
[![Mentioned in Awesome AI Code Agents](https://awesome.re/mentioned-badge-flat.svg)](https://github.com/hesreallyhim/awesome-claude-code)
```

## GitHub Repository Notifications

If your resource is on GitHub, our automated system will create a friendly notification issue on your repository informing you of the inclusion and providing badge options.

## Technical Details

For more information about how the repository works, including the automated systems, validation processes, and technical architecture, see the documents in `docs/` — in particular `README_GENERATION`.

---

Thank you for taking the time to read this and to share your project (or any project).
