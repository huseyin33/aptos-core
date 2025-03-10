---
title: "Local Testnet, Devnet and Incentivized Testnet"
slug: "local-testnet-devnet-and-incentivized-testnet"
---

# Local Testnet, Devnet and Incentivized Testnet

You can connect to the Aptos Blockchain in a few ways. See the below table:

:::tip

Make sure to see the row describing **What not to do**.

:::

|Description |Aptos Devnet | Local Testnet | Aptos Incentivized Testnet (AIT)|
|---|---|---|---|
|**Network runs where**| Validators run on Aptos servers. FullNodes are run by both Aptos and you (i.e., the Aptos community).| Validators and FullNodes run locally on your computer, entirely independent from devnet. | Some Validators run on Aptos servers, others are run by the Aptos community. FullNodes are run by Aptos and the community.|
|**Who is responsible for the network**|Managed by Aptos Team. | Deployed, managed and upgraded by you.| Aptos Incentivized Testnet (AIT) is managed by Aptos and the community.|
|**Purpose of the network**|The devnet is built to experiment with new ideas, improve performance and enhance the user experience.| The local testnet is for your development purposes and runs on your local computer.| For executing the Aptos Incentivized Testnet programs for the community.|
|**Network status**|Mostly live, with brief interruptions during regular updates. | On your local computer. | **Live only during Incentivized Testnet drives**. |
|**Type of nodes** (also see the row **Network runs where**) |Validators and FullNodes. | Validators and FullNodes. | Validators and FullNodes.|
|**How to connect to the network**|<ul><li> You can transact directly with devnet without a local testnet. See, for example, [Your first transaction](/tutorials/first-transaction.md).</li><li> You can run FullNodes locally on your computer and synchronize with devnet. See [Run a FullNode](/tutorials/full-node/run-a-fullnode.md).</li></ul>| You can start a Validator and FullNode locally and connect with your local testnet for development purposes. | You must start both a local AIT Validator node locally to connect to the AIT-1. Optionally, FullNodes can also be run locally and connected to AIT-1.|
|**What not to do**| Do not attempt to sync your local AIT FullNode or AIT Validator node with devnet. | Do not attempt to sync your local testnet Validator node with Aptos Incentivized Testnet. | Make sure you deploy your local AIT FullNode and AIT Validator node in the test mode, and follow the instructions in [Deploying for Aptos Incentivized Testnet](validator-node/intro.md#deploying-for-aptos-incentivized-testnet).|
