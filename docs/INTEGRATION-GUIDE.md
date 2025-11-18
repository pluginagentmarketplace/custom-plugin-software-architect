# 🔗 Agent-Skill-Command Integration Guide

Complete mapping of how agents, skills, commands, and hooks integrate seamlessly.

## Table of Contents

- [Quick Reference](#quick-reference)
- [Agent-Skill Mapping](#agent-skill-mapping)
- [Command Integration](#command-integration)
- [Hook Integration](#hook-integration)
- [User Workflows](#user-workflows)
- [Extension Points](#extension-points)

---

## Quick Reference

### Component Relationships

```
┌─────────────────────────────────────────────────────────┐
│                   7 AGENTS                              │
├─────────────────────────────────────────────────────────┤
│ 01      02         03         04        05      06    07 │
│Frontend Backend   Mobile    AI/ML    DevOps  Database Fund│
└────┬────┬──────┬──────┬────────┬────────┬─────────┬──────┘
     │    │      │      │        │        │         │
     ↓    ↓      ↓      ↓        ↓        ↓         ↓
┌─────────────────────────────────────────────────────────┐
│              7 SKILLS (SKILL.md files)                   │
├─────────────────────────────────────────────────────────┤
│ frontend backend mobile data-sci infrastructure database fund│
└─────────────────────────────────────────────────────────┘

     ↕              ↕             ↕

┌─────────────────────────────────────────────────────────┐
│           4 COMMANDS (route to agents/skills)           │
├─────────────────────────────────────────────────────────┤
│ /learn    /roadmap   /assess    /projects               │
└─────────────────────────────────────────────────────────┘

     ↕              ↕             ↕

┌─────────────────────────────────────────────────────────┐
│       10 HOOKS (provide automation & tracking)          │
└─────────────────────────────────────────────────────────┘
```

---

## Agent-Skill Mapping

### 1:1 Primary Mapping

```
AGENT                           ↔ SKILL FILE
────────────────────────────────────────────────
01-Frontend Development         → frontend-development/SKILL.md
02-Backend API Development      → backend-development/SKILL.md
03-Mobile Game Development      → mobile-development/SKILL.md
04-Data Science & AI           → data-science/SKILL.md
05-Infrastructure DevOps       → infrastructure/SKILL.md
06-Database Management         → database/SKILL.md
07-Fundamentals & Career       → fundamentals/SKILL.md
```

### Detailed Integration Points

#### Agent 01: Frontend Development

```
Agent File: agents/01-frontend-development.md
├─ Overview: 10 frontend roles
├─ Topics: 86+ skill categories
├─ Technologies: React, Vue, Angular, CSS, etc.
└─ Invokes: frontend-development/SKILL.md

Skill File: skills/frontend-development/SKILL.md
├─ Quick Start: Simple React component (5 min)
├─ Foundation: HTML/CSS/JS basics
├─ Intermediate: React hooks, state management
├─ Advanced: Design systems, performance
├─ Projects: 10+ project ideas
└─ Resources: Books, courses, documentation

Integration Links:
├─ Agent mentions → Quick Start in SKILL
├─ SKILL suggests → /projects for hands-on
├─ /assess recommends → This agent/skill
├─ /learn routes → This agent
└─ Hooks track → Progress in this domain

Cross-Agent Links:
├─ To Backend Agent (for full-stack)
├─ To DevOps Agent (for deployment)
└─ To Fundamentals Agent (for CS basics)
```

#### Agent 02: Backend API Development

```
Agent File: agents/02-backend-api-development.md
├─ Overview: 10 backend roles
├─ Topics: 1,073+ topics
├─ Technologies: Node.js, Python, Java, Go, etc.
└─ Invokes: backend-development/SKILL.md

Skill File: skills/backend-development/SKILL.md
├─ Quick Start: Simple REST API (5 min)
├─ Foundation: HTTP, frameworks, databases
├─ Intermediate: APIs, authentication, caching
├─ Advanced: Microservices, GraphQL
├─ Projects: 10+ project ideas
└─ Resources: Full documentation

Integration Links:
├─ Agent mentions → Quick Start in SKILL
├─ SKILL suggests → /projects for hands-on
├─ /assess recommends → This agent/skill
├─ /learn routes → This agent
└─ Hooks track → Progress in this domain

Cross-Agent Links:
├─ To Frontend Agent (for full-stack)
├─ To Database Agent (for data modeling)
├─ To DevOps Agent (for deployment)
└─ To Fundamentals Agent (for system design)
```

#### Agent 03: Mobile Game Development

```
Agent File: agents/03-mobile-game-development.md
├─ Overview: 7 mobile/game roles
├─ Platforms: iOS, Android, React Native, Flutter, Unity
├─ Technologies: Swift, Kotlin, Dart, C#
└─ Invokes: mobile-development/SKILL.md

Skill File: skills/mobile-development/SKILL.md
├─ Quick Start: Simple app with framework (5 min)
├─ Foundation: Platform basics, navigation
├─ Intermediate: UI/UX, APIs, data persistence
├─ Advanced: Native integration, optimization
├─ Projects: 10+ project ideas
└─ Resources: Official docs, tutorials

Integration Links:
├─ Agent mentions → Quick Start in SKILL
├─ SKILL suggests → /projects for hands-on
├─ /assess recommends → This agent/skill
├─ /learn routes → This agent
└─ Hooks track → Progress in this domain

Cross-Agent Links:
├─ To Backend Agent (for APIs)
├─ To DevOps Agent (for deployment)
└─ To Fundamentals Agent (for fundamentals)
```

#### Agent 04: Data Science & AI

```
Agent File: agents/04-data-science-ai.md
├─ Overview: 10 AI/ML/Data roles
├─ Topics: 1,000+ skills
├─ Path: Prompt Eng (2-4 wks) → AI Eng → ML Eng
└─ Invokes: data-science/SKILL.md

Skill File: skills/data-science/SKILL.md
├─ Quick Start: Simple prompt with LLM API (5 min)
├─ Foundation: Python, SQL, statistics
├─ Intermediate: ML, Deep Learning, GenAI
├─ Advanced: Production ML, specializations
├─ Projects: 10+ project ideas
└─ Resources: ML platforms, courses

Integration Links:
├─ Agent mentions → Quick Start in SKILL
├─ SKILL suggests → /projects for hands-on
├─ /assess recommends → This agent/skill
├─ /learn routes → This agent
└─ Hooks track → Progress in this domain

Cross-Agent Links:
├─ To Backend Agent (for model serving)
├─ To DevOps Agent (for infrastructure)
├─ To Database Agent (for data warehousing)
└─ To Fundamentals Agent (for CS basics)

Special: FASTEST PATH
├─ Prompt Engineering: 2-4 weeks
├─ Build real app: 4-8 weeks
└─ Total to AI Engineer: 6-12 weeks
```

#### Agent 05: Infrastructure & DevOps

```
Agent File: agents/05-infrastructure-devops.md
├─ Overview: 5 DevOps/Cloud roles
├─ Topics: 600+ sections
├─ Technologies: 100+ tools (Docker, K8s, AWS, etc.)
└─ Invokes: infrastructure/SKILL.md

Skill File: skills/infrastructure/SKILL.md
├─ Quick Start: Dockerize simple app (5 min)
├─ Foundation: Linux, Docker, Git
├─ Intermediate: Kubernetes, CI/CD, cloud basics
├─ Advanced: Terraform, multi-cloud, architecture
├─ Projects: 10+ project ideas
└─ Resources: Cloud docs, certifications

Integration Links:
├─ Agent mentions → Quick Start in SKILL
├─ SKILL suggests → /projects for hands-on
├─ /assess recommends → This agent/skill
├─ /learn routes → This agent
└─ Hooks track → Progress in this domain

Cross-Agent Links:
├─ From Backend Agent (deploy services)
├─ From Frontend Agent (deploy sites)
├─ From Mobile Agent (deploy backends)
├─ From Data Science Agent (ML infrastructure)
└─ From Database Agent (manage databases)

Support Role:
├─ Enables other agents
├─ Required for production systems
└─ Essential for scaling
```

#### Agent 06: Database Management

```
Agent File: agents/06-database-management.md
├─ Overview: 6 database roles
├─ Topics: 400+ competencies
├─ Systems: PostgreSQL, MongoDB, Redis, Blockchain
└─ Invokes: database/SKILL.md

Skill File: skills/database/SKILL.md
├─ Quick Start: Simple database design (5 min)
├─ Foundation: SQL, normalization, modeling
├─ Intermediate: PostgreSQL/MongoDB advanced
├─ Advanced: Optimization, HA, Blockchain
├─ Projects: 10+ project ideas
└─ Resources: DB docs, optimization guides

Integration Links:
├─ Agent mentions → Quick Start in SKILL
├─ SKILL suggests → /projects for hands-on
├─ /assess recommends → This agent/skill
├─ /learn routes → This agent
└─ Hooks track → Progress in this domain

Cross-Agent Links:
├─ From Backend Agent (data storage)
├─ From Frontend Agent (via backend)
├─ From Data Science Agent (data warehouse)
├─ From DevOps Agent (infrastructure)
└─ From Mobile Agent (via backend)

Cross-Cutting:
├─ Supports all other agents
├─ Critical for data integrity
└─ Performance key to all systems
```

#### Agent 07: Fundamentals & Career

```
Agent File: agents/07-fundamentals-career.md
├─ Overview: 9 fundamental roles
├─ Topics: 1,200+ topics
├─ Paths: CS → Algorithms → System Design → Leadership
└─ Invokes: fundamentals/SKILL.md

Skill File: skills/fundamentals/SKILL.md
├─ Quick Start: Algorithm problem (5 min)
├─ Foundation: CS theory, data structures
├─ Intermediate: Algorithms, design patterns
├─ Advanced: System design, leadership
├─ Projects: Interview prep, system design
└─ Resources: Books, problem sites, mentoring

Integration Links:
├─ Agent mentions → Quick Start in SKILL
├─ SKILL suggests → /projects for hands-on
├─ /assess recommends → This agent/skill
├─ /learn routes → This agent
└─ Hooks track → Progress in this domain

Cross-Agent Links:
├─ Foundation for all agents
├─ Leadership path for career progression
├─ System design for architecture
└─ Algorithms for interviews

Career Path Integration:
├─ Junior Dev (years 0-2): Strong fundamentals
├─ Mid-level (years 2-5): Specialization
├─ Senior (years 5-10): Mastery + leadership
└─ Manager (years 10+): Full transformation

Special: PREREQUISITE AGENT
├─ Recommended starting point
├─ Supports all other learning
└─ Enables better understanding of everything
```

---

## Command Integration

### /learn Command Integration

```
Command File: commands/learn.md
│
├─ Display learning paths
├─ User selects goal
├─ Agent router (context-analyzer hook)
├─ Agent invoked (01-07 agents)
├─ Skill recommended (SKILL.md)
├─ Projects linked (/projects)
└─ Progress tracked (hook)

Example Flow:
User: /learn
  ↓
Plugin: [Display path options]
User: Full-stack development
  ↓
Hook: agent-context-loader
  ↓
Agent: 01-Frontend + 02-Backend Invoked
  ↓
Response: "I recommend starting with Frontend..."
  ↓
Suggest: frontend-development/SKILL.md
  ↓
Link: /projects for project ideas
  ↓
Hook: learning-progress-tracker (recorded)
```

### /roadmap Command Integration

```
Command File: commands/roadmap.md
│
├─ Display all 65+ roles
├─ Show technologies
├─ Display time estimates
├─ Show salaries
├─ Link to agents (/learn)
└─ Exploration logged (hook)

Example Flow:
User: /roadmap
  ↓
Plugin: [Display role browser]
User: Explore AI roles
  ↓
Plugin: [Show 10 AI/ML roles]
  ↓
User: Learn about ML Engineer
  ↓
Link: /learn → 04-Data Science & AI Agent
  ↓
Hook: role-focus-detector (records interest)
```

### /assess Command Integration

```
Command File: commands/assess.md
│
├─ Present questionnaire
├─ Collect skill ratings (1-5)
├─ Analyze responses (hook)
├─ Generate report
├─ Recommend agent
├─ Suggest SKILL.md
├─ Link to /projects
└─ Create learning plan (hook)

Example Flow:
User: /assess
  ↓
Plugin: [Questions across 7 domains]
User: [Rates skills]
  ↓
Hook: assessment-feedback-generator
  ↓
Report:
├─ Level: Intermediate
├─ Strengths: JavaScript, React
├─ Gaps: TypeScript, Performance
├─ Agent: 01-Frontend Development
├─ Skill: frontend-development/SKILL.md
├─ Next: TypeScript Advanced Patterns
└─ Timeline: 8-12 weeks
  ↓
Link: /projects for aligned projects
  ↓
Hook: learning-pace-monitor (sets baseline)
```

### /projects Command Integration

```
Command File: commands/projects.md
│
├─ Display projects (50+)
├─ Filter by difficulty
├─ User selects project
├─ Check prerequisites (hook)
├─ If missing: Suggest /learn
├─ Else: Start project
├─ Track progress (hook)
└─ Celebrate completion (hook)

Example Flow:
User: /projects
  ↓
Plugin: [Beginner/Intermediate/Advanced projects]
User: E-commerce Site (Intermediate)
  ↓
Hook: skill-dependency-validator
  ├─ Needs: Frontend (check ✓)
  ├─ Needs: Backend (check ?)
  └─ Needs: DevOps (check ?)
  ↓
Plugin: "You need Backend basics"
  ↓
Suggest: /learn → 02-Backend Agent
  ↓
Or: "Start project, learn along"
  ↓
Track: Project progress (hook)
  ↓
Milestone: Project completion
  ↓
Celebrate: "Great job! Next project?"
```

---

## Hook Integration

### Hook Triggering Points

```
TRIGGER              HOOKS ACTIVATED           ACTION
─────────────────────────────────────────────────────
/learn executed    → learning-progress-tracker    Track selection
                   → agent-context-loader          Route to agent
                   → command-navigation           Suggest next

agent invoked      → learning-progress-tracker    Track invocation
                   → skill-coverage-tracker       Mark coverage
                   → role-focus-detector          Identify interests

skill requested    → skill-dependency-validator   Check prereqs
                   → learning-progress-tracker    Track engagement
                   → skill-coverage-tracker       Mark skill learned

/assess response   → assessment-feedback          Generate report
                   → learning-pace-monitor        Adjust pacing
                   → project-recommendation       Suggest projects

/projects selection → project-recommendation      Filter projects
                   → skill-dependency-validator   Check prereqs
                   → learning-progress-tracker    Track project choice

completion event   → learning-progress-tracker    Record milestone
                   → learning-pace-monitor        Adjust pace
                   → project-recommendation       Suggest next project

daily check-in     → learning-pace-monitor        Assess pace
                   → project-recommendation       Suggest projects
                   → learning-progress-tracker    Weekly recap
```

### Hook-Command Integration

| Command | Hooks |
|---------|-------|
| **/learn** | agent-context-loader, learning-progress-tracker, command-navigation-enhancer |
| **/roadmap** | role-focus-detector, learning-progress-tracker |
| **/assess** | assessment-feedback-generator, learning-pace-monitor, project-recommendation-engine |
| **/projects** | project-recommendation-engine, skill-dependency-validator, learning-progress-tracker |

---

## User Workflows

### Workflow 1: Complete Beginner

```
Step 1: /assess
  → Identify current level
  → Find strengths & gaps

Step 2: /learn
  → Choose path (e.g., Full-Stack)
  → Get assigned agent (Frontend + Backend)
  → Receive learning plan

Step 3: frontend-development/SKILL.md
  → Quick start (5 min)
  → Learn foundation
  → Build project

Step 4: /projects
  → Find beginner projects
  → Build portfolio
  → Track progress

Step 5: Intermediate content
  → Progress through levels
  → Expand skills
  → Specialize

Step 6: /assess (repeat)
  → Re-evaluate skills
  → Identify new gaps
  → Plan next phase
```

### Workflow 2: Career Changer

```
Step 1: /roadmap
  → Explore all options
  → Understand time/salaries
  → Research roles

Step 2: /assess
  → Evaluate current skills
  → Find transferable skills
  → Identify gaps

Step 3: /learn
  → Choose new career
  → Get learning plan
  → Start agent-guided learning

Step 4: Focused learning
  → Complete SKILL.md sections
  → Build targeted projects
  → Develop new skills

Step 5: Fast tracks (optional)
  → If time-constrained
  → Prompt Engineering path (2-4 wks)
  → Quick wins

Step 6: Portfolio building
  → /projects for portfolio pieces
  → Build 3-5 strong projects
  → Prepare for interviews
```

### Workflow 3: Team Training

```
Step 1: Manager uses /roadmap
  → Assess team against roles
  → Identify skill gaps

Step 2: Run /assess for team
  → Evaluate each member
  → Create development plans

Step 3: /learn paths
  → Create team learning groups
  → Assign agents for focus areas

Step 4: Skill rotation
  → Different agents/skills
  → Cross-train team
  → Improve versatility

Step 5: Track progress
  → Use hooks for team metrics
  → Celebrate milestones
  → Adjust pace

Step 6: Career development
  → Plan promotions
  → Identify specialists
  → Support leadership growth
```

---

## Extension Points

### How to Add New Agent

```
1. Create: agents/08-new-domain.md
   ├─ YAML frontmatter
   ├─ Overview
   ├─ 5+ new roles
   ├─ Technologies
   ├─ Learning paths
   └─ Integration links

2. Create SKILL: skills/new-domain/SKILL.md
   ├─ Quick start
   ├─ Learning levels
   ├─ Code examples
   ├─ Projects
   └─ Resources

3. Update plugin.json:
   "agents": [..., "08-new-domain"]
   "skills": [..., "new-domain/SKILL"]

4. Update hooks.json:
   ├─ Add agent routing keyword
   ├─ Register new agent

5. Update all integration links:
   ├─ Link from related agents
   ├─ Update /roadmap
   ├─ Update learning paths

6. Document:
   ├─ Update LEARNING-PATHS.md
   ├─ Update this guide
   └─ Add to CHANGELOG.md
```

### How to Add New Command

```
1. Create: commands/new-command.md
   ├─ Purpose
   ├─ Features
   ├─ Usage
   ├─ Examples
   └─ Related commands

2. Update plugin.json:
   "commands": [..., "new-command"]

3. Add hooks (if needed):
   └─ hooks/hooks.json

4. Link from other commands:
   ├─ Related commands section
   ├─ Cross-references
   └─ Workflow integration

5. Document integration:
   ├─ This guide
   ├─ ARCHITECTURE.md
   └─ CHANGELOG.md
```

---

<div align="center">

### Perfect Integration ✅

All components work seamlessly together to create a unified learning experience.

**Every agent connects to its skill.**
**Every command routes to the right agent/skill.**
**Every hook provides automated support.**

</div>
