# DevContainer for PowerShell AI Demos

This devcontainer configuration provides a complete environment for working with PowerShell AI demos in GitHub Codespaces or VS Code with the Dev Containers extension.

## Features

- **Lightweight Unix Container**: Based on Debian Linux
- **PowerShell 7.x**: Latest PowerShell Core installed and configured
- **Default Shell**: `pwsh` is set as the default shell in the terminal
- **Pre-installed PowerShell Modules**:
  - `PSAI` - PowerShell AI module
  - `PSAISuite` - PowerShell AI Suite
  - `ImportExcel` - Excel import/export functionality
- **VS Code Extensions**: PowerShell extension pre-installed
- **Optimized Settings**: VS Code configured with PowerShell-specific settings

## Usage

### GitHub Codespaces

1. Navigate to the repository on GitHub
2. Click on "Code" → "Codespaces" → "Create codespace on main"
3. Wait for the container to build and start
4. The terminal will automatically use PowerShell 7

### VS Code with Dev Containers

1. Install the "Dev Containers" extension in VS Code
2. Open the repository folder in VS Code
3. Press `F1` and select "Dev Containers: Reopen in Container"
4. Wait for the container to build and start

## Verification

Once the container is running, you can verify the installation:

```powershell
# Check PowerShell version
$PSVersionTable

# List installed modules
Get-Module -ListAvailable PSAI, PSAISuite, ImportExcel

# Test a module
Import-Module PSAI
Get-Command -Module PSAI
```

## Customization

You can customize the environment by modifying:
- `.devcontainer/devcontainer.json` - VS Code settings and extensions
- `.devcontainer/Dockerfile` - Container configuration and installed software
