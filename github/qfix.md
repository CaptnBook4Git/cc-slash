# Claude Command: Quick Fix (qfix)

This command provides an intelligent GitHub issue-to-solution workflow with **mandatory user approval for every step**. No action is taken without explicit user confirmation.

## Usage

To fix an issue, use the issue number:
```
/qfix #5
```

Or with hash symbol:
```
/qfix 12
```

## What This Command Does

**⚠️ IMPORTANT: Every step requires explicit user approval before execution!**

1. **Issue Analysis**:
   - Fetches the complete issue details including title, description, and all comments
   - Analyzes the problem context and requirements
   - Identifies any referenced files, components, or dependencies
   - **→ Waits for user confirmation to proceed**

2. **Branch Creation** (MANDATORY - IMMEDIATE):
   - **→ Asks permission to create new branch**
   - **⚠️ CRITICAL: Creates a NEW branch IMMEDIATELY - NEVER works on main/master!**
   - Uses `gh issue develop {issue-number} --name fix/issue-{number}-{short-description} --checkout`
   - Automatically creates and links branch to the GitHub issue
   - Switches to the new branch for development
   - **→ Verifies we're on the new branch before proceeding**

3. **Solution Planning**:
   - Creates a detailed implementation plan based on the issue content
   - Considers existing codebase patterns and architecture
   - Provides step-by-step breakdown of required changes
   - Estimates complexity and potential risks
   - **→ Waits for user approval of the plan**

4. **Plan Review & GitHub Comment**:
   - Presents the final plan for review
   - Allows modifications and refinements
   - **→ Asks permission to post plan as comment on GitHub issue**
   - Posts the approved plan as a comment on the GitHub issue only after approval
   - Links the plan to the issue for future reference

5. **Implementation** (Step-by-step with approvals):
   - **→ Before each implementation step: Asks for permission**
   - **⚠️ CRITICAL: Verifies we're on the correct feature branch before ANY code changes**
   - Executes one plan step at a time
   - Shows proposed changes before making them
   - **⚠️ NEVER starts/stops/restarts servers - user handles server management**
   - **→ After implementation: Waits for user testing and feedback**
   - **→ Only proceeds to commit after user confirms implementation is working**
   - Makes incremental commits for each logical change
   - Follows existing code patterns and conventions
   - **→ After each step: Asks to continue or pause**

6. **Quality Assurance**:
   - **→ Asks permission to run linting and formatting checks**
   - Runs linting and formatting checks
   - **→ Asks permission to execute tests**
   - Executes relevant tests
   - Validates the fix addresses the original issue
   - Ensures no regressions are introduced

7. **Completion & Merge**:
   - **→ Asks permission to create pull request**
   - Creates a pull request with detailed description
   - References the original issue with closing keywords
   - **→ Explicitly waits for your testing confirmation**
   - **→ Asks permission to merge PR**
   - Merges the PR using appropriate merge strategy
   - **→ Asks permission to post solution summary to issue**
   - Posts a comprehensive solution summary comment on the original issue
   - **→ Asks permission to post feature update summary**
   - Posts a user-friendly feature update comment explaining new functionality and how it works
   - **→ Asks permission to clean up feature branch**
   - Cleans up the feature branch
   - **→ Asks permission to switch to main and pull latest changes**
   - Switches to main branch and pulls latest changes from remote

## Branch Naming Convention

**⚠️ CRITICAL: Always creates NEW branches - never works on main/master!**

Branches are automatically named following this pattern:
- `fix/issue-{number}-{short-description}`
- Example: `fix/issue-5-memory-leak-in-parser`
- Example: `fix/issue-12-authentication-timeout`

**Branch Creation is MANDATORY:**
- **NEVER work directly on main/master branches**
- **ALWAYS create a new feature branch for every issue**
- **MUST link the branch to the GitHub issue**
- **MUST switch to the new branch before any code changes**
- **NEVER starts/stops/restarts servers - user handles server management**

## Commit Message Format

All commits follow conventional commit format with issue reference:
- `fix: resolve memory leak in parser component (#5)`
- `feat: add authentication timeout handling (#12)`
- `test: add unit tests for issue #5 fix`
- `docs: update documentation for issue #12 changes`

