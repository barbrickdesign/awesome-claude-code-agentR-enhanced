# Find Duplicate Resources

Scan `THE_RESOURCES_TABLE.csv` and identify potential duplicate or near-duplicate entries, then produce a deduplicated candidate list.

## Instructions

### 1. Exact Duplicate Detection
Find rows in `THE_RESOURCES_TABLE.csv` where:
- `Primary Link` values are identical (after normalising trailing slashes and URL schemes)
- `Display Name` values are identical (case-insensitive)

Report these as **hard duplicates** — they must be resolved before any new submission with the same values can be accepted.

### 2. Near-Duplicate Detection
Apply the following similarity checks across all active rows:

#### URL Similarity
- Strip trailing `/`, normalise `http://` → `https://`, and compare
- Treat `github.com/owner/repo` and `github.com/owner/repo/tree/main` as the same repository
- Flag pairs where the normalised URLs differ only in path suffix (e.g., `/blob/main/README.md` vs root)

#### Name Similarity
- Compute Levenshtein distance between all `Display Name` pairs
- Flag pairs with similarity ≥ 80% (configurable via `--threshold`)
- Also flag pairs that share all significant words (ignoring common words like "the", "a", "for", "claude", "code")

#### Description Similarity
- Flag pairs whose `Description` values share more than 70% of unique content words
- This catches cases where the same tool was submitted twice with slightly different names

### 3. Same-Author Multiple Entries
List all authors with more than one entry in the same category — not necessarily duplicates, but worth reviewing.

### 4. Redirect Detection (optional, requires network access)
If `--check-redirects` is passed, follow HTTP redirects for all primary links and flag any two resources that redirect to the same final URL.

## Output Format

```markdown
# Duplicate Resource Report — {date}

## Hard Duplicates (identical URL or name)
| ID A | ID B | Display Name | Primary Link | Recommendation |
|------|------|--------------|--------------|----------------|
| ...  | ...  | ...          | ...          | Remove ID B    |

## Near-Duplicate Candidates (similarity ≥ {threshold}%)
| ID A | Name A | ID B | Name B | Similarity | Reason | Action |
|------|--------|------|--------|------------|--------|--------|
| ...  | ...    | ...  | ...    | 85%        | Name   | Review |

## Same-Author, Same-Category Entries
| Author | Category | Resources |
|--------|----------|-----------|
| ...    | ...      | [Name A](link), [Name B](link) |

## Summary
- Hard duplicates found: {n}
- Near-duplicate candidates: {n}
- Same-author/category pairs: {n}

## Recommended Actions
1. {specific action for each hard duplicate}
2. {note on near-duplicates requiring human review}
```

## Usage

Basic scan:

```
/find-duplicate-resources
```

Adjust similarity threshold (default 80%):

```
/find-duplicate-resources --threshold 70
```

Include redirect checking (requires network access):

```
/find-duplicate-resources --check-redirects
```

Check a specific new submission against the list before adding it:

```
/find-duplicate-resources --check-new "https://github.com/owner/repo" "My Resource Name"
```
