# Nolus-Snapshot
Snapshots allows a new node to join the network by recovering application state from a backup file. Snapshot contains compressed copy of chain data directory. To keep backup files as small as plausible, snapshot server is periodically beeing state-synced.

Snapshots are taken automatically every 6 hours starting at `03:15 UTC`

pruning: 100/0/19 | indexer: null | version tag: v0.1.43
--------------------------
| BLOCK | AGE | DOWNLOAD
--------------------------
| 1206194 | 1 minutes | snapshot (1.72 GB)
--------------------------

## Instructions

## Stop the service and reset the data

```
sudo systemctl stop nolusd
cp $HOME/.nolus/data/priv_validator_state.json $HOME/.nolus/priv_validator_state.json.backup
rm -rf $HOME/.nolus/data
```

## Download latest snapshot

```
curl -L https://snapshots.kjnodes.com/nolus-testnet/snapshot_latest.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.nolus
mv $HOME/.nolus/priv_validator_state.json.backup $HOME/.nolus/data/priv_validator_state.json
```

## Restart the service and check the log

```
sudo systemctl start nolusd && sudo journalctl -u nolusd -f --no-hostname -o cat
```
