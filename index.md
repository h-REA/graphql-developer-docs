---
description: >-
  This guide is intended as a way to help you discover and familiarize with the
  APIs, as opposed to integrating it into your project. For that check out the
  "Quick Start - Integrate" guide.
---

# Quick Start: hREA Integration

A step-by-step guide to integrating **hREA v0.3.3** into your scaffolded Holochain application.

> **⚠️ Version Compatibility Notice**:
> - **hREA v0.3.3** is compatible with **Holochain v0.5.x**
>
> This guide is specifically designed for **hREA version 0.3.3**. Different versions may require different integration steps.


## Prerequisites

This guide assumes you are starting a new Holochain application from scratch using the official scaffolding tool.

### 1. Install Holochain Development Environment

Follow the official Holochain installation guide to set up your development environment. This is most easily done using Nix Flakes.

**[Installing Holochain Development Environment](https://developer.holochain.org/get-started/#2-installing-holochain-development-environment)**

This process will install:
- The Nix package manager
- The `holochain` and `hc` command-line tools
- All other required dependencies for Holochain development

### 2. Create a Scaffolded Holochain Web App

Once your development environment is installed, create a new Holochain web application using the scaffolding tool. This will generate a project with a basic DNA and a starter UI.

```bash
# Navigate to your projects directory
cd ~/your-projects-directory

# Create a scaffolded Holochain web app
nix run "github:holochain/holochain?rev=0a9b89382186834273c3734e5659f7c009139265#hc-scaffold" web-app
```

**During the interactive scaffolding process, you will be asked for:**
- **UI Framework**: Choose your preferred frontend framework (the rest of this guide will use framework-agnostic examples that can be adapted to any UI).
- **App name**: Your preferred name (e.g., `my-hrea-app`).
- **Holonix environment**: **Yes** (recommended for reproducibility).
- **Package manager**: Your preference (npm, bun, pnpm, or yarn).
- **Initial DNA**: **Yes**.
- **DNA name**: Your preferred name (e.g., `my_dna`).

This will create a new directory with a complete project structure, ready for you to build on.

For more detailed scaffolding instructions, you can refer to the official documentation:
**[Holochain Forum App Tutorial - Scaffolding Steps](https://developer.holochain.org/get-started/3-forum-app-tutorial/)**

## Next Steps

Once you have scaffolded your new application, you are ready to begin integrating the hREA modules. The next section, the **[Integration Guide](integration-guide.md)**, will walk you through the process of adding the hREA DNA to your project and configuring it correctly.

