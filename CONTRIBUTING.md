# 🤝 Contributing to Developer Roadmap Plugin

Thank you for considering contributing! This guide explains how to participate and help improve this plugin.

## Table of Contents

- [Ways to Contribute](#ways-to-contribute)
- [Development Setup](#development-setup)
- [Code Standards](#code-standards)
- [Contribution Process](#contribution-process)
- [Agent Development](#agent-development)
- [Skill Development](#skill-development)
- [Command Development](#command-development)
- [Testing & Quality](#testing--quality)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)

---

## Ways to Contribute

### 📝 Documentation

- Improve existing guides in `/docs`
- Fix typos and clarify explanations
- Add examples and tutorials
- Update CHANGELOG.md
- Improve README.md

### 🤖 Agent Enhancements

- Expand learning paths in existing agents
- Add new role profiles
- Improve content quality
- Add code examples
- Link related technologies

### 💡 Skill Improvements

- Add advanced tutorials
- Create code examples
- Add project ideas
- Improve quick starts
- Add resources and references

### 🛠️ Command Enhancements

- Improve interactivity
- Add new command variations
- Better user feedback
- Enhanced navigation

### 🐛 Bug Fixes

- Report and fix bugs
- Improve error messages
- Enhance error handling
- Optimize performance

### 🎨 UI/UX Improvements

- Better formatting
- Enhanced readability
- Improved navigation
- Better organization

### 🧪 Testing

- Test agents and skills
- Verify command behavior
- Check hook functionality
- Report issues

---

## Development Setup

### Prerequisites

```bash
# Node.js (for development tools)
node --version  # 18+

# Git
git --version

# Claude Code
claude-code --version
```

### Local Development Environment

```bash
# 1. Clone repository
git clone https://github.com/pluginagentmarketplace/custom-plugin-software-architect.git
cd custom-plugin-software-architect

# 2. Create feature branch
git checkout -b feature/your-feature-name

# 3. Link for local testing
ln -s $(pwd) ~/.claude-code/plugins/custom-plugin-software-architect-dev

# 4. Restart Claude Code
# Close and reopen Claude Code

# 5. Test with commands
# In Claude Code:
/learn
/assess
/projects
```

### File Organization

```
custom-plugin-software-architect/
├── agents/              ← Agent markdown files
├── skills/             ← SKILL.md files
├── commands/           ← Command markdown files
├── hooks/              ← Hook configuration
├── docs/               ← Documentation
├── .claude-plugin/     ← Plugin manifest
└── [root files]        ← README, LICENSE, etc.
```

---

## Code Standards

### Markdown Standards

```markdown
# Heading 1 (Plugin/document title)
## Heading 2 (Major sections)
### Heading 3 (Subsections)

- Bullet points for lists
  - Nested items with two spaces

1. Numbered lists
2. For ordered content
3. Use numbers sequentially

**Bold** for emphasis
*Italic* for technical terms
`Code` for inline code
```code
  Block code with triple backticks
  Specify language: ```python, ```javascript, etc.
```

### YAML Frontmatter

**Agents:**
```yaml
---
description: Agent description (max 255 chars)
capabilities:
  - Capability 1
  - Capability 2
---
```

**Skills:**
```yaml
---
name: skill-id (lowercase, hyphens, max 64 chars)
description: What skill teaches (max 1024 chars)
---
```

### Content Quality Checklist

- [ ] No typos or grammar errors
- [ ] Clear and concise language
- [ ] Proper headings and organization
- [ ] Code examples where relevant
- [ ] Links to external resources
- [ ] References to related agents/skills
- [ ] Time estimates provided
- [ ] Learning outcomes listed

---

## Contribution Process

### Step 1: Choose What to Work On

**Good first contributions:**
- Fix typos in documentation
- Add examples to existing skills
- Improve README formatting
- Update outdated information

**Medium complexity:**
- Expand agent content
- Add new learning paths
- Create new skill sections
- Enhance commands

**Advanced contributions:**
- Create new agents
- Develop new skills
- Implement new hooks
- Build new commands

### Step 2: Fork & Branch

```bash
# Fork on GitHub
# Go to github.com/pluginagentmarketplace/custom-plugin-software-architect
# Click: Fork

# Clone your fork
git clone https://github.com/YOUR-USERNAME/custom-plugin-software-architect.git

# Create feature branch
git checkout -b feature/descriptive-name
```

### Step 3: Make Changes

**For agent changes:**
```bash
# Edit agent file
vim agents/01-frontend-development.md

# Follow agent content standards
# Include: description, capabilities, technologies, learning outcomes
```

**For skill changes:**
```bash
# Edit SKILL.md
vim skills/frontend-development/SKILL.md

# Sections: YAML frontmatter, quick start, learning outcomes, projects
```

**For command changes:**
```bash
# Edit command file
vim commands/learn.md

# Include: clear instructions, examples, user interactions
```

### Step 4: Test Your Changes

```bash
# 1. Verify markdown syntax
cat agents/01-frontend-development.md | head -20

# 2. Check YAML frontmatter is valid
grep -A5 "^---$" agents/01-frontend-development.md

# 3. Test in Claude Code
#    Copy to .claude-code/plugins/
#    Restart Claude Code
#    Run relevant commands

# 4. Verify all links work
# Check external links are valid

# 5. Proofread content
# Check spelling, grammar, clarity
```

### Step 5: Commit Changes

```bash
# Add files
git add agents/01-frontend-development.md

# Commit with clear message (see Commit Guidelines below)
git commit -m "feat(agent/frontend): Add Next.js and performance sections"

# View commit
git log -1
```

### Step 6: Push & Create Pull Request

```bash
# Push to your fork
git push origin feature/descriptive-name

# Create Pull Request on GitHub
# Go to: github.com/YOUR-USERNAME/custom-plugin-software-architect
# Click: New Pull Request
```

---

## Agent Development

### Agent File Structure

```markdown
---
description: [Max 255 characters describing agent expertise]
capabilities:
  - Capability 1
  - Capability 2
  - [At least 5 capabilities]
---

# Agent Name

## Overview
[2-3 paragraph overview of agent's domain]

## Covered Roles
[Table or list of all roles covered]

## Key Technologies
[Organized by category, technologies covered]

## Learning Path Structure
[How users progress through learning]

## Skills Included
[What skills will be covered]

## When to Use This Agent
[Bullet points of use cases]

## Quick Navigation
[How to navigate this agent's content]

## Integration with Other Agents
[References to related agents]
```

### Agent Content Guidelines

1. **Roles Coverage**
   - Include 5+ roles in each agent
   - Time estimates for each role
   - Difficulty levels

2. **Technologies**
   - 20+ technologies per agent
   - Organized by category
   - Version information (2025 current)

3. **Learning Paths**
   - Progressive difficulty
   - Estimated time (weeks/months)
   - Prerequisites
   - Learning outcomes

4. **Code Examples**
   - Minimum 3-5 code examples
   - Production-ready quality
   - Multiple languages where relevant
   - Comments explaining logic

5. **Resources**
   - Official documentation links
   - Recommended books
   - Courses and tutorials
   - Community resources

### Agent Expansion Checklist

- [ ] Add 2-3 new roles (with time estimates)
- [ ] Expand technology coverage (add 10+ new tech)
- [ ] Add 3-5 new code examples
- [ ] Improve learning path documentation
- [ ] Add project ideas (5+)
- [ ] Add resource references (10+)
- [ ] Update integration links to other agents
- [ ] Proofread and check grammar
- [ ] Verify all links are valid
- [ ] Test in Claude Code

---

## Skill Development

### Skill File Structure

```markdown
---
name: skill-identifier
description: What users learn in this skill (max 1024 chars)
---

# Skill Name

## Quick Start

[10-minute introduction with code example]

## What You'll Learn

### Foundation Level
[Weeks 1-X: Topics and concepts]

### Intermediate Level
[Weeks X-Y: Practical applications]

### Advanced Level
[Weeks Y-Z: Complex scenarios]

## Technologies Covered

[Organized list with versions]

## Learning Outcomes

[Checklist of achievements: ✅ Item]

## Project Examples

[5-10 project ideas with descriptions]

## When to Use This Skill

[Bullet points of when to learn]

## Related Agents

[Links to related agents]

## Resources

[Books, courses, documentation, tutorials]
```

### Skill Content Quality

1. **Quick Start**
   - Runnable code within 5 minutes
   - Clear output or result
   - Good for immediate value

2. **Code Examples**
   - Production-quality code
   - Proper error handling
   - Comments explaining logic
   - Multiple examples (3+)

3. **Learning Outcomes**
   - Specific and measurable
   - Clear checkboxes
   - Realistic achievements

4. **Projects**
   - Beginner, intermediate, advanced mix
   - Clear descriptions
   - Technology requirements
   - Estimated timelines

5. **Resources**
   - Verified working links
   - Mix of free and paid
   - Recent publications
   - Community recommendations

### Skill Expansion Checklist

- [ ] Add advanced tutorial section
- [ ] Include 5+ code examples
- [ ] Add 5+ project ideas
- [ ] Link related agents
- [ ] Update technology versions
- [ ] Add 10+ external resources
- [ ] Include certification paths
- [ ] Add troubleshooting tips
- [ ] Verify all code is executable
- [ ] Test examples work

---

## Command Development

### Command File Structure

```markdown
# Command Title

## Purpose

[Clear explanation of what command does]

## Features

[Bullet list of features with emojis]

## Usage

[How to use the command]

## Example

[Real example with interaction]

## Options

[Available options/variations]

## Tips & Tricks

[Pro tips for using command]

## Related Commands

[Links to other commands]
```

### Command Enhancement Guidelines

1. **User Experience**
   - Clear instructions
   - Visual feedback
   - Helpful examples
   - Error messages

2. **Navigation**
   - Links to other commands
   - Cross-references
   - Suggested next steps

3. **Examples**
   - Real user interactions
   - Expected outputs
   - Edge cases

4. **Documentation**
   - Clear purpose
   - All features explained
   - Pro tips included

### Command Improvement Checklist

- [ ] Add new example scenario
- [ ] Improve instructions
- [ ] Add helpful tips
- [ ] Link related commands
- [ ] Test all examples
- [ ] Verify clarity
- [ ] Check navigation
- [ ] Proofread

---

## Testing & Quality

### Testing Checklist

- [ ] **Markdown Syntax**: Files parse correctly
- [ ] **YAML Frontmatter**: Valid YAML structure
- [ ] **Links**: All links work (internal and external)
- [ ] **Code Examples**: Execute without errors
- [ ] **Content**: No typos, clear language
- [ ] **Structure**: Proper headings and organization
- [ ] **Completeness**: All sections filled out
- [ ] **Consistency**: Matches style guide

### Manual Testing

```bash
# 1. Markdown validation
# Check files parse correctly in Claude Code

# 2. Link checking
# Test all external links work

# 3. Code execution
# Run all code examples

# 4. Navigation
# Test all command flows

# 5. Agent routing
# Verify agents auto-select correctly

# 6. Skill loading
# Confirm skills invoke properly
```

### Automated Testing (Future)

```bash
# Once CI/CD is set up:
npm test

# Or:
make test

# Checks:
# - Markdown syntax
# - YAML structure
# - Link validity
# - Code formatting
# - Required sections
```

---

## Commit Guidelines

### Commit Message Format

```
type(scope): subject

body

footer
```

### Types

- **feat** - New feature
- **fix** - Bug fix
- **docs** - Documentation
- **style** - Formatting
- **refactor** - Code restructuring
- **test** - Tests
- **chore** - Build, deps, etc.

### Scopes

- **agent/frontend** - Frontend agent
- **agent/backend** - Backend agent
- **agent/mobile** - Mobile agent
- **agent/data-science** - AI/ML agent
- **agent/devops** - DevOps agent
- **agent/database** - Database agent
- **agent/fundamentals** - Fundamentals agent
- **skill/frontend** - Frontend skill
- **command/learn** - Learn command
- **docs** - Documentation
- **hooks** - Hook files

### Examples

```
feat(agent/frontend): Add Next.js advanced patterns section

- Add SSR best practices
- Include performance optimization tips
- Add 3 new code examples

Closes #42

---

fix(skill/backend): Update deprecated Mongoose syntax

Updated to latest Mongoose API

---

docs: Improve README installation instructions

Clarified steps for macOS and Linux users

---

feat(command/learn): Add interactive learning path selection

- Better UX with numbered options
- Smart agent routing based on selection
- Link to related /projects command
```

---

## Pull Request Process

### Before Submitting

1. **Self-Review**
   - Does code follow standards?
   - Are examples working?
   - Is documentation complete?

2. **Test**
   - Works in Claude Code?
   - Links functional?
   - No typos?

3. **Update Changelog**
   - Add entry to CHANGELOG.md
   - Version information
   - Clear description

### Pull Request Template

```markdown
## Description
[What changes does this PR make?]

## Type of Change
- [ ] Documentation update
- [ ] Agent enhancement
- [ ] Skill improvement
- [ ] Command enhancement
- [ ] Bug fix
- [ ] Other

## Changes
- [ ] Updated [file]
- [ ] Added [feature]
- [ ] Fixed [bug]

## Testing Done
- [ ] Tested in Claude Code
- [ ] Verified markdown
- [ ] Checked links
- [ ] Ran code examples

## Checklist
- [ ] Follows code standards
- [ ] Documentation updated
- [ ] No breaking changes
- [ ] Tests pass

## Related Issues
Closes #[issue number]
```

### Review Process

1. **Automated Checks**
   - Markdown syntax validation
   - Link checking
   - File structure verification

2. **Human Review**
   - Content quality check
   - Accuracy verification
   - Style consistency

3. **Feedback & Iteration**
   - Respond to comments
   - Make requested changes
   - Re-request review

4. **Merge**
   - Squash commits if requested
   - Merge to main branch
   - Close related issues

---

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inclusive environment.

### Expected Behavior

- Use inclusive language
- Be respectful of differing opinions
- Provide constructive feedback
- Be patient and helpful

### Unacceptable Behavior

- Harassment or discrimination
- Offensive comments
- Personal attacks
- Trolling

### Reporting Issues

Email: conduct@example.com

---

## Recognition

Contributors will be recognized in:
- CHANGELOG.md (Per release)
- Contributors file (When created)
- GitHub contributors graph
- Project documentation

---

## Questions?

- 💬 Start a GitHub discussion
- 📧 Email: contribute@example.com
- 📚 Check docs/

---

<div align="center">

### Thank you for contributing! 🎉

Your improvements make this plugin better for everyone.

</div>
