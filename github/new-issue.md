# Claude Command: New Issue (new-issue)

This command provides an intelligent GitHub issue creation workflow with **mandatory user approval for every action**. It analyzes your input, suggests appropriate issue structure, and creates well-formatted GitHub issues with proper labels and organization.

## Usage

Create a new issue with direct context:
```
/new-issue Create an issue for refactoring the login system
```

Or with complex requirements:
```
/new-issue We need a dashboard with user statistics, charts, and export functionality
```

## What This Command Does

**⚠️ IMPORTANT: Every step requires explicit user approval before execution!**

1. **Input Analysis**:
   - Analyzes your issue description for complexity
   - Identifies different concerns or components
   - Determines if this should be one issue or multiple issues
   - **→ Waits for user confirmation to proceed**

2. **Issue Structure Planning**:
   - Suggests issue organization (single, multiple, or main+sub issues)
   - Creates detailed issue titles and descriptions
   - Recommends appropriate labels and priority levels
   - Plans issue relationships and dependencies
   - **→ Waits for user approval of the structure**

3. **Milestone Planning**:
   - Analyzes available milestones in the repository
   - Suggests appropriate milestone assignment for issues
   - Offers to create new milestones if needed
   - **→ Waits for user approval of milestone strategy**

4. **Issue Content Creation**:
   - Generates comprehensive issue descriptions
   - Creates acceptance criteria and task lists
   - Suggests relevant labels (bug, feature, enhancement, etc.)
   - Plans milestone assignments if applicable
   - **→ Presents all content for review and approval**

5. **GitHub Issue Creation**:
   - **→ Asks permission to create each issue**
   - Creates issues in the specified order
   - Links related issues with proper references
   - Assigns appropriate labels and metadata
   - **→ Auto-creates missing labels if they don't exist in repository**
   - **→ Confirms each creation before proceeding**

## Multi-Issue Detection & Handling

The command intelligently analyzes your input for:

### Single Issue Indicators:
- Simple, focused requests
- Single component or feature
- Clear, atomic scope
- Example: "Fix login button not responding"

### Multiple Issue Indicators:
- Multiple distinct features mentioned
- Different technical areas involved
- Complex workflows with multiple steps
- Example: "Dashboard with statistics, charts, export, and user management"

### Main + Sub-Issue Structure:
- Large features with clear sub-components
- Epic-style requirements
- Multiple related but distinct tasks
- Example: "Complete authentication system overhaul"

## Issue Organization Patterns

### Pattern 1: Single Issue
```
Title: Fix login system authentication timeout
Labels: [bug, authentication, high-priority]
```

### Pattern 2: Multiple Independent Issues
```
Issue 1: Create user statistics dashboard
Issue 2: Implement data export functionality  
Issue 3: Add user management interface
```

### Pattern 3: Main Issue + Sub-Issues
```
Main Issue: Complete Dashboard Implementation
├── Sub-Issue 1: User statistics component
├── Sub-Issue 2: Chart visualization system
├── Sub-Issue 3: Data export functionality
└── Sub-Issue 4: Mobile responsive design
```

## User Approval Gates

**Every action requires explicit user approval:**

1. **Before Analysis**: "May I analyze your issue description?"
2. **After Analysis**: "I've identified X areas. Should I suggest a structure?"
3. **Structure Proposal**: "I suggest: [Structure]. Is this correct?"
4. **Milestone Planning**: "Should I check available milestones and make suggestions?"
5. **Milestone Decision**: "I suggest: [Milestone]. Should I create a new milestone?"
6. **Content Review**: "Here are the proposed issue contents. Approve?"
7. **Before Creation**: "May I create issue '{title}'?"
8. **Label Creation**: "Label '{label}' doesn't exist. Should I create it?"
9. **After Each Issue**: "Issue created. Should I continue with the next one?"

## GitHub Integration

### Issue Creation Features:
- **Comprehensive Descriptions**: Detailed problem descriptions and solutions
- **Acceptance Criteria**: Clear, testable requirements
- **Task Lists**: Broken-down implementation steps
- **Proper Labels**: Automatically suggested based on content analysis
- **Auto-Label Creation**: Creates missing labels automatically with appropriate colors
- **Linking**: Related issues are properly cross-referenced
- **Templates**: Follows repository issue templates if available
- **Milestone Assignment**: Assigns issues to appropriate milestones
- **No Co-Author**: **NEVER adds Claude as Co-Author in any GitHub content**

### Label Suggestions & Auto-Creation:
- **Type Labels**: `bug` (red), `feature` (green), `enhancement` (blue), `documentation` (yellow)
- **Priority Labels**: `low` (gray), `medium` (orange), `high` (red), `critical` (dark red)
- **Component Labels**: `frontend` (purple), `backend` (brown), `api` (teal), `database` (navy)
- **Status Labels**: `needs-investigation` (yellow), `ready-to-implement` (green)
- **Auto-Creation**: Missing labels are created automatically with appropriate colors and descriptions

## Command Arguments

