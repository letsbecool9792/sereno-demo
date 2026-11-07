# FAQ

## Do I need a wallet?

Not to receive or to spend. Every GitHub user already has a sereno account, at an address worked out from their numeric GitHub ID, and anyone can pay it by username. You spend from it by signing with the SSH key already on your GitHub profile, using `ssh-keygen` or `git commit -S`. You only need a browser wallet to send money from outside sereno, for example to pay someone from your own USDC on the pay page or to fund an issue bounty.

## What happens if I rename my GitHub account?

Your money stays put. The account is tied to your numeric GitHub ID, which never changes, not to your username. After the rename, your new username points to the same account. If someone else later takes your old username, sereno refuses to pay that name for 15 days and says the name changed owner, so nobody's payment goes to the wrong person by accident.

## Who pays the gas?

When you spend, a relayer submits your signed payment and pays the gas. In return it keeps the relayer fee written in the text you signed, 0.02 USDC on the hosted relayer. When you pay someone from your own wallet on the pay page, your wallet pays the gas for that transaction, as usual.

## What if I lose my SSH key?

Add a new key to your GitHub profile, then run `npx sereno-ak sync <you>` so it is copied on-chain. Remove the lost key from GitHub too; at the next sync it stops being able to spend. A new key can spend at most 50 USDC per payment for its first 72 hours, so a stolen GitHub account can't empty yours in one go.

## Is it on mainnet?

No. sereno runs on testnets only: payments on Base Sepolia and Arbitrum Sepolia with Circle's test USDC, and the `sereno.eth` names on Ethereum Sepolia. Get test USDC from [faucet.circle.com](https://faucet.circle.com).
