# The 72-hour new-key rule

## The rule

A key that was first seen on your GitHub profile less than **72 hours** ago can send at most **50 USDC per payment**. Smaller payments go through at once. A bigger one is refused with `NewKeyCoolingDown`, which says when the key will be old enough. After 72 hours the key can send any amount.

The clock starts when the key oracle first records the key on-chain, that is, at the first sync after you add it on GitHub. Keys that were already on your profile keep their original date at every later sync.

## Why

Your sereno account is controlled by the keys on your GitHub profile. That means the weak point is your GitHub account itself: if someone takes it over, they can add their own SSH key, sync it, and try to spend.

The rule turns that from "empty the account in one payment" into "at most 50 USDC per payment, during a window in which you can notice". In those 72 hours you can recover your GitHub account, remove the attacker's key, and sync, after which the key can't spend anything at all.

The cost to normal use is small: a brand-new key can still pay everyday amounts right away, and keys you have had for a while are not affected.
