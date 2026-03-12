# Multi-LLM Compatibility Check

Analyse a resource (repository, file, or URL) and determine which LLM-powered coding tools it is compatible with, and identify gaps or improvements that would make it work across more providers.

## Instructions

Given a resource (repository URL or local path), perform the following analysis:

### 1. Declared Compatibility
- Inspect the README, documentation, and any configuration files for explicit mentions of:
  - Claude Code / Anthropic
  - OpenAI Codex / ChatGPT / GPT-4
  - Gemini / Google AI Studio / Vertex AI
  - GitHub Copilot
  - Cursor
  - Windsurf
  - Cline
  - Aider
  - Continue
  - Llama / Ollama / local models
  - Mistral
  - Grok (xAI)
- Summarise which providers/tools are explicitly supported.

### 2. Implicit Compatibility
- Check for provider-specific APIs, SDKs, or configuration formats:
  - `CLAUDE.md` → Claude Code only
  - `AGENTS.md` → OpenAI Codex / general
  - `.cursorrules` / `cursor.rules` → Cursor
  - `.windsurfrules` → Windsurf
  - `.clinerules` → Cline
  - `.github/copilot-instructions.md` → GitHub Copilot
  - `anthropic` / `claude` imports → Anthropic SDK
  - `openai` imports → OpenAI SDK
  - `google.generativeai` / `vertexai` imports → Google AI
- List detected provider-specific dependencies.

### 3. Portability Assessment
Rate the resource's portability on a 1–5 scale:
- **5 - Fully Portable**: Works with any LLM, no provider-specific code
- **4 - Mostly Portable**: Minor provider-specific elements, easily adapted
- **3 - Partially Portable**: Works with 2–3 providers with moderate changes
- **2 - Provider-Coupled**: Significant refactoring required for other providers
- **1 - Provider-Locked**: Tightly coupled to a single provider's API/format

### 4. Adaptation Recommendations
For each gap identified, provide a specific, actionable recommendation:
- What file(s) to create/modify
- What content to add
- Which LLM/tool would become compatible as a result
- Estimated effort (low / medium / high)

### 5. Configuration File Generation (optional)
If the resource is a skill, workflow, or prompt collection that uses a single-provider configuration file, offer to generate equivalent configuration files for other providers:
- If `CLAUDE.md` exists → offer to create `AGENTS.md` (OpenAI), `.cursorrules` (Cursor), `.windsurfrules` (Windsurf), `.clinerules` (Cline), `.github/copilot-instructions.md` (GitHub Copilot)
- If a slash-command exists for Claude Code → offer to port it to equivalent formats for other tools

## Output Format

```markdown
## Multi-LLM Compatibility Report: {Resource Name}

### Declared Support
| Provider / Tool | Explicitly Supported |
|-----------------|---------------------|
| Claude Code     | ✅ / ❌ / ⚠️ partial |
| OpenAI Codex    | ✅ / ❌ / ⚠️ partial |
| Gemini          | ✅ / ❌ / ⚠️ partial |
| GitHub Copilot  | ✅ / ❌ / ⚠️ partial |
| Cursor          | ✅ / ❌ / ⚠️ partial |
| Windsurf        | ✅ / ❌ / ⚠️ partial |
| Cline           | ✅ / ❌ / ⚠️ partial |
| Aider           | ✅ / ❌ / ⚠️ partial |
| Continue        | ✅ / ❌ / ⚠️ partial |
| Llama / Ollama  | ✅ / ❌ / ⚠️ partial |

### Portability Score: {X}/5 — {label}

### Provider-Specific Elements Detected
- {element}: {why it's provider-specific}

### Adaptation Recommendations
1. **{Recommendation title}** (effort: {low/medium/high})
   - Files to create/modify: `{filename}`
   - Change: {description}
   - Unlocks: {provider(s)}

### Suggested Category
{If the resource should be categorised as "Multi-LLM Tools" based on this analysis, say so with reasoning}
```

## Usage

```
/multi-llm-compatibility https://github.com/owner/repo
```

Or for a local path:

```
/multi-llm-compatibility ./path/to/resource
```

Add `--generate-configs` to automatically generate missing configuration files for other providers.
