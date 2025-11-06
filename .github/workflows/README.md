# Validation Workflows

This directory contains GitHub Actions workflows for validating commits, PRs, and code quality.

## Workflows

### validation.yml

Main validation workflow for this repository. Runs on:

- Pull requests to `main` branch
- Pushes to `main` branch

This is a thin wrapper that calls `validation-base.yml` with this repository's specific configuration.

**Configuration:**
Edit the `with` parameters in the workflow file:

```yaml
jobs:
  validate:
    uses: ./.github/workflows/validation-base.yml
    with:
      commit_message_pattern: "^((EPMCDME)-\\d+:..."
      max_commit_length: 300
      node_version: '24'
```

---

### validation-base.yml

Base workflow that contains all validation logic. Can be called from other repositories.

**Usage in other repositories:**

1. **Copy the validation scripts** to your repository:

   ```bash
   # In your target repository
   mkdir -p .github/scripts

   # Copy scripts from this repo
   cp path/to/docs/.github/scripts/validate_commit.py .github/scripts/
   cp path/to/docs/.github/scripts/validate_pr_title.py .github/scripts/
   ```

2. **Create a workflow** in your repository (e.g., `.github/workflows/validation.yml`):

   ```yaml
   name: Validation

   on:
     pull_request:
       branches: [main]

   jobs:
     validate:
       uses: your-org/docs/.github/workflows/validation-base.yml@main
       with:
         # Customize for your project
         commit_message_pattern: "^MYPROJ-\\d+:.*"
         max_commit_length: 250
         node_version: '20'
         run_commit_validation: true
         run_pr_validation: true
         run_code_validation: true
   ```

**Available inputs:**

| Input                    | Type    | Default                   | Description                         |
| ------------------------ | ------- | ------------------------- | ----------------------------------- |
| `commit_message_pattern` | string  | `"^((EPMCDME)-\\d+:...$"` | Regex pattern for commit validation |
| `max_commit_length`      | number  | `300`                     | Maximum line length                 |
| `node_version`           | string  | `"24"`                    | Node.js version                     |
| `run_commit_validation`  | boolean | `true`                    | Enable commit validation            |
| `run_pr_validation`      | boolean | `true`                    | Enable PR title validation          |
| `run_code_validation`    | boolean | `true`                    | Enable code quality checks          |

---

## Examples

### Example 1: Use with default settings

```yaml
jobs:
  validate:
    uses: your-org/docs/.github/workflows/validation-reusable.yml@main
```

### Example 2: Customize pattern and length

```yaml
jobs:
  validate:
    uses: your-org/docs/.github/workflows/validation-reusable.yml@main
    with:
      commit_message_pattern: "^(feat|fix|docs|chore)\\(.*\\):.*"
      max_commit_length: 200
```

### Example 3: Skip code validation (commits/PRs only)

```yaml
jobs:
  validate:
    uses: your-org/docs/.github/workflows/validation-reusable.yml@main
    with:
      commit_message_pattern: "^PROJ-\\d+:.*"
      run_code_validation: false
```

### Example 4: Different Node.js version

```yaml
jobs:
  validate:
    uses: your-org/docs/.github/workflows/validation-reusable.yml@main
    with:
      node_version: '20'
```

---

## Migration Guide

### From inline scripts to extracted scripts

**Before:**

```yaml
- name: Validate commit
  run: |
    python3 << 'EOF'
    import subprocess
    # ... inline script
    EOF
```

**After:**

```yaml
- name: Validate commit
  run: |
    python3 .github/scripts/validate_commit.py \
      --pattern "^PROJ-\\d+:.*" \
      --max-length 300 \
      --verbose
```

### From local workflow to base workflow

**Before (in your repo):**

```yaml
# .github/workflows/validation.yml
jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      # ... many steps
```

**After (in your repo):**

```yaml
# .github/workflows/validation.yml
jobs:
  validate:
    uses: your-org/docs/.github/workflows/validation-base.yml@main
    with:
      commit_message_pattern: "^PROJ-\\d+:.*"
```

---

## Troubleshooting

### Script not found error

**Error:**

```
python3: can't open file '.github/scripts/validate_commit.py': No such file or directory
```

**Solution:**
Ensure you've checked out the code before running scripts:

```yaml
steps:
  - name: Checkout code
    uses: actions/checkout@v4

  - name: Validate commit
    run: python3 .github/scripts/validate_commit.py ...
```

### Pattern not matching

**Error:**

```
FAILED: Commit message is invalid.
Expected pattern: ...
```

**Solution:**

1. Check your commit message format
2. Test the regex pattern locally
3. Ensure special characters are properly escaped in YAML

**Test locally:**

```bash
python3 .github/scripts/validate_commit.py \
  --pattern "^PROJ-\\d+:.*" \
  --verbose
```

### GH_TOKEN error

**Error:**

```
ERROR: Failed to fetch PR title: gh: To use GitHub CLI in a GitHub Actions workflow, set the GH_TOKEN environment variable
```

**Solution:**
Add the token to the step:

```yaml
- name: Validate PR title
  env:
    GH_TOKEN: ${{ github.token }}
  run: python3 .github/scripts/validate_pr_title.py ...
```

---

## Contributing

When modifying validation logic:

1. Update the Python scripts in `.github/scripts/`
2. Test locally before committing
3. Update `validation-base.yml` if changing workflow logic
4. Update `validation.yml` if changing this repo's configuration
5. Update this README with any new parameters or behavior changes
