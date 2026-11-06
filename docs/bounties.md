# How issue bounties work

Anyone can put USDC on a GitHub issue. When a merged pull request closes the issue, its author is paid, with no one having to approve the payout.

## 1. Fund

On the pay page's **Issue bounties** tab, paste the issue link, enter an amount and a refund deadline, and confirm in your wallet (approve, then fund). The USDC goes into the BountyBoard contract, in a pot for that repo, issue and token. Several people can add to the same pot.

Fund before the PR is merged: once an issue is settled, nobody can add to it.

## 2. Settle

1. Someone opens a pull request whose description says `Fixes #<issue number>`.
2. A maintainer merges it, and GitHub closes the issue.
3. A Chainlink CRE workflow asks GitHub what closed the issue. It reports a winner only if the issue's latest close came from a **merged PR in the same repo**, and the winner is that PR's author, by numeric GitHub ID.
4. The BountyBoard records the winner, once per issue.

The relayer watches funded issues and starts this by itself within about a minute of the close. You can also press **Check GitHub and pay the PR author**, or run `npx sereno-ak bounty <issue link> --settle`.

Closing the issue by hand pays nobody.

## 3. Payout

Once settled, anyone can trigger the payout. The pot goes to the winner's sereno account, the address worked out from their GitHub ID. The author doesn't need a wallet, or even to have heard of sereno; they spend it later with their SSH key.

## Refunds

If nobody earns the bounty, each funder can take back their own contribution after their deadline, as long as the issue hasn't been settled.
