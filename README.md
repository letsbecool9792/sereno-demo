# sereno-demo

A live demo repo for [Sereno](https://github.com/letsbecool9792/sereno), which pays GitHub users through the SSH keys already on their profiles.

Each commit here whose message is a Sereno payment intent is a **payment**:

1. `ak commit-pay <amount> <github-user> --as <you> --key <your ssh key> --repo . --push` signs an empty commit. Its message is the exact payment text, signed with `git commit -S` and your SSH key.
2. Pushing it to this repo is the broadcast. A relayer watching the repo picks the commit up through GitHub's API and submits it. The contract checks the SSH signature on-chain and pays.
3. GitHub shows the commit as **Verified**, because it's signed with a key on your profile.

The commits are on Base Sepolia (testnet). The repo holds no code, only payment commits.
