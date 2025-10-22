# Code-Server Custom

A customized [code-server](https://github.com/coder/code-server) Docker image with pre-installed development tools and CLI utilities for cloud development and AI integration.

## Overview

This Docker image extends the [LinuxServer code-server](https://github.com/linuxserver/docker-code-server) base image (VS Code running in your browser) with additional tools commonly needed for modern cloud-native development, Python development, and AI workflows.

## What's Included

This image comes pre-configured with:

### Core Tools
- **code-server 4.105.1** - VS Code in your browser
- **Node.js 24** - Latest Node.js LTS runtime and npm
- **Python 3** - Python runtime with pip and venv support
- **Git** - Version control
- **Zsh** - Modern shell with powerline fonts

### AI & Development Tools
- **Gemini CLI** (`@google/generative-ai-cli`) - Google's Generative AI CLI tool
- **uv** - Fast Python package installer and resolver

### Cloud Platform CLIs
- **AWS CLI v2** - Amazon Web Services command-line interface
- **Google Cloud SDK (gcloud)** - Google Cloud Platform CLI
- **kubectl** - Kubernetes command-line tool

### Additional Utilities
- curl, wget - Download utilities
- ca-certificates, gnupg - Security and certificate management
- fonts-powerline - Enhanced terminal fonts

## Quick Start

### Using Docker Run

```bash
docker run -d \
  --name=code-server \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -e PASSWORD=yourpassword \
  -p 8443:8443 \
  -v /path/to/your/code:/config/workspace \
  --restart unless-stopped \
  ghcr.io/[your-username]/code-server-custom:latest
```

### Using Docker Compose

```yaml
version: "3.8"
services:
  code-server:
    image: ghcr.io/[your-username]/code-server-custom:latest
    container_name: code-server
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Etc/UTC
      - PASSWORD=yourpassword
      # - SUDO_PASSWORD=yoursudopassword  # Optional
    volumes:
      - /path/to/your/code:/config/workspace
      - /path/to/config:/config
    ports:
      - 8443:8443
    restart: unless-stopped
```

## Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `PUID` | User ID for the abc user | `1000` |
| `PGID` | Group ID for the abc user | `1000` |
| `TZ` | Timezone for the container | `Etc/UTC` |
| `PASSWORD` | Password for code-server web interface | - |
| `SUDO_PASSWORD` | Optional sudo password for the abc user | - |

### Volumes

| Path | Description |
|------|-------------|
| `/config/workspace` | Your code/project files |
| `/config` | code-server configuration and extensions |

### Ports

| Port | Description |
|------|-------------|
| `8443` | code-server web interface |

## Usage Examples

### Accessing code-server

After starting the container, access code-server at:
```
https://localhost:8443
```

### Using Cloud CLIs

Once inside the code-server terminal:

```bash
# AWS CLI
aws configure
aws s3 ls

# Google Cloud
gcloud auth login
gcloud projects list

# Kubernetes
kubectl get nodes
kubectl get pods
```

### Using AI Tools

```bash
# Google Gemini CLI
gemini --help
```

### Python Development

```bash
# Create virtual environment
python3 -m venv .venv
source .venv/bin/activate

# Or use uv for faster package management
uv pip install requests
```

### Node.js Development

```bash
# Check Node.js version
node --version  # Should be v24.x

# Install packages
npm install
npm run dev
```

## Building Locally

```bash
# Clone the repository
git clone https://github.com/[your-username]/code-server-custom.git
cd code-server-custom

# Build the image
docker build -t code-server-custom:local .

# Run your local build
docker run -d \
  --name=code-server \
  -e PASSWORD=yourpassword \
  -p 8443:8443 \
  -v $(pwd):/config/workspace \
  code-server-custom:local
```

## Automated Updates

This project uses:
- **Renovate** - Automated dependency updates for the base image and packages
- **Release Please** - Automated versioning and changelog generation
- **GitHub Actions** - Automated Docker image builds and publishing

The image is automatically built and published to GitHub Container Registry when new releases are created.

## Security

- The container runs as the `abc` user (non-root) for improved security
- All CLI tools are installed system-wide but accessible to the `abc` user
- Regular dependency updates via Renovate keep packages current and secure
- Vulnerability alerts are enabled for immediate notification of security issues

## Use Cases

This image is ideal for:
- ☁️ Cloud-native development with multi-cloud CLI access
- 🤖 AI/ML projects requiring CLI access to AI services
- 🐍 Python development with modern tooling
- 🟢 Node.js application development
- ☸️ Kubernetes cluster management
- 🌐 Remote development accessible from any browser
- 📚 Teaching and learning environments
- 🔒 Secure development environments without local setup

## Credits

Built on top of:
- [code-server](https://github.com/coder/code-server) by Coder
- [LinuxServer code-server](https://github.com/linuxserver/docker-code-server) by LinuxServer.io

## License

This project follows the same license as the base code-server image.

## Support

For issues, questions, or contributions, please open an issue on the GitHub repository.

