<div align="center">

<!-- Animated Typing Banner -->
<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=28&duration=3000&pause=1000&color=2E9EF7&center=true&vCenter=true&multiline=true&repeat=true&width=600&height=100&lines=Software+Architect+Assistant;7+Agents+%7C+7+Skills;Claude+Code+Plugin" alt="Software Architect Assistant" />

<br/>

<!-- Badge Row 1: Status Badges -->
[![Version](https://img.shields.io/badge/Version-1.0.0-blue?style=for-the-badge)](https://github.com/pluginagentmarketplace/custom-plugin-software-architect/releases)
[![License](https://img.shields.io/badge/License-Custom-yellow?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Production-brightgreen?style=for-the-badge)](#)
[![SASMP](https://img.shields.io/badge/SASMP-v1.3.0-blueviolet?style=for-the-badge)](#)

<!-- Badge Row 2: Content Badges -->
[![Agents](https://img.shields.io/badge/Agents-7-orange?style=flat-square&logo=robot)](#-agents)
[![Skills](https://img.shields.io/badge/Skills-7-purple?style=flat-square&logo=lightning)](#-skills)
[![Commands](https://img.shields.io/badge/Commands-4-green?style=flat-square&logo=terminal)](#-commands)

<br/>

<!-- Quick CTA Row -->
[📦 **Install Now**](#-quick-start) · [🤖 **Explore Agents**](#-agents) · [📖 **Documentation**](#-documentation) · [⭐ **Star this repo**](https://github.com/pluginagentmarketplace/custom-plugin-software-architect)

---

### What is this?

> **Software Architect Assistant** is a Claude Code plugin with **7 agents** and **7 skills** for software architect development.

</div>

---

## 📑 Table of Contents

<details>
<summary>Click to expand</summary>

- [Quick Start](#-quick-start)
- [Features](#-features)
- [Agents](#-agents)
- [Skills](#-skills)
- [Commands](#-commands)
- [Documentation](#-documentation)
- [Contributing](#-contributing)
- [License](#-license)

</details>

---

## 🚀 Quick Start

### Prerequisites

- Claude Code CLI v2.0.27+
- Active Claude subscription

### Installation (Choose One)

<details open>
<summary><strong>Option 1: From Marketplace (Recommended)</strong></summary>

```bash
# Step 1️⃣ Add the marketplace
/plugin add marketplace pluginagentmarketplace/custom-plugin-software-architect

# Step 2️⃣ Install the plugin
/plugin install software-architect-assistant@pluginagentmarketplace-software-architect

# Step 3️⃣ Restart Claude Code
# Close and reopen your terminal/IDE
```

</details>

<details>
<summary><strong>Option 2: Local Installation</strong></summary>

```bash
# Clone the repository
git clone https://github.com/pluginagentmarketplace/custom-plugin-software-architect.git
cd custom-plugin-software-architect

# Load locally
/plugin load .

# Restart Claude Code
```

</details>

### ✅ Verify Installation

After restart, you should see these agents:

```
software-architect-assistant:05-infrastructure-devops
software-architect-assistant:03-mobile-game-development
software-architect-assistant:01-frontend-development
software-architect-assistant:06-database-management
software-architect-assistant:02-backend-api-development
... and 2 more
```

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🤖 **7 Agents** | Specialized AI agents for software architect tasks |
| 🛠️ **7 Skills** | Reusable capabilities with Golden Format |
| ⌨️ **4 Commands** | Quick slash commands |
| 🔄 **SASMP v1.3.0** | Full protocol compliance |

---

## 🤖 Agents

### 7 Specialized Agents

| # | Agent | Purpose |
|---|-------|---------|
| 1 | **05-infrastructure-devops** | Infrastructure and DevOps specialist covering Docker, Kubern |
| 2 | **03-mobile-game-development** | Mobile and Game Development specialist covering React Native |
| 3 | **01-frontend-development** | Frontend Development specialist covering HTML, CSS, JavaScri |
| 4 | **06-database-management** | Database and Data Management specialist covering PostgreSQL, |
| 5 | **02-backend-api-development** | Backend and API Development specialist covering Node.js, PHP |
| 6 | **07-fundamentals-career** | Fundamentals and Career Development specialist covering Comp |
| 7 | **04-data-science-ai** | Data Science and AI specialist covering AI Engineers, Data S |

---

## 🛠️ Skills

### Available Skills

| Skill | Description | Invoke |
|-------|-------------|--------|
| `database` | Master relational and NoSQL databases including PostgreSQL,  | `Skill("software-architect-assistant:database")` |
| `fundamentals` | Master foundational computer science concepts, data structur | `Skill("software-architect-assistant:fundamentals")` |
| `backend-development` | Build scalable backend systems with Node.js, Python, Java, G | `Skill("software-architect-assistant:backend-development")` |
| `mobile-development` | Build mobile applications for iOS, Android, and cross-platfo | `Skill("software-architect-assistant:mobile-development")` |
| `data-science` | Master machine learning, AI, data science, and GenAI applica | `Skill("software-architect-assistant:data-science")` |
| `frontend-development` | Modern web development with HTML, CSS, JavaScript, TypeScrip | `Skill("software-architect-assistant:frontend-development")` |
| `infrastructure` | Master cloud infrastructure, Kubernetes, Terraform, CI/CD, a | `Skill("software-architect-assistant:infrastructure")` |

---

## ⌨️ Commands

| Command | Description |
|---------|-------------|
| `/learn` | Learning Path Selector |
| `/assess` | Knowledge Assessment |
| `/projects` | Project Ideas & Portfolio Building |
| `/roadmap` | Technology Roadmap Explorer |

---

## 📚 Documentation

| Document | Description |
|----------|-------------|
| [CHANGELOG.md](CHANGELOG.md) | Version history |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to contribute |
| [LICENSE](LICENSE) | License information |

---

## 📁 Project Structure

<details>
<summary>Click to expand</summary>

```
custom-plugin-software-architect/
├── 📁 .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── 📁 agents/              # 7 agents
├── 📁 skills/              # 7 skills (Golden Format)
├── 📁 commands/            # 4 commands
├── 📁 hooks/
├── 📄 README.md
├── 📄 CHANGELOG.md
└── 📄 LICENSE
```

</details>

---

## 📅 Metadata

| Field | Value |
|-------|-------|
| **Version** | 1.0.0 |
| **Last Updated** | 2025-12-29 |
| **Status** | Production Ready |
| **SASMP** | v1.3.0 |
| **Agents** | 7 |
| **Skills** | 7 |
| **Commands** | 4 |

---

## 🤝 Contributing

Contributions are welcome! Please read our [Contributing Guide](CONTRIBUTING.md).

1. Fork the repository
2. Create your feature branch
3. Follow the Golden Format for new skills
4. Submit a pull request

---

## ⚠️ Security

> **Important:** This repository contains third-party code and dependencies.
>
> - ✅ Always review code before using in production
> - ✅ Check dependencies for known vulnerabilities
> - ✅ Follow security best practices
> - ✅ Report security issues privately via [Issues](../../issues)

---

## 📝 License

Copyright © 2025 **Dr. Umit Kacar** & **Muhsin Elcicek**

Custom License - See [LICENSE](LICENSE) for details.

---

## 👥 Contributors

<table>
<tr>
<td align="center">
<strong>Dr. Umit Kacar</strong><br/>
Senior AI Researcher & Engineer
</td>
<td align="center">
<strong>Muhsin Elcicek</strong><br/>
Senior Software Architect
</td>
</tr>
</table>

---

<div align="center">

**Made with ❤️ for the Claude Code Community**

[![GitHub](https://img.shields.io/badge/GitHub-pluginagentmarketplace-black?style=for-the-badge&logo=github)](https://github.com/pluginagentmarketplace)

</div>