**⚠️ NEVER adds Claude as Co-Author in commit messages!**

## Pull Request Integration

The command automatically:
- Creates descriptive PR titles: `Fix: Memory leak in parser component (#5)`
- Generates comprehensive PR descriptions including:
  - Link to the original issue
  - Summary of changes made
  - Testing instructions
  - Breaking changes (if any)
- Uses closing keywords: `Closes #5`, `Fixes #12`, `Resolves #15`
- **Feature Update Comments**: Posts user-friendly explanation of new functionality without code details

## Git Best Practices Applied

1. **Atomic Commits**: Each logical change is committed separately
2. **Descriptive Messages**: All commits reference the issue and describe the change
3. **No Co-Author**: **NEVER adds Claude as Co-Author in commit messages**
4. **Branch Protection**: Follows your repository's branch protection rules
5. **Merge Strategy**: Uses the appropriate merge strategy (merge, squash, or rebase)
6. **Clean History**: Maintains a clean, readable git history
7. **Issue Linking**: Proper GitHub issue linking for traceability
8. **🚨 MANDATORY BRANCH CREATION**: **NEVER works on main/master - ALWAYS creates new branches**
9. **Server Management**: **NEVER starts/stops/restarts servers - user handles server management**
10. **Solution Documentation**: Posts comprehensive solution summary to original issue after merge
11. **Feature Communication**: Posts user-friendly feature update explaining new functionality without code details

## Workflow Steps

### Phase 1: Analysis
1. Fetch issue details using GitHub API
2. Parse issue content and comments
3. Identify problem scope and requirements
4. Check for duplicate or related issues

### Phase 2: Planning
1. Analyze codebase for affected areas
2. Create implementation strategy
3. Identify required changes and files
4. Estimate complexity and risks
5. Plan testing approach

### Phase 3: Branch Creation (IMMEDIATE)
1. **🚨 CRITICAL: Create NEW linked branch IMMEDIATELY after issue analysis**
2. **→ Ask permission to create linked branch**
3. Use `gh issue develop {issue-number} --name fix/issue-{number}-{description} --checkout`
4. **NEVER work on main/master!**
5. Verify we're on the new branch before proceeding

### Phase 4: Planning & Approval
1. Present plan for review
2. Allow plan modifications
3. **→ Ask permission to post plan as issue comment**
4. Post approved plan as issue comment

### Phase 5: Implementation
1. **🚨 CRITICAL: Verify we're on the correct feature branch before ANY code changes**
2. **→ Ask permission for each implementation step**
3. Execute plan step by step with approval gates
4. **⚠️ NEVER starts/stops/restarts servers - user handles server management**
5. **→ Wait for user testing and feedback after implementation**
6. **→ Ask permission for each commit (only after user confirms implementation works)**
7. Make incremental commits
8. **→ Ask permission to run tests**
9. Run tests continuously
10. Handle any unexpected issues with user input

### Phase 6: Review & Merge
1. **→ Ask permission to create pull request**
2. Create pull request
3. **→ Ask permission to run final quality checks**
4. Run final quality checks
5. **→ Explicitly wait for user testing confirmation**
6. Wait for user testing confirmation
7. **→ Ask permission to merge**
8. Merge and clean up only after approval
9. **→ Ask permission to post solution summary to original issue**
10. Post comprehensive solution summary comment on the original issue
11. Summary includes: solution approach, changes made, testing performed, and resolution confirmation
12. **→ Ask permission to post feature update summary**
13. Post user-friendly feature update comment explaining new functionality and how it works
14. **→ Ask permission to switch to main and pull latest changes**
15. Switch to main branch and pull latest changes from remote

## Command Arguments

- `#{number}`: Issue number (required)
  - Examples: `#5`, `12`, `#147`
  - Automatically detects and parses issue numbers

## Error Handling

The command handles various scenarios:
- **Issue not found**: Provides clear error message
- **Insufficient permissions**: Guides through authentication
- **Merge conflicts**: Offers resolution strategies
- **Test failures**: Pauses for manual intervention
- **Network issues**: Retries with exponential backoff

## Prerequisites

- Git repository with GitHub remote
- GitHub CLI (`gh`) configured with appropriate permissions
- Repository access for creating branches and PRs
- Write access to the repository
- **GitHub Username**: [YOUR_USERNAME]

