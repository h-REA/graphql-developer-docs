---
description: >-
  These are instructions for doing set up, and running, of a holochain runtime
  on your device containing the hREA hApp, for the sake of a development
  environment.
---

# Running hREA Backend



Download [hrea\_suite.happ](https://drive.google.com/file/d/1h-Mg\_seAWP8P55S4JVzW9ssu2HhXHQ-W/view?usp=sharing) (todo: point this to official releases)

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



Set up a holochain development "sandbox". A temporary directory on your filesystem that will store all your keys and data for the hREA happ that you are about to install and run. `network quic` is there to instruct `holochain` to use a specific kind of networking, known as `quic`.

```
hc sandbox create -n 1 -d hrea_tester network quic
```



Install the hREA hApp to your holochain sandbox. Make sure you use the right path to wherever on your filesystem you have `hrea_suite.happ` file that you downloaded.

```
hc sandbox call install-app-bundle ./hrea_suite.happ
```



Start your holochain "sandbox" runtime, attaching a port for websocket networking, on the networking port 4000. You can safely stop and restart this particular process, and don't have to rerun the other steps.

```
hc sandbox run --all --ports 4000
```



