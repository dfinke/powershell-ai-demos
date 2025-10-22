# Use Debian as the base image (lightweight Unix container)
FROM mcr.microsoft.com/vscode/devcontainers/base:debian

# Install prerequisites
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    wget \
    apt-transport-https \
    software-properties-common \
    ca-certificates \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Download and install PowerShell 7.x
RUN wget -q https://packages.microsoft.com/config/debian/12/packages-microsoft-prod.deb \
    && dpkg -i packages-microsoft-prod.deb \
    && rm packages-microsoft-prod.deb \
    && apt-get update \
    && apt-get install -y powershell \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Set pwsh as the default shell for the vscode user
RUN usermod -s /usr/bin/pwsh vscode 2>/dev/null || true

# Install PowerShell modules as the vscode user
USER vscode

RUN pwsh -NoLogo -NoProfile -Command " \
    Set-PSRepository -Name PSGallery -InstallationPolicy Trusted; \
    Install-Module -Name PSAI -Scope CurrentUser -Force -AllowClobber; \
    Install-Module -Name PSAISuite -Scope CurrentUser -Force -AllowClobber; \
    Install-Module -Name ImportExcel -Scope CurrentUser -Force -AllowClobber; \
    Write-Host 'PowerShell modules installed successfully'; \
    Get-Module -ListAvailable PSAI, PSAISuite, ImportExcel"

# Switch back to root for any remaining setup
USER root

# Configure PowerShell profile to display a welcome message
RUN mkdir -p /home/vscode/.config/powershell && \
    echo 'Write-Host \"PowerShell AI Demos Environment\" -ForegroundColor Green' > /home/vscode/.config/powershell/Microsoft.PowerShell_profile.ps1 && \
    echo 'Write-Host \"Modules installed: PSAI, PSAISuite, ImportExcel\" -ForegroundColor Cyan' >> /home/vscode/.config/powershell/Microsoft.PowerShell_profile.ps1 && \
    chown -R vscode:vscode /home/vscode/.config

# Set the default shell to pwsh
ENV SHELL=/usr/bin/pwsh

# Switch to the vscode user for the runtime
USER vscode
