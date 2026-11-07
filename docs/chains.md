# Chains and addresses

sereno runs on testnets only.

| | Base Sepolia | Arbitrum Sepolia |
|---|---|---|
| Role | main demo chain | second chain |
| Chain ID | `84532` | `421614` |
| Circle USDC | `0x036CbD53842c5426634e7929541eC2318f3dCF7e` | `0x75faf114eafb1BDbe2F0316DF893fd58CE46AA4d` |
| Explorer | [sepolia.basescan.org](https://sepolia.basescan.org) | [sepolia.arbiscan.io](https://sepolia.arbiscan.io) |

Test USDC comes from [faucet.circle.com](https://faucet.circle.com).

## One address on both chains

A GitHub user's sereno account address is the **same on both chains**. It is worked out from their numeric GitHub ID by the account factory, and the factory and the other contracts are deployed at the same addresses on every chain. So `npx sereno-ak account <user>` gives one address, and you can send to it on either chain.

The two balances are separate, though: USDC sent on Base Sepolia stays on Base Sepolia. The `chain:` line of a signed payment says which chain it spends on.

The `sereno.eth` names live on Ethereum Sepolia, where ENSv2 is deployed, and resolve to that same address for both chains.
