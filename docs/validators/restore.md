---
sidebar_position: 4
sidebar_label: "Restore"
description: 'Restore and sync the 0L Network database to the current state'
---

# Restore

Restore the Database to be up to date with the current state of the Network. Repository is located [here](https://github.com/0LNetworkCommunity/epoch-archive-testnet) and contains other useful commands out this scope.
:::note
This guide is referencing the REX testnet as we develop the `libra-framework` software for v6.9.x (soon v7)
:::

### Prerequisites
:::note
You will need an account and libra configuration to use this tool
```
# Create account
libra wallet keygen
```
:::

- The Makefile is designed for libra-framework v6.9.x (soon v7) Ensure you are using the correct version.

### Initialize configs
Currently you need to sync as a full node. To do that you need to initialize `fullnode.yaml` in `~/.libra/fullnode.yaml`. An example config can be found [here](/validators/yaml-templates/fullnode-yaml)

`libra config fullnode-init`

### Setup

  Clone the repo and prepare the binary:
  
  ```
  cd ~
  git clone https://github.com/0LNetworkCommunity/epoch-archive-testnet
  cd ~/epoch-archive-testnet
  make bins
  ```


### Restoring to the latest version of the 0L Network public backup

This is most likely all you will need to restore and start/resume syncing:

  ```
    cd ~/epoch-archive-testnet
    make wipe-db && make restore-all
  ```

  This will also update your yaml file with the latest waypoint.


### Sync as a Full Node
:::note
You will need to open port `6182`
:::

#### Start

`libra node --config-path ~/.libra/fullnode.yaml`

#### Verify

You can check that you are syncing by checking that your `ledger_version` and `block_height` are increasing via the API endpoint `curl localhost:8080/v1/ | jq`

**Response**

```
{
  "chain_id": 2,
  "epoch": "700",
  "ledger_version": "3322278",
  "oldest_ledger_version": "3316234",
  "ledger_timestamp": "1699327458805056",
  "node_role": "full_node",
  "oldest_block_height": "1581950",
  "block_height": "1584970",
  "git_hash": "bafac94d6edd39d972729db21156d47758eb8969"
}
```
