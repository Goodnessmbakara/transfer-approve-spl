# Practice Exercise

Copy the scripts (Approve & Transfer) and create a new repo with them to run and test how they work.
Observe:
- Gas estimation
- Balance changes
- tx hash resolution from Neon RPC
  
You don’t need to write your own script to submit the task—but playing with the code is highly recommended!

Once done, push your scripts to GitHub and submit the repo link including a README with your observations about how approval and transfer work with Solana Native SDK.

## Keep in mind that spending from Solana ATA balance requires initializing the balance account:

To be able to spend the token balance held on a Solana SPL associated token account (ATA) via the corresponding ERC20ForSPL smart contract deployed on NeonEVM, the native Solana user who owns that ATA must have done the following:

To have successfully registered the native Solana account that owns the ATA, i.e. to have scheduled at least one NeonEVM transaction from the native Solana account that owns the ATA in order to have a NeonEVM account attributed to that native Solana account
To have delegated (on Solana) the ATA token balance to the external authority (Solana account) associated to the attributed NeonEVM account (the address of this external authority Solana account can be obtained by calling the getUserExtAuthority function, passing the attributed NeonEVM account address).
Once those two steps have been completed, the Solana user's ATA token balance will be included in the balance returned by the balanceOf function and this ATA token balance will be spendable via the transfer and transferFrom functions.
