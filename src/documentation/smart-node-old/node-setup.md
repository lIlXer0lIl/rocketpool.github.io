# Node Setup, Registration & Management

<br>

## Initializing Your Node Wallet


With the Rocket Pool service running, the first thing you'll need to do is initialize your node wallet::

```
rocketpool wallet init
```

This will prompt you to enter a node password, and will then save it to disk.
You won't need to enter your node password again, it will simply be used by the smart node to unlock your wallet.

Next, a HD wallet will be generated to store your node account and all validator keys for your minipools.
You will be shown a mnemonic phrase to recover your wallet in case of hardware failure, and prompted to record it and enter it to confirm it is correct.
You can make sure your wallet was created successfully with:

```
rocketpool wallet status
```

Your node password is stored at `~/.rocketpool/data/password`, while your wallet is stored at `~/.rocketpool/data/wallet`.
You can export the contents of both of these files and display them on screen with:

```
rocketpool wallet export
```

Feel free to back these up in a safe and secure storage area which can't be accessed by anyone else.
You do not need to back your wallet up repeatedly, even after creating new minipools.



<br>

## Recovering Your Node Wallet

If you lose your node wallet, you can recover it with::

```
rocketpool wallet recover
```

This will prompt you to enter the recovery mnemonic phrase for your wallet.
If successful, the wallet will be restored along with your node account and all validator keys for created minipools.



<br>

## Seeding Your Node Account

Next, you'll need to load your node account up with ETH and RPL to deposit into Rocket Pool. Find your node address with::

```
rocketpool node status
```

If you're participating in a testnet beta, you can obtain GoETH from one of the following faucets:

* [ethstaker discord](https://discord.gg/GGGmqZdCBf)
* [faucet.goerli.mudit.blog](https://faucet.goerli.mudit.blog/)

Once you have some GoETH, you can also request RPL from a faucet directly from the CLI:

```
rocketpool faucet withdraw-rpl
```

Note that this requires a 0.5 GoETH fee to prevent abuse.

After requesting your GoETH and RPL, check your node status again to ensure your balances have increased.
Note that the RPL you received will be referred to as "old RPL", which can be swapped for the new RPL token.


<br>

## Registering Your Node


Once you have some ETH, register with:

```
rocketpool node register
```

You will be prompted to either detect your timezone location automatically, or enter it manually.
This information is not used for KYC purposes, but is sent to Rocket Pool during registration in order to display accurate node information to users.
You may abstain by manually entering a location such as `Hidden/Hidden`.

Once you've registered successfully, you can check your status with:

```
rocketpool node status
```

This should now display additional information like: `The node is registered with Rocket Pool with a timezone location of Australia/Brisbane`.



<br>

## Updating Your Registration


If you want to set a withdrawal address which all node rewards & refunds will be sent to, run:

```
rocketpool node set-withdrawal-address [address]
```

If you want to update the timezone your node is registered in, run::

```
rocketpool node set-timezone
```

This will repeat the prompts run during registration, and update your node's information in the network.


<br>

## Sending From Your Node Account


If you want to send ETH or tokens from your node account to another Ethereum address at any time, use:

```
rocketpool node send [amount] [token] [to-address]
```

This will send the specified amount of ETH from the node account to the specified address.