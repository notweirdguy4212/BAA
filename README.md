# ⚡ Build Anything (BAA)

**The agent-native engineering workbench**

Understand systems. Generate projects. Inspect evidence. Verify what changed.

[![Node.js](https://img.shields.io/badge/Node.js-22%2B-43853D?logo=node.js&logoColor=white)](https://nodejs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-first-3178C6?logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![MCP](https://img.shields.io/badge/MCP-enabled-6E56CF)](https://modelcontextprotocol.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## Overview

**Build Anything (BAA)** is a local-first engineering toolkit for developers and AI agents. It unites project scaffolding workflows, deep software analysis, and artifact-inspection capabilities behind both a command-line interface (CLI) and a Model Context Protocol (MCP) server.

BAA is designed to guide agents and developers from *understanding a codebase* to *generating starter architectures* and *verifying structural integrity*—all while keeping actions bounded, inspectable, and backed by verifiable evidence.

> **The BAA Principle:** Make useful engineering actions available as bounded tools, return concrete evidence, and never claim a check happened when it did not.

---

## ✨ Key Capabilities

| Capability | Purpose |
|---|---|
| **Project Discovery** | Inspect a local source tree and produce a bounded analysis of its structure, dependencies, and candidates. |
| **Project Generation** | Scaffolds starter projects for supported targets without silently overwriting existing files. |
| **Structural Verification** | Automatically validates generated manifests, directory topologies, and required entry files. |
| **Source & Runtime Inspection** | Inspect runtime artifacts, binaries, and devices via specialized tool contracts (including Android/ADB, APK analysis, decompilation, and firmware). |
| **Agent & MCP Integration** | Exposes operations as tools via the Model Context Protocol (MCP) across stdio and streamable HTTP transports. |
| **CLI Workflows** | Execute setup, project discovery, generation, and verification directly from a local terminal. |

### Supported Starter Targets

BAA includes built-in starter generation targets for:
- **Web & Desktop:** React, Next.js, Vue, Electron, Tauri
- **Mobile:** Flutter, React Native, SwiftUI, Jetpack Compose
- **Game Engines & Metaverses:** Unity, Unreal Engine, Roblox

---

## 🛠️ Technology Stack

Inferred directly from the repository structure and tool contracts:

- **Core Runtime & Language:** Node.js (ESM), TypeScript
- **Package Management:** npm
- **Protocol Standard:** Model Context Protocol (MCP) via `server.json` and `.codex-plugin/mcp.json`
- **Tooling & Git Hooks:** Husky (`.husky/pre-commit`, `.husky/pre-push`), Release-Please
- **Target Analysis & Reverse Engineering Bridges:**
  - **Android / Mobile:** Android Debug Bridge (ADB), APKtool, APK signature verification
  - **Binary & Decompilation:** Ghidra (MIPS, relocatables), Cutter, Frida
  - **Virtual Machines & Runtimes:** EVM (Ethereum Virtual Machine) contracts, Erlang BEAM
  - **Embedded:** Firmware tool contracts and requirement checks
  - **Headless Testing:** Browser scenario and browser provider tools
- **Ecosystem Providers:** Anthropic Claude (`.claude-plugin/`), OpenAI Codex (`.codex-plugin/`), ChatGPT, GitHub Copilot, Google Gemini, Cursor, Windsurf, LM Studio, and Ollama

---

## 🚀 Getting Started

### System Requirements

- **Node.js:** `22.23.4+`, `24.22.1+`, or `26.12.1+`
- **npm:** `11+`
- Optional: Android SDK Platform-Tools (for ADB tools), Termux environment (see `TERMUX-INSTALL.txt`)

### Installation from Source

```bash
git clone https://github.com/notweirdguy4212/BAA.git
cd BAA
npm ci
npm run build:cached
node scripts/baa.mjs setup
```

> **Note:** If your local checkout directory has a different name, run the commands from that directory. Always build BAA (`npm run build:cached`) before launching its MCP server for the first time.

---

## 💻 CLI Usage

BAA provides project workflows via `scripts/baa.mjs`:

```bash
# Display available starter targets
node scripts/baa.mjs project targets

# Analyze an existing local codebase and export findings
node scripts/baa.mjs project analyze ./existing-project --out ./baa-analysis.json

# Generate a starter project safely (will not overwrite files)
node scripts/baa.mjs project generate --target react --out ./new-project --name "My App"

# Verify the structure and manifests of a generated project
node scripts/baa.mjs project verify ./new-project
```

To see all available commands and flags, run:
```bash
node scripts/baa.mjs --help
```

---

## 🤖 Connect an MCP Client

BAA integrates natively into MCP-compatible clients (e.g., Claude Desktop, Cursor, Windsurf, or Codex plugins).

Add the following entry to your client's MCP configuration file, replacing `/absolute/path/to/BAA` with the real path on your system:

```json
{
  "mcpServers": {
    "baa": {
      "command": "node",
      "args": ["/absolute/path/to/BAA/scripts/baa.m