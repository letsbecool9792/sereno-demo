# What the relayer does

To spend from your sereno account you sign a payment with your SSH key. Something still has to send that signature to the chain and pay the gas. That is the relayer's whole job.

## What it does

- It takes your signed payment, from `npx sereno-ak send`, the Spend page, or a payment commit pushed to GitHub.
- If your account hasn't been deployed yet, it deploys it first.
- It submits the payment to your account contract and pays the gas.
- It keeps the **relayer fee** written in the text you signed, 0.02 USDC on the hosted relayer, in the same token.

## What it can't do

The signed text fixes the chain, the account, the nonce, the amount, the recipient and the fee. The contract rebuilds that text and checks your signature against it, so if the relayer changed any of them, the signature would no longer match and the payment would fail. The relayer can only submit your payment as it is, or refuse to.

It can't spend twice either: each payment carries the account's nonce, which goes up by one when it is used.

## You don't need ours

The account's `execute` function is open to anyone. You can run your own relayer from the open-source code, or call `execute` yourself from any wallet with your signed payment and pay the gas directly. If the hosted relayer is down or refuses you, your money is still yours to move.
