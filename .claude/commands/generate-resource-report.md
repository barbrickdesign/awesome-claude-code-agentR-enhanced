# Generate Resource Report

Generate a comprehensive analytics and health report for all resources in `THE_RESOURCES_TABLE.csv`, or for a filtered subset.

## Instructions

Read `THE_RESOURCES_TABLE.csv` and produce a structured report covering the following dimensions.

### 1. Overview Statistics
- Total number of active resources
- Total number of inactive/removed resources
- Breakdown by category (count per category, percentage of total)
- Breakdown by sub-category
- Breakdown by license type
- Number of GitHub vs non-GitHub resources

### 2. LLM Coverage Analysis
- For each major LLM/tool (Claude Code, OpenAI Codex, Gemini, Copilot, Cursor, Windsurf, Cline, Aider, Multi-LLM), count how many resources target it
- Identify the most under-served LLMs/tools
- List "Multi-LLM Tools" category resources specifically

### 3. Freshness & Activity
- Resources added in the last 7 days / 30 days / 90 days
- Resources not modified in the last 180 days (potentially stale)
- Resources with a `Latest Release` in the past 30 days
- Resources with `Removed From Origin = TRUE` that are still `Active` (data inconsistency)

### 4. Quality Signals
- Resources with no license specified ("No License / Not Specified")
- Resources with descriptions under 20 characters or over 400 characters
- Resources with a `Stale = TRUE` flag
- Resources with broken/missing secondary links

### 5. Author & Community Health
- Total unique authors
- Authors with 2+ resources in the list
- Resources submitted in the past 30 days that are still awaiting merging (if issue data is available)

### 6. Category Gap Analysis
- Categories that exist in `templates/categories.yaml` but have fewer than 3 resources
- Suggested new subcategories based on patterns in existing resource descriptions
- Categories with the most recent additions (momentum indicators)

### 7. Top Resources (by GitHub Stars, if available)
- Top 10 resources by star count (from `Repo Created` / GitHub data)
- Top 10 most recently released resources

## Output Format

Produce a Markdown report:

```markdown
# Resource Report — {date}

## Overview
- **Total Active Resources:** {n}
- **Total Inactive Resources:** {n}
- **Categories:** {n}

## Category Breakdown
| Category | Count | % of Total |
|----------|-------|------------|
| ...      | ...   | ...        |

## LLM Coverage
| LLM / Tool | Resource Count | Coverage |
|------------|----------------|----------|
| ...        | ...            | ...      |

## Freshness
- Added last 7 days: {n}
- Added last 30 days: {n}
- Not modified in 180+ days: {n}
- Recent releases (30 days): {n}

## Quality Signals
- No license specified: {n} resources
- Short descriptions (<20 chars): {n} resources
- Long descriptions (>400 chars): {n} resources
- Stale flag set: {n} resources

## Community Health
- Unique authors: {n}
- Authors with 2+ resources: {list}

## Category Gaps (< 3 resources)
{list of under-populated categories/subcategories}

## Top 10 by Stars
{table}

## Recommendations
{Actionable suggestions for improving list quality and coverage}
```

## Usage

```
/generate-resource-report
```

Filter to a specific category:

```
/generate-resource-report --category "Multi-LLM Tools"
```

Filter by LLM target keyword:

```
/generate-resource-report --llm "Gemini"
```

Export as CSV:

```
/generate-resource-report --format csv
```
