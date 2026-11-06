# How to verify a payment commit by hand

A commit in this repo whose message is a sereno payment is a payment. You don't have to trust the relayer or the pay page to know it happened; two public checks are enough.

## 1. The commit is signed by the payer

1. Open the commit on GitHub.
2. Look for the **Verified** badge next to it. Click it: GitHub shows which SSH key signed the commit and that the key is on the author's profile.
3. Read the commit message. It should be exactly the payment text: `sereno v1`, then `chain`, `account`, `github-id`, `nonce`, `send`, `to` and `relayer-fee`. Nothing before it, nothing after it.

No badge doesn't always mean a bad payment: the badge needs the key added on GitHub as a **Signing Key** and a verified commit email. The contract only needs the key on the profile. But a commit made in GitHub's web editor is signed by GitHub's own key, not the author's, and the contract rejects it.

## 2. The transaction matches the text

1. Take the `account:` address from the message and open it on [Base Sepolia's explorer](https://sepolia.basescan.org) (or Arbitrum Sepolia's, if `chain:` is 421614).
2. Find the transaction that emitted an `Executed` event with the same `nonce` as the message.
3. Check that the event and its USDC transfers match the text:
   - the `to` address received the `send` amount;
   - the relayer received at most the `relayer-fee`;
   - `viaCommit` is `true`, meaning the signature was over the commit itself.

If both checks pass, the person whose key is on that GitHub profile signed this exact payment, and the chain paid exactly what it says.
