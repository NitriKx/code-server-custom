# Code-Server Custom

A customized [code-server](https://github.com/coder/code-server) Docker image with pre-installed development tools and CLI utilities for cloud development and AI integration.

## Overview

This Docker image extends the [LinuxServer code-server](https://github.com/linuxserver/docker-code-server) base image (VS Code running in your browser) with additional tools commonly needed for modern cloud-native development, Python development, and AI workflows.

## NPM Setup for global packages

```
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> /config/.bashrc  # ← put this line in .bashrc
source ~/.bashrc  # if you only updated .bashrc
```

## Credits

Built on top of:
- [code-server](https://github.com/coder/code-server) by Coder
- [LinuxServer code-server](https://github.com/linuxserver/docker-code-server) by LinuxServer.io

## License

This project follows the same license as the base code-server image.
