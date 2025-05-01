## Script Execution

Each package manager provides ways to define and run scripts in your package.json file. Here's how to effectively use scripts across different package managers:

### Script Definition in package.json

```json
{
  "name": "my-package",
  "scripts": {
    "start": "node index.js",
    "build": "webpack",
    "test": "jest",
    "lint": "eslint .",
    "custom": "echo 'Custom script'"
  }
}
```

### npm Script Execution

```bash
# Run a defined script
$ npm run start
$ npm run build

# Shorthand for common scripts
$ npm start   # shorthand for npm run start
$ npm test    # shorthand for npm run test

# Pass additional arguments
$ npm run test -- --watch

# Run multiple scripts sequentially
$ npm run clean && npm run build

# Run multiple scripts in parallel
$ npm run lint & npm run test

# Run pre/post scripts automatically
# If you define "prebuild" or "postbuild", they run automatically
$ npm run build  # Will run prebuild, build, postbuild in order

# List available scripts
$ npm run

# Run script with environment variable
$ NODE_ENV=production npm run build

# Run script with npx-installed tools
$ npm run build --workspace=package-name

# Show script verbosity
$ npm run build --loglevel=verbose
```

### pnpm Script Execution

```bash
# Run a defined script
$ pnpm run start
$ pnpm start  # shorthand

# Run with arguments
$ pnpm test -- --watch

# Run in specific directory
$ pnpm --dir=packages/app run build

# Run in workspace
$ pnpm --filter=package-name run build

# Run in all packages
$ pnpm -r run test

# Run in packages with specific changes
$ pnpm -r --filter="[origin/main]" run test

# Run script with specific node version
$ pnpm run --use-node-version=16.14.0 build

# Environment variables
$ NODE_ENV=production pnpm run build
```

### Yarn Script Execution

```bash
# Run a defined script
$ yarn run start
$ yarn start  # shorthand

# Pass additional arguments
$ yarn test --watch

# Run in a workspace
$ yarn workspace package-name run build

# Run in all workspaces
$ yarn workspaces run test

# View script source before running
$ yarn run --inspect test

# Environment variables
$ NODE_ENV=production yarn build
```

### Bun Script Execution

```bash
# Run a defined script
$ bun run start
$ bun start  # shorthand

# Pass additional arguments
$ bun test -- --watch

# Run with environment variables
$ NODE_ENV=production bun run build

# Run with watch mode (restart on file changes)
$ bun --watch run dev

# Run with hot reload
$ bun --hot run dev
```

### Custom Script Features

#### npm
```bash
# Access npm variables in scripts
{
  "scripts": {
    "info": "echo Package name: $npm_package_name"
  }
}

# CLI environment variables are accessible in scripts
$ NAME=value npm run custom  # process.env.NAME will be "value"

# Script hooks
{
  "scripts": {
    "prebuild": "echo Pre-build tasks",
    "build": "webpack",
    "postbuild": "echo Post-build tasks"
  }
}
```

#### pnpm
```bash
# Use --if-present to run a script only if it exists
$ pnpm run --if-present lint

# Shell automation - pnpm exec within scripts
{
  "scripts": {
    "lint": "pnpm exec eslint ."
  }
}

# Access pnpm variables
{
  "scripts": {
    "info": "echo Package name: $npm_package_name"
  }
}
```

#### Yarn
```bash
# Use conditional execution
$ yarn run lint || echo "Lint failed but continuing"

# Access yarn variables in scripts
{
  "scripts": {
    "info": "echo Package name: $npm_package_name"
  }
}

# Use yarn bin within scripts
{
  "scripts": {
    "lint": "$(yarn bin eslint) ."
  }
}
```

#### Bun
```bash
# Access package variables in scripts
{
  "scripts": {
    "info": "echo Package name: $npm_package_name"
  }
}

# Bun script task runner specifics
{
  "scripts": {
    "build": "bun build ./src/index.ts --outdir ./dist"
  }
}
```

## Node Version Management

