```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install curl and basic tools
sudo apt install -y curl build-essential

# Install Node.js 24 (recommended) via NodeSource
curl -fsSL https://deb.nodesource.com/setup_24.x | sudo -E bash -
sudo apt install -y nodejs

# Verify
node -v   # should show v24.x
npm -v

# Update system
sudo apt update && sudo apt upgrade -y

# Install curl and basic tools
sudo apt install -y curl build-essential

# Install Node.js 24 (recommended) via NodeSource
curl -fsSL https://deb.nodesource.com/setup_24.x | sudo -E bash -
sudo apt install -y nodejs

# Verify
node -v   # should show v24.x
npm -v

```
```bash

npm install --global rea-agents

```
```bash

rea setup
# or (if not installed globally)
npx rea-agents@latest setup
```

```bash

rea --help
rea doctor          # full health check
rea doctor --json   # machine-readable report

```

```bash

export REA_ANALYSIS_PROVIDER=ghidra   # or hopper

# For Ghidra example:

export GHIDRA_INSTALL_DIR=/path/to/ghidra
export JAVA_HOME=/path/to/jdk-21
rea doctor --provider ghidra


# Overview of a binary
rea analyze /absolute/path/to/program --provider ghidra --json

# Search for a string or symbol
rea search /absolute/path/to/program "search_term" --provider ghidra --json

# Get details about a function (by name or address)
rea function /absolute/path/to/program main --provider ghidra --json
rea function /absolute/path/to/program 0x1000 --provider ghidra --json

# Decompile a function / address
rea decompile /absolute/path/to/program 0x1000 --provider ghidra --json

# Cross-references
rea xrefs /absolute/path/to/program 0x1000 --provider ghidra --json

# Trace a feature / string through the binary
rea trace /absolute/path/to/program "offline" --provider ghidra --json

# List available providers and what they support
rea providers --json
rea capabilities --json


```

```bash

rea inspect-go-binary /absolute/path/to/go-program --json

# Identity + deployment form
rea inspect-managed-artifact /absolute/path/Assembly.dll --json

# All members
rea inspect-managed-members /absolute/path/Assembly.dll --json

# Specific type
rea inspect-managed-members /absolute/path/Assembly.dll --type Example.Parser --json

```

```bash
# Save a big analysis result
rea analyze-javascript-application /path/to/app --json > app-evidence.json

# Create a small summary view of a large Evidence file
jq -c '{source: {kind: "inline", evidence: .}, view: {kind: "summary"}}' app-evidence.json > app-view.json
rea inspect-analysis-view app-view.json

# Compare two Evidence bundles
rea compare /path/to/left-evidence.json /path/to/right-evidence.json --json

# Import / export Evidence
rea evidence-import /path/to/evidence/bundle.json
rea evidence-export /path/to/evidence/bundle.json /path/to/canonical.json

```
```bash

# Analyze and save a snapshot at the same time
rea analyze /path/to/program --provider ghidra --snapshot /path/to/program-snapshot.json

# Later queries can reuse the snapshot automatically
rea analyze /path/to/program --provider ghidra --snapshot /path/to/program-snapshot.json
```

```bash
# Health / readiness check
rea doctor
rea doctor --provider ghidra --json
rea doctor --client cursor --json

# Import historical source for comparison
rea import-reference-source /absolute/path/to/old-source-tree

# Generic analyze (auto-selects JS workflow for directories/.asar)
rea analyze /path/to/app-or-binary

# Help
rea --help
rea analyze --help

```






```bash

# Make sure you have a recent Node.js
node -v   # should be 22.19+ or 24.11+ or 26+

# Create a clean folder
mkdir ~/rea-test && cd ~/rea-test

# Clone the official Electron quick-start (very small)
git clone https://github.com/electron/electron-quick-start.git
cd electron-quick-start

# Install dependencies
npm install

```

```bash

# Quick edit – add a simple IPC handler
cat >> main.js << 'EOF'

// Simple IPC example for REA to discover
const { ipcMain } = require('electron');
ipcMain.handle('notes:search', async (event, query) => {
  return `You searched for: ${query}`;
});
EOF

```


```bash

rea analyze-javascript-application "$(pwd)" --json

# From inside the electron-quick-start folder
npx -y rea-agents@latest analyze-javascript-application "$(pwd)" --json

```


```bash

google-chrome \
  --remote-debugging-port=9222 \
  --user-data-dir=/tmp/rea-browser-profile \
  https://example.com


rea list-browser-targets http://127.0.0.1:9222 --json

rea inspect-web-page http://127.0.0.1:9222 TARGET_ID \
  --observation-ms 5000 \
  --include-script-sources \
  --include-json-body-shapes \
  --json


rea analyze-web-bundle http://127.0.0.1:9222 TARGET_ID --json

rea observe-web-session http://127.0.0.1:9222 TARGET_ID \
  --observation-ms 10000 --json
  
```
