# Glossary

**SSH signing key**
: A key on your GitHub profile (Settings → SSH and GPG keys) that can sign data, not just log you in. In sereno, any key on your profile counts, authentication or signing, and it is what spends from your account.

**SSHSIG**
: OpenSSH's signature format, made by `ssh-keygen -Y sign` and by `git commit -S` with an SSH key. sereno's contract checks SSHSIG signatures on-chain (ed25519, P-256, RSA and security keys).

**Intent**
: The plain-text payment you sign: chain, account, GitHub ID, nonce, amount and token, recipient, and relayer fee, one per line. The contract rebuilds the same text, so you always sign something readable, never blind calldata.

**Relayer**
: A service that takes your signed intent and submits it on-chain, paying the gas and keeping the fee written in the intent. It can't change the payment; anyone can run one, or submit themselves.

**Key oracle**
: The on-chain list of each GitHub user's SSH keys (as hashes), kept up to date by a Chainlink CRE workflow that reads GitHub. It also remembers when each key was first seen, for the 72-hour rule.

**CREATE2 account**
: Each GitHub user's smart account, at an address computed from their numeric GitHub ID with CREATE2. The address is known before the account exists, is the same on every chain, and survives a username change.

**ENS name**
: `<user>.sereno.eth`, a name that resolves to a GitHub user's sereno account. Every user has one automatically; claiming it makes it a real ENSv2 subname owned by their account.