Package managers provide various ways to manage and enforce Node.js versions for your projects.

### Using .nvmrc / .node-version Files

```bash
# .nvmrc or .node-version file content example
16.14.0
```

### npm with Node Version
```bash
# Check if installed Node version satisfies engines requirement
$ npm config set engine-strict true

# Define Node.js version in package.json
{
  "engines": {
    "node": ">=16.14.0",
    "npm": ">=8.0.0"
  }
}

# Run with a specific Node version (using nvm)
$ nvm use && npm run build
```

### pnpm with Node Version
```bash
# Install and use specified Node.js version
$ pnpm env use --global 16.14.0

# Use a specific version for current directory
$ pnpm env use 16.14.0

# Run script with specific Node version
$ pnpm --use-node-version=16.14.0 run build

# Auto-install Node version from .nvmrc or package.json engines
$ pnpm env auto
```

### Yarn with Node Version
```bash
# Define Node.js version in package.json
{
  "engines": {
    "node": ">=16.14.0"
  }
}

# Yarn 2+ can be configured to use specific Node.js version
# In .yarnrc.yml:
nodeLinker: node-modules
yarnPath: .yarn/releases/yarn-3.2.1.cjs
```

### Bun with Node Version
```bash
# Define Node.js version in package.json
{
  "engines": {
    "node": ">=16.14.0",
    "bun": ">=1.0.0"
  }
}

# Run with node compatibility mode
$ bun --node-compat run start
```# JavaScript Package Manager Cheatsheet

A comprehensive reference guide for npm, pnpm, Yarn, and Bun CLI commands.

