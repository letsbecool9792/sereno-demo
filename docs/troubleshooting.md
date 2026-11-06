# Troubleshooting

## `ssh-keygen` is too old (no `-O hashalg`)

**Symptom:** the CLI prints `retrying without -O hashalg=sha256`, or `ssh-keygen` rejects the `-O hashalg=sha256` option.

**Cause:** OpenSSH older than 8.9, such as Windows 10's built-in 8.1 or Ubuntu 20.04.

**Fix:** the payment still works without it: it is signed with SHA-512 and costs more gas. To sign with SHA-256 (and to claim a `sereno.eth` name, which needs it), install OpenSSH 8.9 or newer. On Windows you can point the CLI at Git for Windows' copy:

```powershell
$env:AK_SSH_KEYGEN = "C:\Program Files\Git\usr\bin\ssh-keygen.exe"
```

## The key isn't synced on-chain yet

**Symptom:** the relayer refuses with `KeyNotOnProfile`, or the pay page lists your key as *not synced yet*.

**Cause:** the contract checks keys against the on-chain key oracle, not GitHub directly. A key added on GitHub after the last sync isn't there yet. It also happens if the key is on a different GitHub account than the one you pass with `--as`.

**Fix:** run `npx sereno-ak sync <you>`, or press **Sync my keys from GitHub** on the Spend page, and wait for `done … ok`. If the sync stays `queued`, the sync worker is offline; try again later. A newly synced key can send at most 50 USDC per payment for 72 hours.

## The payment commit was made in GitHub's web editor

**Symptom:** a commit whose message is a payment intent never pays; the relayer refuses it.

**Cause:** commits made in GitHub's web editor are signed by GitHub's own key, not yours. The contract only accepts signatures from keys on your profile, so it rejects them.

**Fix:** make the commit locally with your own key, then push it:

```sh
npx sereno-ak commit-pay 1 <friend> --as <you> --push
```

or, with the `intent.txt` from the Spend page, `git commit -S --allow-empty --cleanup=verbatim -F intent.txt` and `git push`.
