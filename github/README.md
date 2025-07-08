# Claude Commands - Setup Instructions

## Required Software

1. **GitHub CLI** (`gh`)
   ```bash
   # macOS
   brew install gh
   
   # Windows
   winget install --id GitHub.cli
   
   # Linux
   # See: https://github.com/cli/cli/blob/trunk/docs/install_linux.md
   ```

2. **Authenticate GitHub CLI**
   ```bash
   gh auth login
   ```

## Required Text Changes

### In both files (`new-issue.md` and `qfix.md`):

Replace `[YOUR_USERNAME]` with your GitHub username in these locations:

1. **Prerequisites** section:
   ```markdown
   - **GitHub Username**: [YOUR_USERNAME]
   ```

2. **Security & Permissions** section:
   ```markdown
   - Uses existing GitHub CLI authentication for [YOUR_USERNAME]
   - All GitHub operations are performed under the [YOUR_USERNAME] account
   ```

3. **Troubleshooting** section:
   ```markdown
   - **"Permission denied"**: Check GitHub CLI authentication with `gh auth status` (should show [YOUR_USERNAME])
   ```

## Verify Setup

```bash
gh auth status
```

This should show your GitHub username.

## Usage

- Create issues: `/new-issue Your issue description`
- Fix issues: `/qfix #123`