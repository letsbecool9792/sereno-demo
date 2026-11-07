# The 72-Hour New-Key Rule

When you add a new SSH key to your GitHub profile and sync it with Sereno, the system imposes a temporary restriction: for the first 72 hours, any payment signed by this key is limited to a maximum of 50 USDC.

## Why does this exist?

This rule is a security safeguard designed to protect your funds in the event of a GitHub account compromise. 

If an attacker gains unauthorized access to your GitHub account, they might attempt to add their own SSH key to your profile to authorize transactions. By enforcing a 72-hour "cooldown" period with a low transaction limit, we provide a window of opportunity for you to:

1. **Detect the unauthorized access:** Notice suspicious activity or unauthorized key additions on your GitHub account.
2. **Revoke the key:** Remove the malicious key from your GitHub profile and run `npx sereno-ak sync <you>` to propagate the change on-chain.

## What it protects against

Without this rule, an attacker who gains control of your GitHub account could immediately drain your entire balance in a single transaction. The 72-hour rule ensures that even if an attacker successfully adds a key, they cannot perform a large-scale theft immediately, significantly limiting the potential damage and giving you time to secure your account.