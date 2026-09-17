# Integration Guide

Now that you have a scaffolded Holochain 0.7 app, you can compose hREA into it.

## Step 1: check your DNA structure

Your hApp needs at least one DNA with a zome before it will compile. If you chose an initial DNA during scaffolding you already have one.

```bash
ls dnas/                     # at least one DNA directory, e.g. my_dna/
ls dnas/my_dna/zomes/        # integrity/ and coordinator/
```

Build it once before adding hREA, so that a later failure is unambiguous:

```bash
npm run build:happ           # or bun / pnpm / yarn
ls dnas/my_dna/workdir/      # my_dna.dna
```

## Step 2: choose your artifact

`happ-0.5.0-beta.1` publishes two files, and they are not interchangeable:

| File | Use it when |
|------|-------------|
| `hrea.dna` | you are composing hREA into your own hApp alongside your own DNAs. This is the case this guide covers. |
| `hrea.happ` | you want to run hREA on its own, as a separate installed app. |

Full detail, including how the two differ at runtime, is in **[Consuming a release](consuming-a-release.md)**.

## Step 3: add the hREA role

Add hREA as a second role in your hApp manifest.

```yaml title="workdir/happ.yaml"
manifest_version: "1"
name: your_app_name
roles:
  - name: your_main_dna
    dna:
      bundled: ../dnas/your_dna/workdir/your_dna.dna
  - name: hrea
    dna:
      bundled: ./hrea.dna
```

The role name `hrea` is what you pass to the GraphQL adapter later. If you name it something else, pass that instead.

## Step 4: download the DNA

Fetch the prebuilt DNA into `workdir/`. Automating it in `package.json` keeps the version pinned in one place:

```json title="package.json"
{
  "scripts": {
    "postinstall": "npm run download-hrea",
    "download-hrea": "[ ! -f \"workdir/hrea.dna\" ] && curl -L --output workdir/hrea.dna https://github.com/h-REA/hREA/releases/download/happ-0.5.0-beta.1/hrea.dna; exit 0"
  }
}
```

Then install, which triggers the download:

```bash
npm install
```

!!! tip "Pin the tag, not `latest`"

    The URL above names `happ-0.5.0-beta.1` explicitly. Pointing at a moving target means a conductor upgrade can arrive without you choosing it, and the 0.6 to 0.7 transition is exactly the kind that breaks a build.

## Step 5: add the UI dependencies

In your UI package (for example `ui/package.json`):

```json
{
  "dependencies": {
    "@apollo/client": "^3.7.0",
    "@holochain/client": "^0.21.0",
    "@valueflows/vf-graphql-holochain": "^0.700.0-rc.0",
    "graphql": "^16.6.0"
  }
}
```

- `@holochain/client` connects to the conductor. **0.21 is required** for a Holochain 0.7 conductor.
- `@valueflows/vf-graphql-holochain` builds the GraphQL schema bound to the running hREA cell. Its version line tracks the Holochain line: `0.700.x` pairs with 0.7, `0.600.x` with 0.6.
- `@apollo/client` is one GraphQL client among several. The adapter produces a schema; the client is your choice.

!!! warning "If npm still shows `0.600.0-rc.0` as latest"

    The 0.7 adapter may not be published yet. Check with `npm view @valueflows/vf-graphql-holochain versions`. If no `0.700.x` appears, build it from source in the meantime:

    ```bash
    git clone https://github.com/h-REA/hREA.git
    cd hREA && nix develop
    yarn install && yarn run build:graphql:adapter
    # then depend on the built package by path, e.g.
    # "@valueflows/vf-graphql-holochain": "file:../hREA/modules/vf-graphql-holochain/build"
    ```

Install them:

```bash
cd ui && npm install
```

## Next steps

**[Basic Usage](basic-usage-lit.md)** wires the client and issues a first query and mutation.
