# The payment intent, line by line

A sereno payment is a short piece of plain text. You sign it with your SSH key (`ssh-keygen -Y sign -n sereno@v1`, or `git commit -S` with the text as the whole commit message), and the contract rebuilds the same text and checks your signature against it. Here is an example for Base Sepolia:

```
sereno v1
chain: 84532
account: 0xa22f7e55c2ef953d16607636c9ba48d60e78e402
github-id: 99113360
nonce: 3
send: 1500000 of 0x036cbd53842c5426634e7929541ec2318f3dcf7e
to: 0xfa3b979b706fb90ee20458166a68995e389540dd
relayer-fee: 20000
```

| Line | What it says |
|---|---|
| `sereno v1` | The header: this is a sereno payment, format version 1, so the text can't be mistaken for anything else you sign. |
| `chain: 84532` | The chain ID the payment is valid on (84532 is Base Sepolia), so it can't be replayed on another chain. |
| `account: 0x...` | The sereno account the money leaves from, in lowercase hex. |
| `github-id: 99113360` | The numeric GitHub ID that owns that account. Your key has to be on this ID's profile. |
| `nonce: 3` | The account's payment counter. Each payment uses the next number, so a signature can only be spent once. |
| `send: 1500000 of 0x036c...` | The amount in the token's base units, and which token. USDC has 6 decimals, so 1500000 is 1.5 USDC. |
| `to: 0xfa3b...` | The address that receives the money. |
| `relayer-fee: 20000` | What the relayer that submits it may keep, in the same token: 20000 is 0.02 USDC. |

Every line ends with a newline, including the last, and there is no other whitespace. Because the contract can return this exact text (`intent(token, to, amount, fee, nonce)`), any client can show you what you are about to sign instead of rebuilding it.
