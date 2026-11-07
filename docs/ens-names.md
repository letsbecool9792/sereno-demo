# `<user>.sereno.eth` names

## Everyone already has one

Every GitHub user has a name under `sereno.eth` without doing anything: `octocat.sereno.eth`, `torvalds.sereno.eth`, and so on. The parent name `sereno.eth` lives on Ethereum Sepolia (ENSv2), and a wildcard resolver answers for every name under it. When you look one up, a gateway turns the username into the numeric GitHub ID, and the ID into the user's sereno account address. The answer is signed by the gateway, and the resolver checks that signature (ENS's CCIP-read).

The address is the same for Base Sepolia and Arbitrum Sepolia, so one name works for both. Stock wallets only resolve mainnet names, so the sereno pay page and CLI resolve these themselves.

## What claiming changes

`npx sereno-ak claim --as <you>` turns your name into a **real ENSv2 subname** in the `sereno.eth` registry:

- **It's owned by your account**, not by sereno.
- **It has its own resolver**, set up with your account's address for Ethereum, Base and Arbitrum, so it resolves on-chain and lookups no longer depend on our gateway.
- **Only you can claim it.** The registrar checks an SSH signature from a key on your GitHub profile and the key oracle's username-to-ID map, so nobody can claim someone else's username.

Claims are verified on Ethereum Sepolia, where the ed25519 verifier doesn't fit the gas limit, so they need a P-256 key (`ssh-keygen -t ecdsa`) or a security key (`-t ecdsa-sk`).

## Renames

A claimed name doesn't follow a GitHub rename by itself. If you rename, or someone else gets the username, the old claim becomes stale, anyone can release it, and the name is quarantined for 15 days, during which it resolves to nobody.
