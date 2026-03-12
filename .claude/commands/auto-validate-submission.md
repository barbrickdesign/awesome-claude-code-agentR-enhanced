# Auto-Validate Submission

Perform a deep, automated validation of a pending resource submission before it is committed to the CSV.

## Instructions

Given a resource submission (from a GitHub issue or provided directly), perform the following checks in order and produce a structured validation report.

### 1. URL Reachability
- Confirm the primary link returns HTTP 200 (or appropriate redirect).
- If the URL points to GitHub, confirm the repository exists and is public.
- Confirm any secondary link is also reachable.

### 2. Duplicate Detection
- Search `THE_RESOURCES_TABLE.csv` for any row whose `Primary Link` or `Display Name` matches (or is very similar to) the submission.
- Flag near-duplicates (fuzzy name match ≥ 80%) for human review, not automatic rejection.

### 3. Category Validity
- Confirm the submitted `Category` exists in `templates/categories.yaml`.
- If a `Sub-Category` is provided, confirm it is a valid subcategory of the chosen category.
- Suggest the most appropriate category/subcategory if the submitted one looks wrong.

### 4. License Detection
- If the URL is a GitHub repository, use the GitHub API (`/repos/{owner}/{repo}/license`) to detect the license automatically.
- Compare with the submitter-declared license; flag mismatches.
- Accept "No License / Not Specified" if the API returns no license.

### 5. Description Quality
- Confirm the description is between 10 and 500 characters.
- Flag descriptions that are clearly promotional ("the best", "amazing", "revolutionary") rather than descriptive.
- Flag descriptions that contain emojis (per list style guide).
- Flag descriptions that address the reader directly (e.g., "you can use this to…").

### 6. Multi-LLM Compatibility Check
- Inspect the repository README (if GitHub) for mentions of supported LLMs/tools.
- Note which LLMs/tools the resource explicitly supports or is compatible with.
- Suggest the `Multi-LLM Tools` category if the resource clearly works with multiple providers.

### 7. Security Red Flags
- Flag if the README or description mentions:
  - `--dangerously-skip-permissions` or equivalent bypass flags
  - Telemetry, analytics, or data collection
  - Network calls beyond the declared AI provider API
  - Auto-update mechanisms (`npx @latest`, `pip install --upgrade`, etc.)
  - Shell scripts that are not clearly documented

### 8. Age Check
- If the URL is a GitHub repository, confirm the repository creation date is at least 7 days before today.

## Output Format

Produce a Markdown report with the following sections:

```markdown
## Validation Report: {Display Name}

**Submitted Category:** {category} / {subcategory}
**Submitted License:** {license}

### ✅ Checks Passed
- (list each passing check with a brief note)

### ⚠️ Warnings (require human review)
- (list any warnings with details)

### ❌ Failures (block submission)
- (list any hard failures with details)

### 📋 Enriched Data
- **Detected License:** {detected_license}
- **Detected LLM Targets:** {comma-separated list}
- **Repository Created:** {date}
- **Last Modified:** {date}

### 🏷️ Category Suggestion
{Suggested category/subcategory if different from submitted, with reasoning}

### 🔒 Security Notes
{Any security observations}
```

A submission passes validation only if there are **zero ❌ Failures**.
Warnings must be reviewed by the maintainer before approval.

## Usage

```
/auto-validate-submission
```

Then paste the raw issue body, or provide the issue number and the tool will fetch it automatically.

Alternatively:

```
/auto-validate-submission <primary_url> [--name "Resource Name"] [--category "Category"]
```
