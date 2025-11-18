# 🔧 Setup & Installation Guide

Complete guide to installing and configuring the Developer Roadmap plugin.

## Table of Contents

- [System Requirements](#system-requirements)
- [Installation Methods](#installation-methods)
- [Verification](#verification)
- [Configuration](#configuration)
- [Troubleshooting](#troubleshooting)
- [First Run](#first-run)

---

## System Requirements

### Minimum Requirements

- **Claude Code**: Latest version
- **Operating System**: macOS, Linux, Windows (WSL2)
- **Disk Space**: 50MB+ for plugin files
- **Internet**: Required for external resources and documentation links
- **RAM**: 512MB+ for plugin operation

### Recommended Setup

- **Claude Code**: Latest stable version
- **Node.js**: 18+ (optional, for advanced hook development)
- **Git**: For cloning and updates
- **Disk Space**: 100MB+ for plugin + learning materials
- **Internet Speed**: Broadband for smooth experience

### Supported Platforms

✅ macOS (Intel & Apple Silicon)
✅ Linux (Ubuntu, Debian, CentOS, etc.)
✅ Windows (WSL2 recommended)
✅ Docker (for containerized setup)

---

## Installation Methods

### Method 1: Direct Copy (Recommended)

**Easiest for local development and testing**

```bash
# Step 1: Navigate to Claude Code plugins directory
cd ~/.claude-code/plugins

# Step 2: Clone or download plugin
git clone https://github.com/pluginagentmarketplace/custom-plugin-software-architect.git
# OR
cp -r /path/to/custom-plugin-software-architect .

# Step 3: Verify plugin.json exists
ls -la custom-plugin-software-architect/.claude-plugin/plugin.json

# Step 4: Restart Claude Code
# (Close and reopen Claude Code application)
```

### Method 2: Using Claude Code CLI

**For users with Claude Code CLI installed**

```bash
# Check Claude Code version
claude-code --version

# Add plugin
claude-code add-plugin ./custom-plugin-software-architect

# List installed plugins
claude-code list-plugins

# Verify installation
claude-code plugin-info custom-plugin-software-architect
```

### Method 3: Marketplace Installation (Future)

**Once published to Claude Marketplace**

```
1. Open Claude Code
2. Go to: Extensions → Marketplace
3. Search: "Developer Roadmap" or "Software Architect"
4. Click: Install
5. Confirm: Accept permissions
```

### Method 4: Manual Download

**For users without Git**

```bash
# 1. Download ZIP from GitHub
#    https://github.com/pluginagentmarketplace/custom-plugin-software-architect

# 2. Extract to plugins directory
unzip custom-plugin-software-architect-main.zip
cp -r custom-plugin-software-architect ~/.claude-code/plugins/

# 3. Restart Claude Code
```

### Method 5: Docker Setup

**For containerized environments**

```dockerfile
FROM claude-code:latest

# Copy plugin
COPY custom-plugin-software-architect /opt/claude-code/plugins/

# Set permissions
RUN chmod -R 755 /opt/claude-code/plugins/custom-plugin-software-architect

# Entry point
CMD ["claude-code"]
```

```bash
# Build and run
docker build -t claude-code-with-plugin .
docker run -it claude-code-with-plugin
```

---

## Verification

### Check Installation

```bash
# 1. List plugins
claude-code list-plugins | grep custom-plugin

# Expected output:
# custom-plugin-software-architect (v1.0.0) ✓

# 2. Verify directory structure
ls -la ~/.claude-code/plugins/custom-plugin-software-architect/

# Expected directories:
# .claude-plugin/
# agents/
# skills/
# commands/
# hooks/
# docs/

# 3. Check plugin.json validity
cat ~/.claude-code/plugins/custom-plugin-software-architect/.claude-plugin/plugin.json | jq '.'

# 4. Verify agents exist
ls agents/ | wc -l
# Expected: 7 files

# 5. Verify skills exist
find skills -name "SKILL.md" | wc -l
# Expected: 7 files

# 6. Verify commands exist
ls commands/ | wc -l
# Expected: 4 files
```

### Test Installation

**In Claude Code, type:**

```
/learn
```

Expected response:
- ✅ Plugin loads successfully
- ✅ Learning path selector appears
- ✅ Menu options display

If plugin doesn't load, see [Troubleshooting](#troubleshooting)

---

## Configuration

### plugin.json Configuration

The plugin.json file controls how the plugin behaves. Default configuration includes:

```json
{
  "name": "Developer Roadmap Software Architect",
  "description": "Comprehensive developer learning platform...",
  "version": "1.0.0",
  "agents": ["01-frontend-development", "02-backend-api-development", ...],
  "commands": ["learn", "roadmap", "assess", "projects"],
  "skills": ["frontend-development/SKILL", ...]
}
```

**To customize:**

1. Edit `.claude-plugin/plugin.json`
2. Modify name, description, or agent list
3. Restart Claude Code

### hooks.json Configuration

Configure automation and tracking behaviors:

```json
{
  "hooks": [
    {
      "name": "learning-progress-tracker",
      "triggers": ["after-agent-invoked"],
      "enabled": true
    }
  ],
  "configuration": {
    "tracking_enabled": true,
    "learning_progress_enabled": true,
    "notifications": {
      "milestone_celebrations": true,
      "skill_recommendations": true
    }
  }
}
```

**To disable specific hooks:**

```bash
# Edit hooks/hooks.json
# Set "enabled": false for unwanted hooks

# Example: disable celebrations
"milestone_celebrations": false
```

### Environment Variables (Optional)

Create `.env` file in plugin root:

```bash
# Learning preferences
LEARNING_LANGUAGE=en
SKILL_DIFFICULTY_DEFAULT=intermediate

# Tracking (if server-side hooks enabled)
TRACKING_ENABLED=true
ANALYTICS_ENDPOINT=https://your-endpoint.com

# Resources
EXTERNAL_RESOURCES_ENABLED=true
DOCUMENTATION_LANGUAGE=en
```

### Custom Agent Selection

Edit `hooks/hooks.json` to customize agent routing:

```json
{
  "agent-context-loader": {
    "match_keywords": {
      "frontend|react|vue": "01-frontend-development",
      "backend|api|rest": "02-backend-api-development",
      "mobile|ios|android": "03-mobile-game-development",
      "ai|ml|data": "04-data-science-ai",
      "devops|docker|kubernetes": "05-infrastructure-devops",
      "database|sql": "06-database-management",
      "algorithm|cs|git": "07-fundamentals-career"
    }
  }
}
```

---

## File Structure After Installation

```
~/.claude-code/plugins/
└── custom-plugin-software-architect/
    ├── .claude-plugin/
    │   └── plugin.json
    ├── agents/
    │   ├── 01-frontend-development.md
    │   ├── 02-backend-api-development.md
    │   ├── 03-mobile-game-development.md
    │   ├── 04-data-science-ai.md
    │   ├── 05-infrastructure-devops.md
    │   ├── 06-database-management.md
    │   └── 07-fundamentals-career.md
    ├── skills/
    │   ├── frontend-development/SKILL.md
    │   ├── backend-development/SKILL.md
    │   ├── mobile-development/SKILL.md
    │   ├── data-science/SKILL.md
    │   ├── infrastructure/SKILL.md
    │   ├── database/SKILL.md
    │   └── fundamentals/SKILL.md
    ├── commands/
    │   ├── learn.md
    │   ├── roadmap.md
    │   ├── assess.md
    │   └── projects.md
    ├── hooks/
    │   └── hooks.json
    ├── docs/
    │   ├── SETUP.md (this file)
    │   ├── ARCHITECTURE.md
    │   ├── INTEGRATION-GUIDE.md
    │   ├── AGENT-REFERENCE.md
    │   ├── SKILL-REFERENCE.md
    │   ├── LEARNING-PATHS.md
    │   └── TROUBLESHOOTING.md
    ├── README.md
    ├── CONTRIBUTING.md
    ├── LICENSE
    └── CHANGELOG.md
```

---

## Troubleshooting

### Plugin Not Loading

**Symptom:** `/learn` command not recognized

**Solutions:**

```bash
# 1. Verify installation path
ls ~/.claude-code/plugins/custom-plugin-software-architect/.claude-plugin/plugin.json

# 2. Check plugin.json syntax
cat ~/.claude-code/plugins/custom-plugin-software-architect/.claude-plugin/plugin.json | jq '.'

# 3. Restart Claude Code completely
# Close all windows and reopen

# 4. Check file permissions
chmod -R 755 ~/.claude-code/plugins/custom-plugin-software-architect/

# 5. Clear cache (if applicable)
rm -rf ~/.claude-code/cache/*

# 6. Reinstall plugin
rm -rf ~/.claude-code/plugins/custom-plugin-software-architect/
cp -r ./custom-plugin-software-architect ~/.claude-code/plugins/
```

### Commands Not Appearing

**Symptom:** /learn, /roadmap, /assess, /projects not recognized

**Solutions:**

```bash
# 1. Verify commands directory exists
ls -la ~/.claude-code/plugins/custom-plugin-software-architect/commands/

# 2. Check command files
ls -la *.md | grep -E "(learn|roadmap|assess|projects)"

# 3. Verify plugin.json references commands
grep -A5 '"commands"' .claude-plugin/plugin.json

# 4. Restart Claude Code and try commands again
```

### Agents Not Responding

**Symptom:** Agent invoked but no response

**Solutions:**

```bash
# 1. Verify agent files exist
ls ~/.claude-code/plugins/custom-plugin-software-architect/agents/ | wc -l
# Expected: 7

# 2. Check agent file syntax
grep "^---$" agents/01-frontend-development.md
# Should see YAML frontmatter

# 3. Verify skills exist for agents
find ~/.claude-code/plugins/custom-plugin-software-architect/skills -name "SKILL.md"

# 4. Check hooks.json for agent routing
cat hooks/hooks.json | jq '.hooks[] | select(.name == "agent-context-loader")'
```

### Slow Performance

**Symptom:** Plugin responds slowly or lags

**Solutions:**

```bash
# 1. Disable unnecessary hooks
# Edit hooks/hooks.json, set "enabled": false for non-essential hooks

# 2. Clear cache
rm -rf ~/.claude-code/cache/*

# 3. Restart Claude Code
# Completely close and reopen

# 4. Check system resources
ps aux | grep "claude-code"
# Look for high CPU/memory usage

# 5. Update to latest version
cd ~/.claude-code/plugins/custom-plugin-software-architect
git pull origin main
```

### Hooks Not Triggering

**Symptom:** Progress not being tracked

**Solutions:**

```bash
# 1. Verify hooks.json is valid
cat hooks/hooks.json | jq '.'

# 2. Check hooks are enabled
grep -A3 '"configuration"' hooks/hooks.json | grep '"enabled"'

# 3. Verify hook triggers
grep '"triggers"' hooks/hooks.json

# 4. Look for error messages
# Check Claude Code logs (if available)

# 5. Temporarily disable all hooks and re-enable one by one
```

---

## First Run

### Initial Setup (5 minutes)

1. **Install Plugin** (choose one method above)

2. **Verify Installation**
   ```
   /learn
   ```

3. **Choose Learning Path**
   - Select from displayed options
   - Or ask: "I want to learn full-stack development"

4. **Agent Auto-Routes**
   - Plugin selects appropriate agent
   - Displays relevant learning content

5. **Explore Further**
   - Try `/roadmap` to see all technologies
   - Try `/assess` to evaluate current skills
   - Try `/projects` for project ideas

### Recommended First Commands

```
# Command 1: Get learning recommendations
/learn

# Command 2: Self-assess your skills
/assess

# Command 3: Discover projects aligned with your level
/projects

# Command 4: Explore complete technology roadmap
/roadmap
```

### Pro Tips for First Use

1. **Start with /assess** before /learn
   - Understand your current level
   - Get accurate recommendations

2. **Use /roadmap to explore**
   - See all 65+ roles
   - Understand salary ranges and timelines

3. **Browse /projects** for motivation
   - See real projects you can build
   - Choose beginner projects first

4. **Follow agent guidance**
   - Agents automatically route based on context
   - Trust the smart routing system

5. **Refer to documentation**
   - docs/ folder has detailed guides
   - AGENT-REFERENCE.md explains each agent
   - LEARNING-PATHS.md shows sample paths

---

## Updating the Plugin

### Check Current Version

```bash
cat ~/.claude-code/plugins/custom-plugin-software-architect/.claude-plugin/plugin.json | jq '.version'
```

### Update from GitHub

```bash
cd ~/.claude-code/plugins/custom-plugin-software-architect
git pull origin main
```

### Manual Update

```bash
# 1. Download latest version
wget https://github.com/pluginagentmarketplace/custom-plugin-software-architect/archive/refs/heads/main.zip

# 2. Extract
unzip main.zip

# 3. Backup current version
mv ~/.claude-code/plugins/custom-plugin-software-architect ~/.claude-code/plugins/custom-plugin-software-architect.backup

# 4. Copy new version
cp -r custom-plugin-software-architect-main ~/.claude-code/plugins/custom-plugin-software-architect

# 5. Restart Claude Code
```

### Rollback

```bash
rm -rf ~/.claude-code/plugins/custom-plugin-software-architect
mv ~/.claude-code/plugins/custom-plugin-software-architect.backup ~/.claude-code/plugins/custom-plugin-software-architect
```

---

## Uninstallation

### Remove Plugin

```bash
# Option 1: Complete removal
rm -rf ~/.claude-code/plugins/custom-plugin-software-architect

# Option 2: Using CLI
claude-code remove-plugin custom-plugin-software-architect
```

### Verify Removal

```bash
# Check plugin is gone
claude-code list-plugins | grep custom-plugin
# Should show nothing

# Double-check directory
ls ~/.claude-code/plugins/ | grep custom
# Should not list our plugin
```

---

## Getting Help

### Documentation

- **Installation Issues** → This file (SETUP.md)
- **Architecture Questions** → docs/ARCHITECTURE.md
- **Learning Paths** → docs/LEARNING-PATHS.md
- **Integration** → docs/INTEGRATION-GUIDE.md
- **Common Problems** → docs/TROUBLESHOOTING.md

### Support Channels

- 📧 **Email**: support@example.com
- 💬 **GitHub Issues**: Report bugs
- 📚 **Documentation**: Complete guides
- 🤝 **Contributing**: Help improve plugin

---

## Next Steps

1. ✅ Install plugin (choose method above)
2. ✅ Run `/learn` to verify
3. ✅ Read docs/ARCHITECTURE.md to understand structure
4. ✅ Try `/assess` to self-evaluate
5. ✅ Choose learning path with `/learn`
6. ✅ Start building projects with `/projects`

**Happy learning! 🚀**
