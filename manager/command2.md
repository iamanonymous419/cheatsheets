# JavaScript Package Manager Cheatsheet

A comprehensive reference guide for npm, pnpm, Yarn, and Bun CLI commands.

- [npm](#npm)
- [pnpm](#pnpm)
- [Yarn](#yarn)
- [Bun](#bun)
- [Common Operations Comparison](#common-operations-comparison)

## npm

### Installation & Setup
```bash
# Install npm (comes with Node.js)
$ curl -fsSL https://nodejs.org/install.sh | sh

# Check version
$ npm -v
```

### Managing Packages
```bash
# Install dependencies from package.json
$ npm install
$ npm i

# Install a package and add to dependencies
$ npm install <package>
$ npm i <package>

# Install a specific version
$ npm install <package>@<version>

# Install as dev dependency
$ npm install <package> --save-dev
$ npm i <package> -D

# Install globally
$ npm install -g <package>

# Uninstall a package
$ npm uninstall <package>

# Update packages
$ npm update
$ npm update <package>
```

### Package Scripts
```bash
# Run a script defined in package.json
$ npm run <script>

# Common built-in scripts
$ npm start
$ npm test
$ npm stop
```

### Package Management
```bash
# Initialize a new project
$ npm init
$ npm init -y  # Skip questions with defaults

# List installed packages
$ npm list
$ npm ls
$ npm ls --depth=0  # Show only top-level packages

# Show outdated packages
$ npm outdated

# Show package details
$ npm info <package>
$ npm view <package>

# Search packages
$ npm search <keyword>
```

### Dependencies
```bash
# Install production dependencies only
$ npm install --production
$ npm i --production

# Update package.json dependencies
$ npm install <package> --save-exact  # Exact version
$ npm i <package> -E  # Short for --save-exact

# Install optional dependencies
$ npm install <package> --save-optional
$ npm i <package> -O
```

### Version Management
```bash
# Check current version
$ npm version

# Update version (updates package.json)
$ npm version patch  # 1.0.0 -> 1.0.1
$ npm version minor  # 1.0.0 -> 1.1.0
$ npm version major  # 1.0.0 -> 2.0.0
```

### Publishing
```bash
# Create a user account
$ npm adduser

# Publish a package
$ npm publish

# Update package access
$ npm access public|restricted <package>

# Deprecate a version
$ npm deprecate <package>@<version> "<message>"
```

### Configuration
```bash
# Set config values
$ npm config set <key> <value>

# Get config value
$ npm config get <key>

# List all config settings
$ npm config list

# Delete config value
$ npm config delete <key>
```

### Cache
```bash
# Clean cache
$ npm cache clean --force

# Verify cache
$ npm cache verify
```

### Security
```bash
# Audit packages for vulnerabilities
$ npm audit

# Automatically fix vulnerabilities when possible
$ npm audit fix

# Run security audit without fixing
$ npm audit --no-fix
```

### Workspaces (monorepo)
```bash
# Run command in a specific workspace
$ npm run <script> --workspace=<name>
$ npm run <script> -w <name>

# Run command in all workspaces
$ npm run <script> --workspaces
$ npm run <script> -ws
```

## pnpm

### Installation & Setup
```bash
# Install pnpm
$ npm install -g pnpm

# Using npm
$ npm install -g pnpm

# Using curl for Linux/macOS
$ curl -fsSL https://get.pnpm.io/install.sh | sh -

# Check version
$ pnpm -v
```

### Managing Packages
```bash
# Install dependencies from package.json
$ pnpm install

# Install a package and add to dependencies
$ pnpm add <package>

# Install a specific version
$ pnpm add <package>@<version>

# Install as dev dependency
$ pnpm add -D <package>
$ pnpm add --save-dev <package>

# Install globally
$ pnpm add -g <package>
$ pnpm add --global <package>

# Uninstall a package
$ pnpm remove <package>
$ pnpm rm <package>

# Update packages
$ pnpm update
$ pnpm update <package>
```

### Package Scripts
```bash
# Run a script defined in package.json
$ pnpm <script>
$ pnpm run <script>

# Common built-in scripts
$ pnpm start
$ pnpm test
```

### Package Management
```bash
# Initialize a new project
$ pnpm init

# List installed packages
$ pnpm list
$ pnpm ls

# Show outdated packages
$ pnpm outdated

# Show package details
$ pnpm info <package>
```

### Dependencies
```bash
# Install production dependencies only
$ pnpm install --prod
$ pnpm install --production

# Install peer dependencies
$ pnpm install --no-optional  # Skip optional dependencies
```

### Store Management
```bash
# Store path
$ pnpm store path

# Prune store (remove unreferenced packages)
$ pnpm store prune

# Check store status
$ pnpm store status
```

### Workspaces (monorepo)
```bash
# Run a command in a specific workspace
$ pnpm --filter <package_name> <command>

# Run a command in all workspaces
$ pnpm -r <command>
$ pnpm --recursive <command>

# Execute in all packages that have changes
$ pnpm -r --filter="./packages/*" <command>

# Filter by dependencies
$ pnpm --filter <pkg_name>... <command>  # Package and its dependencies
$ pnpm --filter ...<pkg_name> <command>  # Package and its dependents
```

### Configuration
```bash
# Set config values
$ pnpm config set <key> <value>

# Get config value
$ pnpm config get <key>

# List all config settings
$ pnpm config list
```

### Importing Projects
```bash
# Import from npm or Yarn
$ pnpm import
```

## Yarn

### Installation & Setup
```bash
# Install Yarn using npm
$ npm install -g yarn

# Check version
$ yarn -v
```

### Managing Packages
```bash
# Install dependencies from package.json
$ yarn
$ yarn install

# Install a package and add to dependencies
$ yarn add <package>

# Install a specific version
$ yarn add <package>@<version>

# Install as dev dependency
$ yarn add <package> --dev
$ yarn add <package> -D

# Install globally
$ yarn global add <package>

# Uninstall a package
$ yarn remove <package>

# Update packages
$ yarn upgrade
$ yarn upgrade <package>
$ yarn upgrade <package>@<version>

# Upgrade interactive mode (Yarn 2+)
$ yarn upgrade-interactive
```

### Package Scripts
```bash
# Run a script defined in package.json
$ yarn <script>
$ yarn run <script>

# Common built-in scripts
$ yarn start
$ yarn test
```

### Package Management
```bash
# Initialize a new project
$ yarn init
$ yarn init -y  # Skip questions with defaults

# List installed packages
$ yarn list
$ yarn list --depth=0  # Show only top-level packages

# Show outdated packages
$ yarn outdated

# Show package info
$ yarn info <package>
```

### Dependencies
```bash
# Install production dependencies only
$ yarn --production
$ yarn install --production

# Force resolving dependencies
$ yarn install --force
```

### Workspaces (monorepo)
```bash
# Run a command in a specific workspace
$ yarn workspace <workspace_name> <command>

# Run a command in all workspaces
$ yarn workspaces run <command>
```

### Cache
```bash
# Clean cache
$ yarn cache clean

# List cached packages
$ yarn cache list
```

### Publishing
```bash
# Publish a package
$ yarn publish

# Create a new version
$ yarn version
```

### Configuration
```bash
# Set config values
$ yarn config set <key> <value>

# Get config value
$ yarn config get <key>

# Delete config value
$ yarn config delete <key>

# List all config
$ yarn config list
```

### Yarn 2+ (Berry) Specific Commands
```bash
# Switch to Yarn 2+
$ yarn set version berry

# Create a package from the workspace (Yarn 2+)
$ yarn pack

# Check for errors and suggestions
$ yarn dlx @yarnpkg/doctor

# Get detailed diagnostics
$ yarn explain peer-requirements

# Plugin management
$ yarn plugin import <plugin>
$ yarn plugin list
```

## Bun

### Installation & Setup
```bash
# Install Bun (macOS, Linux, WSL)
$ curl -fsSL https://bun.sh/install | bash

# Check version
$ bun -v
```

### Managing Packages
```bash
# Install dependencies from package.json
$ bun install
$ bun i

# Install a package and add to dependencies
$ bun add <package>
$ bun a <package>

# Install a specific version
$ bun add <package>@<version>

# Install as dev dependency
$ bun add <package> --dev
$ bun add <package> -d

# Install globally
$ bun add -g <package>
$ bun add --global <package>

# Uninstall a package
$ bun remove <package>
$ bun rm <package>

# Update packages
$ bun update
$ bun update <package>
```

### Running Scripts
```bash
# Run a script defined in package.json
$ bun run <script>

# Common built-in scripts
$ bun start
$ bun test

# Run a JavaScript/TypeScript file directly
$ bun run file.js
$ bun file.js
```

### Project Management
```bash
# Initialize a new project
$ bun init

# Create a new project from a template
$ bun create <template> [dir]

# List available templates
$ bun create

# Create from GitHub repo
$ bun create github-user/repo-name [dir]
```

### Workspaces
```bash
# Run a command in a workspace
$ bun run --cwd <dir> <command>
```

### Package Management
```bash
# List installed packages
$ bun pm ls

# Install native dependencies
$ bun pm cache c++
```

### Testing
```bash
# Run tests
$ bun test
$ bun test <file>
$ bun test --watch  # Watch mode

# Test coverage
$ bun test --coverage
```

### Bundling
```bash
# Build a production bundle
$ bun build ./index.ts --outdir ./out

# Bundle as a single file
$ bun build ./index.ts --outfile ./dist/bundle.js
```

### Development Server
```bash
# Start development server
$ bun --hot ./server.ts
```

## Common Operations Comparison

| Operation | npm | pnpm | Yarn | Bun |
|-----------|-----|------|------|-----|
| Install dependencies | `npm install` | `pnpm install` | `yarn` | `bun install` |
| Add a package | `npm i <pkg>` | `pnpm add <pkg>` | `yarn add <pkg>` | `bun add <pkg>` |
| Add dev dependency | `npm i -D <pkg>` | `pnpm add -D <pkg>` | `yarn add -D <pkg>` | `bun add -d <pkg>` |
| Remove a package | `npm uninstall <pkg>` | `pnpm remove <pkg>` | `yarn remove <pkg>` | `bun remove <pkg>` |
| Update packages | `npm update` | `pnpm update` | `yarn upgrade` | `bun update` |
| Run script | `npm run <script>` | `pnpm run <script>` | `yarn run <script>` | `bun run <script>` |
| Global install | `npm i -g <pkg>` | `pnpm add -g <pkg>` | `yarn global add <pkg>` | `bun add -g <pkg>` |
| List packages | `npm ls` | `pnpm ls` | `yarn list` | `bun pm ls` |
| Clean cache | `npm cache clean --force` | `pnpm store prune` | `yarn cache clean` | N/A |
| Init project | `npm init` | `pnpm init` | `yarn init` | `bun init` |
| Audit for security | `npm audit` | `pnpm audit` | `yarn audit` | N/A |
| Lock file | `package-lock.json` | `pnpm-lock.yaml` | `yarn.lock` | `bun.lockb` |
| Workspaces | `-w <workspace>` | `--filter <workspace>` | `workspace <workspace>` | `--cwd <workspace>` |