- **Direct Context**: Everything after `/new-issue` is treated as the issue description
- **Examples**:
  - `/new-issue Login button doesn't work on mobile`
  - `/new-issue Need to implement user roles and permissions system`
  - `/new-issue Dashboard should show real-time analytics and export options`

## Advanced Features

### Intelligent Content Generation:
1. **Problem Analysis**: Identifies the core issue or requirement
2. **Solution Suggestions**: Proposes potential approaches
3. **Technical Considerations**: Highlights important technical aspects
4. **Testing Requirements**: Suggests testing strategies
5. **Documentation Needs**: Identifies documentation requirements

### Milestone Management:
1. **Milestone Discovery**: Automatically finds existing milestones
2. **Smart Assignment**: Matches issues to appropriate milestones based on content
3. **Milestone Creation**: Offers to create new milestones when needed
4. **Timeline Awareness**: Considers milestone due dates and priorities
5. **Milestone Suggestions**: Proposes milestone names and descriptions

### Relationship Management:
- **Dependencies**: Identifies which issues depend on others
- **Blocking**: Marks issues that block other development
- **Related**: Links conceptually related issues
- **Epic Tracking**: Creates proper epic/story relationships

## Workflow Examples

### Example 1: Simple Bug Report
```bash
/new-issue Login button not responsive on mobile
```

**Agent Analysis:**
- Single issue detected
- Bug type identified
- Mobile-specific problem

**Suggested Structure:**
- One issue: "Fix: Login button not responsive on mobile devices"
- Labels: [bug, mobile, frontend, medium-priority]
- Milestone: "Bug Fixes v1.2" (existing) or "Mobile Improvements" (new)

### Example 2: Complex Feature Request
```bash
/new-issue Need a complete user management system with roles, permissions, and admin dashboard
```

**Agent Analysis:**
- Multiple components detected
- Large feature scope
- Several distinct areas

**Suggested Structure:**
- Main Issue: "Epic: Complete User Management System"
- Sub-Issue 1: "Implement user roles system"
- Sub-Issue 2: "Create permissions framework"
- Sub-Issue 3: "Build admin dashboard interface"
- Sub-Issue 4: "Add role-based access control"
- Milestone: "User Management v2.0" (new milestone with 3-month timeline)

### Example 3: Multiple Independent Features
```bash
/new-issue We need dark mode, export feature, and push notifications
```

**Agent Analysis:**
- Three independent features
- Different technical areas
- Can be developed in parallel

**Suggested Structure:**
- Issue 1: "Feature: Implement dark mode theme"
- Issue 2: "Feature: Add data export functionality"  
- Issue 3: "Feature: Implement push notifications"
- Milestone Options: "UI Enhancements v1.5" (existing) or "New Features Q1" (new)

## Prerequisites

- Git repository with GitHub remote
- GitHub CLI (`gh`) configured with appropriate permissions
- Repository access for creating issues
- **GitHub Username**: [YOUR_USERNAME]

## Security & Permissions

- Uses existing GitHub CLI authentication for [YOUR_USERNAME]
- Respects repository settings and permissions
- Never creates issues without explicit approval
- All GitHub operations are performed under the [YOUR_USERNAME] account
- **⚠️ NEVER adds Claude as Co-Author in any GitHub content!**

## Quality Assurance Features

1. **Content Validation**: Ensures issues have clear, actionable descriptions
2. **Duplicate Detection**: Checks for similar existing issues
3. **Label Consistency**: Uses repository's established labeling conventions
4. **Label Auto-Creation**: Creates missing labels with appropriate colors and descriptions
5. **Template Compliance**: Follows repository issue templates
6. **Relationship Integrity**: Ensures proper issue linking and dependencies
7. **No Co-Author**: **NEVER adds Claude as Co-Author in any GitHub content**

## Error Handling

The command handles various scenarios:
- **Repository not found**: Provides clear error message
- **Insufficient permissions**: Guides through authentication
- **Duplicate issues**: Offers to update existing issues instead
- **Network issues**: Retries with exponential backoff
- **Invalid input**: Requests clarification from user

## Integration with Other Commands

- **Works with `/qfix`**: Creates issues that can be fixed with qfix command
- **Label Integration**: Uses consistent labeling with your workflow
- **GitHub Username**: All issues created under [YOUR_USERNAME] account

## Best Practices Enforced

1. **Clear Titles**: Descriptive, searchable issue titles
2. **Detailed Descriptions**: Comprehensive problem/requirement descriptions
3. **Actionable Content**: Issues contain clear next steps
4. **Proper Organization**: Logical grouping of related issues
5. **Consistent Labeling**: Uses repository's labeling conventions
6. **User Control**: Never creates issues without explicit approval
7. **No Co-Author**: **NEVER adds Claude as Co-Author in any GitHub content**

## Troubleshooting

Common issues and solutions:
- **"Repository not found"**: Verify you're in a GitHub repository
- **"Permission denied"**: Check GitHub CLI authentication with `gh auth status` (should show [YOUR_USERNAME])
- **"Issue creation failed"**: Verify repository write permissions
- **"Template errors"**: Check if repository has required issue templates

This command intelligently transforms your ideas into well-structured GitHub issues while maintaining complete user control over the creation process.