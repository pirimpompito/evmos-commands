# Useful Evmos commands

## Table of contents

- [Edit validator](#edit-validator)
- [Delegate](#delegate)
- [Undelegate](#undelegate)
- [Unjail](#unjail)
- [Validators active set ranking](#validators-active-set-ranking)
- [Wallet balance](#wallet-balance)
- [Send photons](#send-photons)
- [Add key](#add-key)
- [Delete key](#delete-key)
- [List keys](#list-keys)
- [Show key details](#show-key-details)
- [Recover key with mnemonic](#recover-key-with-mnemonic)
- [Export key (unsafe)](#export-key-unsafe)
- [Import key (unsafe)](#import-key-unsafe)
- [Show current block height](#show-current-block-height)
- [Compare current block height and chain block height](#compare-current-block-height-and-chain-block-height)
- [Show number of peer connections](#show-number-of-peer-connections)
- [Node status](#node-status)

### Edit validator

```
evmosd tx staking edit-validator \
--commission-rate="<commission>" \
--details="<details>" \
--from="<your-key>" \
--identity="<identity>" \
--commission-rate="<commission-rate>" \
--fees="5000aphoton" \
--website="https://example.com" \
--moniker="<moniker>" \
--chain-id="<chain-id>" \
```

### Delegate

```
evmosd tx staking delegate <validator-address> <amount>aphoton --from <delegator-address> --chain-id <chain-id> --fees=5000aphoton
```

### Undelegate

```
evmosd tx staking unbond <validator-address> --from <delegator-address> --chain-id <chain-id> --fees=5000aphoton
```

### Unjail

```
evmosd tx slashing unjail --from=<your-key> --chain-id=<chain-id> --fees=5000aphoton
```

### Validators active set ranking

```
evmosd query staking validators --limit 3000 -o json | jq -r '.validators[] | select(.status=="BOND_STATUS_BONDED") | [.operator_address, .status, (.tokens|tonumber / pow(10; 18)), .description.moniker] | @csv' | column -t -s"," | sort -k3 -n -r | nl
```

### Wallet balance

```
evmosd query bank balances <wallet-address>
```

### Send photons

```
evmosd tx bank send <from-address> <to-address> <amount>aphoton --fees=5000aphoton
```

### Add key

```
evmosd keys add <key-name> --keyring-backend <keyring-backend>
```

### Delete key

```
evmosd keys delete <key-name>
```

### List keys

```
emvosd keys list
```

### Show key details

```
evmosd keys show <key-name>
```

### Recover key with mnemonic
```
evmosd keys add --recover <mnemonic> --keyring-backend <keyring-backend>
```

### Export key (unsafe)

```
evmosd keys unsafe-export-eth-key <key-name> --keyring-backend <keyring-backend>
```

### Import key (unsafe)

```
evmosd keys unsafe-import-eth-key <key-name> <private-key> --keyring-backend <keyring-backend>
```

### Show current block height

```
evmosd status --node http://arsiamons.rpc.evmos.org:26657 | jq .SyncInfo.latest_block_height
```

### Compare current block height and chain block height

```
evmosd status --node http://arsiamons.rpc.evmos.org:26657 | jq .SyncInfo.latest_block_height && evmosd status | jq .SyncInfo.latest_block_height
```

### Show number of peer connections

```
curl -s http://localhost:26657/net_info | jq '.result.n_peers'
```

### Node status

```
curl -s http://localhost:26657/status | jq '.'
```

