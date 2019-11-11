# 51% Attack Workshop

This workshop is based on [Kulupu](https://github.com/kulupu/kulupu), a proof-of-work blockchain built on
[Substrate](https://github.com/paritytech/substrate).

## Prerequisites

Clone this repo and update the submodules:

```bash
git clone https://github.com/kulupu/kulupu
cd kulupu
git submodule update --init --recursive
```

Install Rust:

```bash
curl https://sh.rustup.rs -sSf | sh
```

Install required tools:

```bash
./scripts/init.sh
```

## Run

If you can run these commands successfully, you're ready for the workshop.

### Full Node

```bash
cargo run --release
```

### Mining
This portion is optional for workshop participation. If you want to actively attack or defend the chain you will need to follow these instructions. If you just want to use the network and experience the effects, you may skip this section.


Install `subkey`:

```bash
cargo install --force --git https://github.com/paritytech/substrate subkey
```
TODO Can we save recompile, by using the subkey that's already in `vendor`?

Generate an account to use as the target for mining:

```bash
subkey --sr25519 --network=16 generate
```

Remember the public key, and pass it to node for mining. For example:

```
cargo run --release -- --validator --author 0x7e946b7dd192307b4538d664ead95474062ac3738e04b5f3084998b76bc5122d
```

## Join a Network

Participants start their nodes and connect to the specified bootnodes

## Use the Network
Add your adresses to polkadot UI.

Make a few transfers to see what the chain can do

## Start mining
Generate your own address to use for mining. Restart your node as a miner.

Notice the difficulty adjusts as more users start mining

If you didn't build `subkey` but still want to mine, here are the pubkeys for the dev accounts.

| Name    | SR25519 Public Key |
| ------- | ------------------ |
| Alice   | 0xd43593c715fdd31c61141abd04a99fd6822c8558854ccde39a5684e7a56da27d |
| Bob     | 0x8eaf04151687736326c9fea17e25fc5287613693c912909cb226aa4794f26a48 |
| Charlie | 0x90b5ab205c6974c9ea841be688864633dc9ca8a357843eeacf2314649965fe22 |
| Dave    | 0x306721211d5404bd9da88e0204360a1a9ab8b87c66c1bc2fcdd37f3c2222cc20 |
| Eve     | 0xe659a7a1628cdd93febc04a4e0646ea20e9f5f0ce097d9a05290d4a9e054df4e |
| Ferdie  | 0x1cbd2d43530a44705ad088af313e18f80b53ef16b36177cd4b77b846f2a5f07c |

## Uncontroversial Upgrade
Start compile, then discuss what's happening

It seems a malicious user can set any user's balance arbitrarily. This is definitely not the monetary policy we agreed on or thought we had when the network was launched. The bug is in the buggy-balances module.

Let's fix it.
* Fix the actual bug
* Build the new runtime
* Plan the hardfork
* Build the new node.

## Test the fix
Check that normal token transfers still work as expected. Can you send and receive tokens?

Check that the arbitrary setting of balances no longer works.

## Execute this Scenario
The following headlines emerge
* Bug fixed, dev token grows in popularity
* Bad guys capture child, request ransom
* Good guys pay ransom, child returned safely
  * This is the only part of the scenario that happened on chain
* Bad guys still not caught.
* Governments urge developers to freeze Bad guys' funds
* Bad guys: "There's two sides. We're actually the good guys"

## Controversial Hardfork
The government manages to convince many miners to freeze the funds. They plan a hard fork just as we did before.
