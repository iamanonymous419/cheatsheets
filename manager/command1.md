# 📦 Node.js Package Managers CLI Cheatsheet

> Covers **npm**, **yarn**, **pnpm**, and **bun** with comprehensive commands.

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
- [Lockfiles](#lockfiles)
- [Install Specific Version](#install-specific-version)
- [Install from Git/URL/Path](#install-from-giturlpath)
- [Environment Variables](#environment-variables)
- [Publish Package](#publish-package)
- [Set Registry](#set-registry)
- [Rebuild Native Modules](#rebuild-native-modules)
- [Run Binaries from Node Modules](#run-binaries-from-node-modules)
- [Other Helpful Commands](#other-helpful-commands)

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
npm init [-y]
yarn init [-y]
pnpm init [-y]
bun init
```

---

## 📦 Install Dependencies

```bash
npm install <pkg>
yarn add <pkg>
pnpm add <pkg>
bun add <pkg>
```

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

For specific packages:
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
yarn <script>
pnpm run <script>
bun run <script>
```

---

## 📋 List Installed Packages

```bash
npm list [--depth=0]
yarn list
pnpm list
bun pm ls
```

---

## 🔍 Audit & Fix

```bash
npm audit && npm audit fix
yarn audit
pnpm audit
# bun - audit not fully supported
```

---

## 🧹 Cache Commands

```bash
npm cache clean --force && npm cache verify
yarn cache clean
pnpm store prune && pnpm store path
bun pm cache clean
```

---

## 🧩 Workspaces Support

| Feature    | npm    | yarn   | pnpm   | bun       |
|------------|--------|--------|--------|-----------|
| Workspaces | ✅ v7+ | ✅      | ✅      | ⚠️ Partial |

---

## 🔒 Lockfiles

| Tool  | Lockfile          |
|-------|-------------------|
| npm   | `package-lock.json` |
| yarn  | `yarn.lock`         |
| pnpm  | `pnpm-lock.yaml`    |
| bun   | `bun.lockb`         |

---

## 📌 Install Specific Version

```bash
npm install <pkg>@1.2.3
yarn add <pkg>@1.2.3
pnpm add <pkg>@1.2.3
bun add <pkg>@1.2.3
```

---

## 🔗 Install from Git/URL/Path

```bash
npm install git+https://url
npm install ./local-folder

yarn add https://url
yarn add file:./local-folder

pnpm add https://url
pnpm add ./local-folder

bun add https://url
bun add ./local-folder
```

---

## 🌱 Environment Variables

Run a script with env:
```bash
MY_ENV=production npm run build
cross-env MY_ENV=production npm run build
```

Same applies to other tools (`yarn`, `pnpm`, `bun`).

---

## 📤 Publish Package

```bash
npm publish
yarn publish
pnpm publish
bun publish
```

---

## 🌐 Set Registry

```bash
npm config set registry <url>
yarn config set registry <url>
pnpm config set registry <url>
bun config set registry <url>
```

---

## 🔧 Rebuild Native Modules

```bash
npm rebuild
yarn rebuild
pnpm rebuild
bun rebuild
```

---

## 🏃 Run Binaries from Node Modules

```bash
npx <command>
yarn dlx <command>
pnpm dlx <command>
bunx <command>
```

---

## 🧠 Other Helpful Commands

```bash
npm outdated            # Show outdated packages
npm ci                  # Clean install (from lockfile only)
yarn autoclean --init   # Enable cleaning
pnpm why <pkg>          # Why a dependency is installed
bun pm why <pkg>        # Similar for bun
```

---

## ✅ Recommendations

- Use **`pnpm`** for large monorepos (speed + disk efficiency)
- Use **`bun`** for ultra-fast installs and native bundling
- Use **`yarn`** for Plug'n'Play or zero-install setups
- Stick with **`npm`** if using vanilla Node.js without extra tools

---

> Feel free to copy, fork, and customize this cheatsheet for your team or open-source project!


