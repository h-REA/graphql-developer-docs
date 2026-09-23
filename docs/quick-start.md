# Quick Start

A step-by-step guide to integrating **hREA `happ-0.5.0-beta.1`** into your scaffolded Holochain application.

!!! warning "Version compatibility"

    `happ-0.5.0-beta.1` runs on **Holochain 0.7.x** and needs `@holochain/client` **^0.21.0**. The client and the conductor move together: 0.20 speaks to a 0.6 conductor, 0.21 to a 0.7 one, and mixing them does not fail with a message that tells you so.

    Older releases target older lines: `happ-0.4.0-beta` on Holochain 0.6, `happ-0.3.x-beta` on 0.5. This guide is for 0.5.0-beta.

## Prerequisites

This guide assumes you are starting a new Holochain application from scratch using the official scaffolding tool.

### 1. Install the Holochain development environment

Follow the official installation guide, most easily through Nix flakes:

**[Installing the Holochain development environment](https://developer.holochain.org/get-started/#2-installing-holochain-development-environment)**

That gives you the Nix package manager, the `holochain` and `hc` command line tools, and the rest of the toolchain.

### 2. Scaffold a Holochain web app

Create the application with the scaffolding tool from the **0.7 holonix line**. This matters: at the time of writing, the official get-started guide still pins `main-0.6`, and a 0.6 app cannot load this hREA release. hREA's own `flake.nix` tracks `holonix?ref=main-0.7`, so use the same:

```bash
cd ~/your-projects-directory
nix run "github:holochain/holonix?ref=main-0.7#hc-scaffold" -- web-app
```

During the interactive process you will be asked for:

- **UI framework**: your preference. The examples in this guide are framework agnostic.
- **App name**: for example `my-hrea-app`.
- **Holonix environment**: yes, for reproducibility.
- **Package manager**: your preference.
- **Initial DNA**: yes.
- **DNA name**: for example `my_dna`.

!!! note "Check what you scaffolded"

    hREA 0.5.0-beta only composes into a Holochain 0.7 hApp. After scaffolding, confirm the generated `flake.nix` and `Cargo.toml` target 0.7 (`hdk 0.7`, `hdi 0.8`) before adding hREA. A 0.6 app will not load the DNA.

## Next steps

With a scaffolded application in place, continue to the **[Integration Guide](integration-guide.md)**, which adds the hREA DNA to your hApp and wires the GraphQL client.

If you only want to consume a published release without reading the integration path end to end, **[Consuming a release](consuming-a-release.md)** covers the two artifacts and the version pinning contract.