## Security & Permissions

- Uses existing GitHub CLI authentication for [YOUR_USERNAME]
- Respects repository branch protection rules
- Follows your organization's security policies
- Never commits sensitive information
- All GitHub operations are performed under the [YOUR_USERNAME] account

## Examples

### Example 1: Simple Bug Fix
```bash
/qfix #23
```
Result: Analyzes issue #23 about a button not working, creates a plan to fix the click handler, implements the fix, and creates a PR titled "Fix: Button click handler not responding (#23)"

### Example 2: Feature Request
```bash
/qfix 45
```
Result: Analyzes issue #45 requesting a new search feature, creates an implementation plan, builds the feature across multiple commits, and creates a PR titled "Feat: Add advanced search functionality (#45)"

### Example 3: Performance Issue
```bash
/qfix #8
```
Result: Analyzes issue #8 about slow page loading, creates optimization plan, implements performance improvements, adds benchmarks, and creates a PR titled "Perf: Optimize page loading performance (#8)"

## Integration with Other Commands

- Uses `/commit` patterns for commit message formatting
- Integrates with existing linting and testing workflows
- Follows project-specific conventions from `CLAUDE.md`

## Quality Assurance Features

1. **Code Analysis**: Reviews existing code patterns before implementing
2. **Test Coverage**: Ensures new code has appropriate test coverage
3. **Documentation**: Updates relevant documentation automatically
4. **Linting**: Runs project linters and fixes issues
5. **Type Checking**: Validates TypeScript/type annotations if applicable

## User Control & Approval Gates

**Every action requires explicit user approval:**

1. **Before Issue Analysis**: "May I fetch and analyze issue #{number}?"
2. **Before Branch Creation**: "May I create branch using `gh issue develop {issue-number} --name fix/issue-{number}-{description} --checkout`?"
3. **Before Planning**: "May I create an implementation plan?"
4. **Before Plan Posting**: "May I post this plan as a comment on the GitHub issue?"
5. **Before Each Implementation Step**: "May I proceed with step X: {description}?"
6. **After Implementation**: "Please test the implementation and provide feedback before I commit."
7. **Before Each Commit**: "May I commit these changes: {commit_message}? (only after user confirms implementation works)"
8. **Before Testing**: "May I run the test suite?"
9. **Before PR Creation**: "May I create a pull request?"
10. **Before Merge**: "May I merge the pull request?"
11. **Before Solution Summary**: "May I post a solution summary comment to the original issue?"
12. **Before Feature Update Summary**: "May I post a user-friendly feature update comment explaining the new functionality?"
13. **Before Cleanup**: "May I delete the feature branch?"
14. **Before Main Update**: "May I switch to main branch and pull the latest changes?"

## Monitoring & Feedback

- Provides progress updates throughout the process
- Offers clear next steps at each phase
- **Pauses at every major action for user approval**
- Allows intervention at any point
- Maintains detailed logs for debugging
- **Never proceeds without explicit "yes" confirmation**
- **Always waits for user testing and feedback before committing changes**

## Best Practices Enforced

1. **Single Responsibility**: Each commit addresses one concern
2. **Clear Communication**: Detailed PR descriptions and commit messages
3. **No Co-Author**: **NEVER adds Claude as Co-Author in commit messages**
4. **User Testing First**: Waits for user testing and feedback before any commits
5. **Server Management**: **NEVER starts/stops/restarts servers - user handles server management**
6. **Proper Testing**: Validates changes before merging
7. **Documentation**: Updates docs when necessary
8. **Feature Communication**: Posts user-friendly feature update explaining new functionality without code details
9. **Clean History**: Maintains readable git history
10. **Issue Tracking**: Proper linking and closure of issues

## Troubleshooting

Common issues and solutions:
- **"Issue not found"**: Verify issue number and repository access
- **"No GitHub remote"**: Ensure repository has GitHub remote configured
- **"Permission denied"**: Check GitHub CLI authentication with `gh auth status` (should show [YOUR_USERNAME])
- **"Merge conflicts"**: Command will pause and guide through resolution
- **"Tests failing"**: Review test output and fix issues before continuing

This command streamlines the entire issue-to-solution workflow while maintaining high code quality and following Git best practices.