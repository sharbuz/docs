# Validation Scripts

This directory contains Python scripts for validating commit messages and PR titles in GitHub Actions workflows.

## Scripts

### validate_commit.py

Validates commit message format and line length.

**Usage:**

```bash
python3 validate_commit.py \
  --pattern "^PROJ-\d+:.*" \
  --max-length 300 \
  --verbose
```

**Arguments:**

- `--pattern` (required): Regex pattern that commit message must match
- `--max-length` (optional): Maximum allowed line length (default: 300)
- `--commit-ref` (optional): Git reference to validate (default: HEAD)
- `--verbose` (optional): Enable verbose output

**Example:**

```bash
# Validate current commit
python3 validate_commit.py --pattern "^EPMCDME-\d+:.*" --max-length 300

# Validate specific commit
python3 validate_commit.py --pattern "^EPMCDME-\d+:.*" --commit-ref abc123
```

### validate_pr_title.py

Validates pull request title format and length using GitHub CLI.

**Usage:**

```bash
python3 validate_pr_title.py \
  --pattern "^PROJ-\d+:.*" \
  --max-length 300 \
  --pr-number 123 \
  --repo owner/repo \
  --verbose
```

**Arguments:**

- `--pattern` (required): Regex pattern that PR title must match
- `--pr-number` (required): Pull request number
- `--repo` (required): Repository in format 'owner/repo'
- `--max-length` (optional): Maximum allowed title length (default: 300)
- `--verbose` (optional): Enable verbose output

**Requirements:**

- GitHub CLI (`gh`) must be installed and authenticated
- `GH_TOKEN` environment variable must be set

**Example:**

```bash
export GH_TOKEN=your_token
python3 validate_pr_title.py \
  --pattern "^EPMCDME-\d+:.*" \
  --max-length 300 \
  --pr-number 42 \
  --repo epm/cdme-docs
```

## Local Testing

You can test these scripts locally before pushing:

```bash
# Test commit validation
python3 .github/scripts/validate_commit.py \
  --pattern "^EPMCDME-\d+:\s[A-Z][a-z].*" \
  --max-length 300 \
  --verbose

# Test PR validation (requires gh CLI and GH_TOKEN)
python3 .github/scripts/validate_pr_title.py \
  --pattern "^EPMCDME-\d+:\s[A-Z][a-z].*" \
  --max-length 300 \
  --pr-number 1 \
  --repo your-org/your-repo \
  --verbose
```

## Integration with GitHub Actions

These scripts are used in the validation workflows:

1. **Direct usage** (`.github/workflows/validation.yml`):
   - Scripts are called directly in workflow steps
   - Uses repository-specific configuration

2. **Reusable workflow** (`.github/workflows/validation-reusable.yml`):
   - Can be called from other repositories
   - Supports customizable parameters

See the workflows directory for usage examples.
