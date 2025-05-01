Here's a complete cheatsheet covering **npm**, **pnpm**, **bun**, and **yarn** CLI commands in a well-structured `README.md` format. It includes the most common tasks across all tools—installing, updating, running scripts, managing dependencies, etc.

---

### 📦 Node Package Manager CLI Cheatsheet (`npm`, `pnpm`, `yarn`, `bun`)

> A unified command reference for popular Node.js package managers.

---

## 📁 Table of Contents

- [Installation](#installation)
- [Initialize Project](#initialize-project)
- [Install Dependencies](#install-dependencies)
- [Install Dev Dependencies](#install-dev-dependencies)
- [Global Install](#global-install)
- [Remove Dependencies](#remove-dependencies)
- [Update Packages](#update-packages)
- [Run Scripts](#run-scripts)
- [List Installed Packages](#list-installed-packages)
- [Audit & Fix](#audit--fix)
- [Cache Commands](#cache-commands)
- [Workspaces Support](#workspaces-support)
- [Executables & Temporary Package Execution](#executables--temporary-package-execution)
- [Misc](#misc)

---

## 📥 Installation

| Tool | Install Command |
|------|-----------------|
| **npm** | Comes with Node.js |
| **yarn** | `npm install -g yarn` |
| **pnpm** | `npm install -g pnpm` |
| **bun** | `curl -fsSL https://bun.sh/install | bash` |

---

## 🚀 Initialize Project

```bash
npm init            # Interactive
npm init -y         # Default

yarn init           # Interactive
yarn init -y        # Default

pnpm init           # Interactive
pnpm init -y        # Default

bun init            # Scaffolds full project (incl. ts, tests, etc.)
```

---

## 📦 Install Dependencies

```bash
npm install <pkg>

yarn add <pkg>

pnpm add <pkg>

bun add <pkg>
```

---

## 🧪 Install Dev Dependencies

```bash
npm install <pkg> --save-dev

yarn add <pkg> --dev

pnpm add -D <pkg>

bun add -d <pkg>
```

---

## 🌐 Global Install

```bash
npm install -g <pkg>

yarn global add <pkg>

pnpm add -g <pkg>

bun add -g <pkg>
```

---

## ❌ Remove Dependencies

```bash
npm uninstall <pkg>

yarn remove <pkg>

pnpm remove <pkg>

bun remove <pkg>
```

---

## 🔁 Update Packages

```bash
npm update

yarn upgrade

pnpm update

bun upgrade
```

> For specific packages:

```bash
npm install <pkg>@latest

yarn upgrade <pkg>

pnpm update <pkg>

bun upgrade <pkg>
```

---

## 🔧 Run Scripts

```bash
npm run <script>
npm start         # Runs 'start' script

yarn <script>
yarn start

pnpm run <script>
pnpm start

bun run <script>
```

---

## 📋 List Installed Packages

```bash
npm list           # Local
npm list -g        # Global

yarn list

pnpm list

bun pm ls          # For bun
```

---

## 🔍 Audit & Fix

```bash
npm audit
npm audit fix

yarn audit

pnpm audit

# Bun doesn't currently support audit directly
```

---

## 🧹 Cache Commands

```bash
npm cache clean --force
npm cache verify

yarn cache clean

pnpm store prune
pnpm store path

bun pm cache clean
```

---

## 🧩 Workspaces Support

| Feature        | npm       | yarn       | pnpm       | bun (partial) |
|----------------|-----------|------------|------------|---------------|
| Workspaces     | ✅ v7+     | ✅ native   | ✅ native   | ⚠️ Limited     |
| Command        | `workspaces` | `workspaces` | `--filter` | not fully stable |

---

## ⚡ Executables & Temporary Package Execution

| Command     | Purpose                                                |
|-------------|--------------------------------------------------------|
| `npx <pkg>` | Execute CLI tools without global install (npm)        |
| `pnpm dlx <pkg>` | Like `npx`, fetches and runs package (pnpm)        |
| `yarn dlx <pkg>` | Similar to `npx`, works with Yarn 3+              |
| `bunx <pkg>` | Bun’s fast version of `npx`                          |
| `pnpm exec <cmd>` | Runs command from a package's bin (like `npx`)   |

### 🔍 Examples

```bash
npx create-react-app my-app
pnpm dlx create-react-app my-app
yarn dlx create-react-app my-app
bunx create-react-app my-app

pnpm exec jest   # run local jest
npm exec eslint .
```

**Notes:**
- `npx` is part of npm >= 5.2+
- `bunx` is usually faster as it skips global cache writes
- `pnpm dlx` creates an isolated environment each time
- `pnpm exec` runs binary already in dependencies (like `npm exec`)

---

## ⚙️ Misc

### Install All Packages
```bash
npm install

yarn

pnpm install

bun install
```

### Lockfiles
| Tool   | Lockfile        |
|--------|-----------------|
| npm    | `package-lock.json` |
| yarn   | `yarn.lock`          |
| pnpm   | `pnpm-lock.yaml`     |
| bun    | `bun.lockb`          |

---

## 📚 Notes

- **pnpm** uses a symlink strategy for speed & disk efficiency.
- **bun** is a runtime + package manager with ultra-fast performance.
- **yarn 2+** has a different architecture (`Zero-Install`, `Plug’n’Play`).
- All support `.npmrc` or tool-specific RC files for config overrides.