- [npm](#npm)
- [pnpm](#pnpm)
- [Yarn](#yarn)
- [Bun](#bun)
- [Environment Variables](#environment-variables)
- [Lock Files](#lock-files)
- [Dependencies Management](#dependencies-management)
- [Offline Mode](#offline-mode)
- [CI/CD Best Practices](#cicd-best-practices)
- [Common Operations Comparison](#common-operations-comparison)
- [Migrating Between Package Managers](#migrating-between-package-managers)
- [Performance Comparison](#performance-comparison)
- [Registry Configuration](#registry-configuration)

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

## Environment Variables

### npm
```bash
# Enable verbose logging
$ NODE_DEBUG=npm npm <command>

# Set npm registry
$ NPM_CONFIG_REGISTRY=https://registry.npmjs.org/

# Set log level
$ NPM_CONFIG_LOGLEVEL=verbose|silent|error|warn|info|http|silly

# Skip installation of optional dependencies
$ NPM_CONFIG_OPTIONAL=false

# Force npm to run scripts
$ NPM_CONFIG_IGNORE_SCRIPTS=false

# Offline mode
$ NPM_CONFIG_OFFLINE=true
```

### pnpm
```bash
# Set pnpm home directory
$ PNPM_HOME=/path/to/pnpm/home

# Skip installation of peer dependencies
$ PNPM_CONFIG_STRICT_PEER_DEPENDENCIES=false

# Set registry
$ PNPM_CONFIG_REGISTRY=https://registry.npmjs.org/

# Enable debug logs
$ PNPM_DEBUG=1
```

### Yarn
```bash
# Skip using the cache
$ YARN_CACHE_FOLDER=/dev/null

# Set registry
$ YARN_REGISTRY=https://registry.npmjs.org/

# Use offline mode
$ YARN_OFFLINE=true

# Enable verbose logging
$ YARN_VERBOSE=true
```

### Bun
```bash
# Set Bun registry
$ BUN_CONFIG_REGISTRY=https://registry.npmjs.org/

# Set log level
$ BUN_CONFIG_LOGLEVEL=debug|info|error|warn

# Skip installing devDependencies
$ BUN_CONFIG_DEVELOPMENT=false
```

## Lock Files

### Understanding Lock Files
Each package manager uses its own lock file format to ensure consistent installations across different environments:

- **npm**: `package-lock.json` (JSON format)
- **pnpm**: `pnpm-lock.yaml` (YAML format)
- **Yarn**: `yarn.lock` (Custom format)
- **Bun**: `bun.lockb` (Binary format)

### Managing Lock Files
```bash
# npm - Generate a package lock without installing
$ npm install --package-lock-only

# npm - Update lock file based on package.json without installing
$ npm update --package-lock-only

# pnpm - Generate lockfile without installing
$ pnpm install --lockfile-only

# yarn - Generate a yarn.lock without installing
$ yarn install --mode update-lockfile

# bun - Generate only the lockfile
$ bun install --dry-run
```

### Lock File Best Practices
- Always commit lock files to version control
- Do not manually edit lock files
- Use `--frozen-lockfile` (or equivalent) in CI environments
- Update lock files regularly to keep dependencies secure

## Dependencies Management

### Types of Dependencies
- **dependencies**: Required packages for production
- **devDependencies**: Packages needed for development only
- **peerDependencies**: Compatible packages that the consumer should install
- **optionalDependencies**: Optional packages that won't fail installation if missing
- **bundledDependencies/bundleDependencies**: Packages that will be bundled with your package

### Managing Different Types of Dependencies

#### npm
```bash
# dependencies
$ npm install <pkg> --save
$ npm install <pkg> -S

# devDependencies
$ npm install <pkg> --save-dev
$ npm install <pkg> -D

# peerDependencies (must be manually added to package.json)
# optionalDependencies
$ npm install <pkg> --save-optional
$ npm install <pkg> -O

# List all dependencies
$ npm ls --all

# List direct dependencies
$ npm ls --depth=0
```

#### pnpm
```bash
# dependencies
$ pnpm add <pkg>

# devDependencies
$ pnpm add -D <pkg>

# peerDependencies
$ pnpm add -P <pkg>

# optionalDependencies
$ pnpm add -O <pkg>

# List dependencies with filter
$ pnpm list --depth infinity --prod|dev|optional|peer
```

#### Yarn
```bash
# dependencies
$ yarn add <pkg>

# devDependencies
$ yarn add <pkg> --dev

# peerDependencies (must be manually added to package.json)

# optionalDependencies
$ yarn add <pkg> --optional

# List dependencies by type
$ yarn list --pattern "pattern"
```

#### Bun
```bash
# dependencies
$ bun add <pkg>

# devDependencies
$ bun add <pkg> --dev
$ bun add <pkg> -d

# peerDependencies (must be manually added to package.json)

# optionalDependencies
$ bun add <pkg> --optional

# List all dependencies
$ bun pm ls
```

### Overriding Dependencies

#### npm
```bash
# Override a dependency (npm 8+)
# Add to package.json:
"overrides": {
  "dependency-name": "version"
}

# Resolve dependency conflicts during installation
$ npm install --force
```

#### pnpm
```bash
# Override a dependency
# Add to package.json:
"pnpm": {
  "overrides": {
    "dependency-name": "version"
  }
}

# Or use the command:
$ pnpm add dependency-name@npm:real-dependency-name@version
```

#### Yarn
```bash
# Yarn 1:
# Add to package.json:
"resolutions": {
  "dependency-name": "version"
}

# Yarn 2+:
# Add to package.json:
"packageExtensions": {
  "dependency-name@*": {
    "dependencies": {
      "other-dependency": "^1.0.0"
    }
  }
}
```

#### Bun
```bash
# Add to package.json:
"overrides": {
  "dependency-name": "version"
}
```

## Offline Mode

### npm
```bash
# Install packages in offline mode
$ npm install --offline

# Download packages without installing
$ npm fetch <pkg>

# Make a cache copy of online registry
$ npm ci --cache .npm-cache
```

### pnpm
```bash
# Install in offline mode
$ pnpm install --offline

# Store all packages for offline use
$ pnpm fetch

# Configure offline mode
$ pnpm config set prefer-offline true
```

### Yarn
```bash
# Install in offline mode
$ yarn install --offline

# Cache all packages for future offline use
$ yarn cache clean && yarn install

# Configure offline preference
$ yarn config set prefer-offline true
```

### Bun
```bash
# Install in offline mode
$ bun install --offline

# Configure offline mode
$ bun config set offline true
```

## CI/CD Best Practices

### npm
```bash
# Clean install for CI environments
$ npm ci

# Skip running scripts
$ npm ci --ignore-scripts

# Don't save to package.json
$ npm ci --no-save
```

### pnpm
```bash
# Clean install for CI
$ pnpm install --frozen-lockfile

# Skip post-install scripts
$ pnpm install --ignore-scripts

# Use strict mode for CI
$ pnpm install --strict-peer-dependencies
```

### Yarn
```bash
# Yarn 1 - CI install
$ yarn install --frozen-lockfile

# Yarn 2+ - CI install
$ yarn install --immutable

# Skip post-install scripts
$ yarn install --ignore-scripts
```

### Bun
```bash
# CI install
$ bun install --frozen-lockfile

# Skip post-install scripts
$ bun install --no-scripts
```

## Registry Configuration

### npm
```bash
# Set default registry
$ npm config set registry https://registry.npmjs.org/

# Set scoped registry
$ npm config set @scope:registry https://registry.example.com/

# Use a specific registry for a single command
$ npm install --registry=https://registry.example.com/

# Login to registry
$ npm login

# Publish to registry
$ npm publish
```

### pnpm
```bash
# Set default registry
$ pnpm config set registry https://registry.npmjs.org/

# Set scoped registry
$ pnpm config set @scope:registry https://registry.example.com/

# Use a registry for a single command
$ pnpm add pkg --registry https://registry.example.com/

# Login to registry
$ pnpm login

# Publish package
$ pnpm publish
```

### Yarn
```bash
# Set default registry
$ yarn config set registry https://registry.npmjs.org/

# Set scoped registry
# Add to .yarnrc.yml:
# npmScopes:
#   scope:
#     npmRegistryServer: "https://registry.example.com/"

# Use registry for a single command
$ yarn add pkg --registry https://registry.example.com/

# Login to registry
$ yarn login

# Publish package
$ yarn publish
```

### Bun
```bash
# Set default registry
$ bun config set registry https://registry.npmjs.org/

# Use registry for a single command
$ bun add pkg --registry https://registry.example.com/

# Login to registry
$ bun login

# Publish package
$ bun publish
```

## Migrating Between Package Managers

### npm to pnpm
```bash
# Install pnpm
$ npm install -g pnpm

# Generate pnpm-lock.yaml from package-lock.json
$ pnpm import

# Install dependencies
$ pnpm install
```

### npm to Yarn
```bash
# Install Yarn
$ npm install -g yarn

# Import from package-lock.json
$ yarn import

# Install dependencies
$ yarn
```

### npm to Bun
```bash
# Install Bun
$ curl -fsSL https://bun.sh/install | bash

# Install dependencies
$ bun install
# Bun will automatically read package-lock.json
```

### pnpm to npm
```bash
# Remove pnpm lock and modules
$ rm pnpm-lock.yaml
$ rm -rf node_modules

# Install with npm
$ npm install
```

### Yarn to npm
```bash
# Remove Yarn lock and modules
$ rm yarn.lock
$ rm -rf node_modules

# Install with npm
$ npm install
```

### Migration Best Practices
- Run tests after migration to ensure everything works
- Check for platform-specific dependencies
- Review scripts in package.json for compatibility
- Consider using corepack for managing multiple package managers

## Performance Comparison

### Installation Performance
Performance metrics from fastest to slowest (generally):

1. **Bun**: Fastest overall due to its Zig-based implementation
2. **pnpm**: Fast due to its unique disk-linking approach
3. **Yarn**: Medium speed with efficient caching
4. **npm**: Slowest of the four

### Cold Install Recommendations
- Use `bun install` for maximum speed
- Use `pnpm install --frozen-lockfile` for reliability with speed
- Use `yarn install --immutable` for Yarn 2+ projects
- Use `npm ci` for npm projects

### Disk Space Usage
From most efficient to least:

1. **pnpm**: Most efficient due to content-addressable store
2. **Bun**: Efficient binary approach
3. **Yarn**: Moderate with deduplication
4. **npm**: Least efficient with nested dependencies

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
| CI install | `npm ci` | `pnpm i --frozen-lockfile` | `yarn --frozen-lockfile` | `bun i --frozen-lockfile` |
| Offline mode | `npm i --offline` | `pnpm i --offline` | `yarn --offline` | `bun i --offline` |

## Package Executors and Binaries

Package managers provide utilities to execute binaries from packages without explicitly installing them. These tools are essential for running one-off commands, testing packages, or executing scripts from node_modules.

### npx (npm executor)

`npx` is included with npm and allows you to execute binary packages without installing them globally.

```bash
# Basic usage - run a package binary
$ npx cowsay "Hello World"

# Run a specific version of a package
$ npx cowsay@2.0.0 "Hello World"

# Execute a GitHub gist
$ npx https://gist.github.com/username/gistid

# Execute a GitHub repository
$ npx github:username/repo

# Bypass local cache, always fetch the latest
$ npx --no-cache cowsay "Hello World"

# Don't install package if not found locally
$ npx --no-install cowsay "Hello World"

# Force clean installation before running
$ npx --ignore-existing cowsay "Hello World"

# Specify the package manager to use
$ npx --package-manager=yarn cowsay "Hello World"

# Run with Node.js flags
$ npx --node-arg=--max-old-space-size=4096 large-memory-app

# Run with arguments containing spaces
$ npx cowsay -- "Message with spaces"

# Run a locally available binary from node_modules/.bin
$ npx eslint .

# Specify registry
$ npx --registry=https://registry.example.com cowsay "Hello"

# Run in quiet mode (suppress output)
$ npx -q cowsay "Hello World"

# Debug mode
$ npx --loglevel=debug cowsay "Hello World"
```

**Use Cases for npx:**
- Running one-off commands without permanent installation
- Creating new projects with scaffolding tools (`npx create-react-app my-app`)
- Running a specific version of a tool for testing
- Executing GitHub repositories or gists directly
- Running local project binaries without path references

### pnpm dlx & pnpm exec

pnpm provides `pnpm dlx` (similar to npx) and `pnpm exec` for executing packages:

```bash
# pnpm dlx - Run a package without installing
$ pnpm dlx cowsay "Hello World"

# Run a specific version
$ pnpm dlx cowsay@2.0.0 "Hello World"

# Run from a different registry
$ pnpm dlx --registry=https://registry.example.com cowsay "Hello"

# Run with environment variables
$ pnpm dlx -E VARIABLE=value cowsay "Hello World"

# Use a specific Node.js version (if using pnpm's built-in node version manager)
$ pnpm dlx -n 16.14.0 cowsay "Hello World"

# pnpm exec - Execute a locally installed binary
$ pnpm exec eslint .

# Short form of exec
$ pnpm exec -- eslint .

# Run with arguments containing spaces
$ pnpm exec -- "echo Hello World"

# Run locally installed binary from specific directory
$ pnpm --dir=./packages/app exec eslint .

# Run in the context of a workspace
$ pnpm --filter=@scope/package exec eslint .
```

**Difference between `pnpm dlx` and `pnpm exec`:**
- `pnpm dlx` is for executing packages that aren't installed locally (downloads temporarily)
- `pnpm exec` runs binaries that are already installed in the project

### Yarn dlx & yarn exec

Yarn provides `yarn dlx` (in Yarn 2+/Berry) and `yarn exec` for executing binaries:

#### Yarn 1.x
```bash
# Yarn 1.x doesn't have dlx, use global add + run + remove
$ yarn global add cowsay && cowsay "Hello" && yarn global remove cowsay

# Execute locally installed binary
$ yarn exec cowsay "Hello World"

# Execute with specific arguments
$ yarn exec eslint -- --fix .
```

#### Yarn 2+ (Berry)
```bash
# Run a package without installing
$ yarn dlx cowsay "Hello World"

# Run a specific version
$ yarn dlx cowsay@2.0.0 "Hello World"

# Run with environment variables
$ yarn dlx --env VAR=value cowsay "Hello World"

# Run with specific package manager
$ yarn dlx --pm=npm cowsay "Hello World"

# Execute locally installed binary
$ yarn exec cowsay "Hello World"

# Run in a specific workspace
$ yarn workspace @scope/package exec cowsay "Hello"
```

**Yarn 2+ Advanced Features:**
```bash
# Execute with custom Node.js options
$ yarn exec --node-options="--max-old-space-size=4096" large-memory-app

# Run with binaries from specific sub-dependencies
$ yarn exec "eslint:eslint" -- --fix .

# Run with specific environment
$ yarn exec --cwd packages/tools cowsay "Hello"
```

### Bun x & Bun run

Bun provides `bun x` (similar to npx) and `bun run` for executing packages:

```bash
# Execute a package without installing
$ bun x cowsay "Hello World"

# Run a specific version
$ bun x cowsay@2.0.0 "Hello World"

# Execute from GitHub
$ bun x github:username/repo

# Run a local binary
$ bun run eslint .

# Run a locally installed binary (alternative)
$ bun eslint .

# Execute binary with arguments
$ bun run eslint -- --fix .

# Run with specific Node.js compatibility flags
$ bun --node-compat run app.js

# Run script in package.json
$ bun run start

# Run with watch mode (restart on file changes)
$ bun --watch run app.js

# Run with hot module reloading
$ bun --hot run app.js
```

**Bun execution features:**
- Significantly faster execution than other package managers
- Built-in watch mode for development
- Node.js compatibility flags for better ecosystem support
- Direct HTTP imports support
- TypeScript and JSX execution without transpilation

### Global Binaries Management

#### npm
```bash
# Install global binary
$ npm install -g cowsay

# List global binaries
$ npm list -g --depth=0

# Binary location
$ which cowsay
# typically in: /usr/local/bin or ~/.npm-global/bin

# Update global binary
$ npm update -g cowsay

# Remove global binary
$ npm uninstall -g cowsay
```

#### pnpm
```bash
# Install global binary
$ pnpm add -g cowsay

# List global binaries
$ pnpm list -g --depth=0

# Binary location
$ which cowsay
# typically in: ~/.pnpm-global/bin

# Update global binary
$ pnpm update -g cowsay

# Remove global binary
$ pnpm remove -g cowsay
```

#### Yarn
```bash
# Install global binary
$ yarn global add cowsay

# List global binaries
$ yarn global list

# Binary location
$ which cowsay
# typically in: ~/.config/yarn/global/node_modules/.bin

# Update global binary
$ yarn global upgrade cowsay

# Remove global binary
$ yarn global remove cowsay
```

#### Bun
```bash
# Install global binary
$ bun add -g cowsay

# List global binaries
$ bun pm ls -g

# Binary location
$ which cowsay
# typically in: ~/.bun/bin

# Update global binary
$ bun update -g cowsay

# Remove global binary
$ bun remove -g cowsay
```

### Local Binary Execution

Each package manager provides ways to run locally installed binaries:

#### npm
```bash
# Run local binary directly
$ ./node_modules/.bin/eslint .

# Using npm exec (npm 7+)
$ npm exec -- eslint .

# Using npx to run local binaries
$ npx eslint .

# Using npm run for scripts with binaries
$ npm run lint  # if "lint": "eslint ." is in package.json
```

#### pnpm
```bash
# Run local binary directly
$ ./node_modules/.bin/eslint .

# Using pnpm exec
$ pnpm exec eslint .

# Shorthand for exec
$ pnpm eslint .

# Using pnpm run for scripts with binaries
$ pnpm run lint  # if "lint": "eslint ." is in package.json
```

#### Yarn
```bash
# Run local binary directly
$ ./node_modules/.bin/eslint .

# Using yarn exec
$ yarn exec eslint .

# Using yarn bin
$ $(yarn bin eslint) .

# Using yarn run for scripts with binaries
$ yarn run lint  # if "lint": "eslint ." is in package.json

# In Yarn 2+, you can run it directly
$ yarn eslint .
```

#### Bun
```bash
# Run local binary directly
$ ./node_modules/.bin/eslint .

# Using Bun run for direct binary execution
$ bun run eslint .

# Shorthand for run
$ bun eslint .

# Using Bun run for scripts with binaries
$ bun run lint  # if "lint": "eslint ." is in package.json
```

### Package Runner Security Considerations

When using package executors, consider these security practices:

1. **Validate packages before execution**: Check the source and reputation of packages
2. **Pin versions**: Use specific versions to prevent supply chain attacks
3. **Use official packages**: Prefer packages from trusted maintainers
4. **Inspect scripts**: Review what scripts do, especially for lesser-known packages
5. **Use `--no-script` flags**: Skip running lifecycle scripts when uncertain

```bash
# Example of pinning exact versions for security
$ npx cowsay@2.0.0 "Hello World"
$ pnpm dlx cowsay@2.0.0 "Hello World"
$ yarn dlx cowsay@2.0.0 "Hello World"
$ bun x cowsay@2.0.0 "Hello World"

# Running without executing lifecycle scripts
$ npx --ignore-scripts cowsay "Hello World"
$ pnpm dlx --ignore-scripts cowsay "Hello World"
$ yarn dlx --ignore-scripts cowsay "Hello World" 
$ bun x --no-scripts cowsay "Hello World"
```

## Package Publishing

### npm
```bash
# Publish a package
$ npm publish

# Publish as public package
$ npm publish --access public

# Publish to a specific registry
$ npm publish --registry https://registry.example.com/

# Create a new version
$ npm version patch|minor|major|prerelease

# Publish a pre-release version
$ npm publish --tag beta
```

### pnpm
```bash
# Publish a package
$ pnpm publish

# Publish as public package
$ pnpm publish --access public

# Publish to a specific registry
$ pnpm publish --registry https://registry.example.com/

# Create a new version
$ pnpm version patch|minor|major|prerelease

# Dry run to check what will be published
$ pnpm publish --dry-run
```

### Yarn
```bash
# Publish a package
$ yarn publish

# Publish as public package
$ yarn publish --access public

# Publish to a specific registry
$ yarn publish --registry https://registry.example.com/

# Create a new version during publish
$ yarn publish --new-version <version>

# Publish a pre-release version
$ yarn publish --tag beta
```

### Bun
```bash
# Publish a package
$ bun publish

# Publish as public package
$ bun publish --access public

# Publish to a specific registry
$ bun publish --registry https://registry.example.com/

# Create a new version
$ bun version patch|minor|major|prerelease
```

## Peer Dependencies Management

### npm
```bash
# npm 7+ automatically installs peer dependencies
# Skip auto-installation of peer dependencies
$ npm install --legacy-peer-deps

# Check peer dependency issues
$ npm ls --all
```

### pnpm
```bash
# Configure peer dependency behavior
$ pnpm config set auto-install-peers true

# Strict peer dependencies mode
$ pnpm install --strict-peer-dependencies

# Allow peer dependency resolution to modify other dependencies
$ pnpm install --resolve-peers-from-workspace-root
```

### Yarn
```bash
# Yarn 1: Doesn't install peer dependencies automatically
# Check peer dependency issues
$ yarn check

# Yarn 2+: Check peer dependency issues
$ yarn info

# Configure Yarn 2+ peer dependency mode in .yarnrc.yml
# pnpMode: loose|strict
```

### Bun
```bash
# Bun automatically installs peer dependencies
# Skip auto-installation of peer dependencies
$ bun install --no-peer
```
