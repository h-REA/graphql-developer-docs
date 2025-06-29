# Integration Guide

Now that you have a scaffolded Holochain app, you can integrate hREA.

### Step 1: Ensure Basic DNA Structure

**⚠️ Important**: Before integrating hREA, your hApp must have at least one basic DNA with a zome to compile properly. If you followed the scaffolding process and chose to create an initial DNA, you should already have this.

**Verify your DNA structure:**
```bash
# Check that you have a basic DNA structure in your app's root directory
ls dnas/
# Should show at least one DNA directory (e.g., my_dna/)

# Check that your DNA has at least one zome
ls dnas/my_dna/zomes/
# Should show integrity/ and coordinator/ directories with zomes
```

If you do not have this structure, you may need to run `hc scaffold dna` and `hc scaffold zome` from within the `nix develop` shell.

**Build and test your basic hApp first:**
It is a good idea to ensure your basic hApp compiles before adding hREA.
```bash
# From your project root, build the happ
npm run build:happ # Or bun run build:happ, etc.

# If successful, you'll see your DNA file created
ls dnas/my_dna/workdir/
# Should show my_dna.dna
```
Once you have a working basic hApp structure, you can proceed with hREA integration.

### Step 2: Add hREA DNA to Configuration

Navigate to your scaffolded app directory and add the hREA role to your hApp configuration.

**Edit `workdir/happ.yaml`:**
```yaml
manifest_version: "1"
name: your_app_name
roles:
  - name: your_main_dna    # Your existing DNA role
    dna:
      bundled: ../dnas/your_dna/workdir/your_dna.dna
    # ... other DNA configuration
  # Add the hREA role
  - name: hrea
    dna:
      bundled: ./hrea.dna
```

### Step 3: Download the hREA DNA

You need to download the pre-compiled hREA DNA and place it in your `workdir`. A simple way to automate this is to add a script to your `package.json`.

**Edit your root `package.json`:**
```json
{
  "scripts": {
    "postinstall": "npm run download-hrea",
    // other scripts...
    "download-hrea": "[ ! -f \"workdir/hrea.dna\" ] && curl -L --output workdir/hrea.dna https://github.com/h-REA/hREA/releases/download/happ-0.3.2-beta/hrea.dna; exit 0"
  }
}
```

Then run the installation command for your package manager, which will trigger the `postinstall` script.
```bash
npm install  # or your chosen package manager
```
This will download `hrea.dna` into your `workdir/` if it doesn't already exist.

### Step 4: Add UI Dependencies

To communicate with the hREA DNA from your user interface, you will need to add a few dependencies to your UI's `package.json`.

**Navigate to your UI directory (e.g., `cd ui`) and add these dependencies:**
```json
{
  "dependencies": {
    "@apollo/client": "^3.7.0",
    "@valueflows/vf-graphql-holochain": "^0.0.3-alpha.10",
    "graphql": "^16.6.0"
  }
}
```
*Note: The versions above are compatible with hREA v0.3.2. Check for the latest compatible versions if you are using a different release.*

**Key dependencies explained:**
- `@apollo/client`: A powerful GraphQL client that helps manage data fetching, caching, and state.
- `@valueflows/vf-graphql-holochain`: Provides the tools to create a GraphQL schema from the running hREA DNA.
- `graphql`: The core GraphQL library.

Install the dependencies:
```bash
cd ui
npm install  # or your chosen package manager
```

## Next Steps

With the backend configuration complete, you are now ready to set up the client-side integration and start interacting with hREA from your UI. The next section, **[Basic Usage with Lit](basic-usage-lit.md)**, provides a complete, framework-agnostic example of how to connect to Holochain and hREA. 