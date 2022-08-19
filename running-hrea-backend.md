---
description: >-
  These are instructions for doing set up, and running, of a holochain runtime
  on your device containing the hREA hApp, for the sake of a development
  environment.
---

# Running hREA Backend

Before trying to develop a user interface or service on top of hREA, you need to be running the hREA backend, within a holochain runtime.



Download the `hrea_suite.happ` file from [this hREA release](https://github.com/h-REA/hREA/releases/tag/happ-0.0.1-alpha.6).



You need to install some packages to your command line, which you can do manually, or via the nix-shell dev environment manager. There are instructions for either way that you choose right below this, just click to expand the section you would like to follow.

<details>

<summary>With Nix-shell</summary>

If you have nix-shell installed already, or install it now, you can follow these instructions in order to utilize the command line utilities that you need to proceed, such as `holochain` `hc` and `lair-keystore`.&#x20;

In your project folder, create a file called `default.nix`.&#x20;

Add these contents to that file:

```
let
  holonixRev = "c7a0b2c75480d429d570c94909cec3210280ad4c";

  holonixPath = builtins.fetchTarball "https://github.com/holochain/holonix/archive/${holonixRev}.tar.gz";
  holonix = import (holonixPath) {
    holochainVersionId = "v0_0_143";
  };
  nixpkgs = holonix.pkgs;
in nixpkgs.mkShell {
  inputsFrom = [ holonix.main ];
  packages = with nixpkgs; [
    # :TODO: binaryen, wasm-opt?
    # Additional packages go here
    nodejs-16_x
    nodePackages.pnpm
  ];
}
```

Then, just enter the nix-shell by executing the following command:

`nix-shell .`

Once you are inside that nix-shell, you can verify that you have `hc` on your path by typing `hc --version` and you should see the following printed to your console:

```
holochain_cli 0.0.41
```

You are ready to proceed.

</details>

<details>

<summary>Without Nix-shell</summary>

[Install Rust](https://www.rust-lang.org/tools/install), if you don't have it installed already.

Install the following to your system, via Rusts package manager "cargo".



The following installs a holochain developer tools binary to your system, accessible as the binary `hc` on your system.

```
cargo install holochain_cli --version 0.0.41
```



The following installs the core holochain runtime to your system, accessible as the binary `holochain` on your system. It can be used directly, or implicitly via the `hc sandbox` calls that we make next.

```
cargo install holochain --version 0.0.143
```



The following is the secure private key enclave that `holochain` uses for cryptography. It is available as a binary on your path `lair-keystore`, but `holochain` manages these subprocesses automatically on your behalf.

```bash
cargo install lair_keystore --version 0.0.10
```



</details>



Set up a holochain development "sandbox". A temporary directory on your file system that will store all your keys and data for the hREA happ that you are about to install and run. `network quic` is there to instruct `holochain` to use a specific kind of networking, known as `quic`.

```
hc sandbox create -n 1 -d hrea_tester network quic
```



Install the hREA hApp to your holochain sandbox. Make sure you use the right path to wherever on your filesystem you have `hrea_suite.happ` file that you downloaded.

```
hc sandbox call install-app-bundle ./hrea_suite.happ
```



Start your holochain "sandbox" runtime, attaching a port for websocket networking, on the networking port 4000.&#x20;

```
hc sandbox run --all --ports 4000
```

{% hint style="info" %}
You can safely stop and restart this particular process, and don't have to rerun the other steps. This is the process that you must have running in order to develop a user interface or service with an hREA backend.&#x20;
{% endhint %}

