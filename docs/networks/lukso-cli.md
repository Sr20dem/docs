# LUKSO CLI

>⚠️ This page may change. Not everything is ready yet.

## Installation ( Linux/MacOS )
`curl https://install.l15.lukso.network | bash`

## Installation ( Windows )
Run `powershell` as an administrator  

`(New-Object System.Net.WebClient).DownloadString("https://install.l15.lukso.network/windows") | powershell -command -`  



This shell script will: 
1. Create directory under `/opt/lukso`
2. Download zipped files required for node startup.
3. Unzip them (using `unzip` tool)
4. Create symbolic link in `/usr/local/bin`.

## Running
Enter `lukso config` in your shell to generate config file. You may need to use `sudo` on `macos` devices.

Example:
~~~yaml
COINBASE: "0x616e6f6e796d6f75730000000000000000000000"
WALLET_DIR: "/home/user/.lukso/l15/vanguard-wallet"
DATADIR: "/home/user/.lukso/l15/datadirs"
LOGSDIR: "/home/user/.lukso/l15/logs"
NODE_NAME: "l15-60F08373"
~~~
After that, simply run:  
`lukso start` to start an archive node  
`lukso start --validate` to start a validator node


## Available parameters
`lukso <command> [argument] [--flags]`

| command   | description            | argument |
|-----------|------------------------|----------------------|
| start     | Starts up all or specific client(s) | [orchestrator, pandora, vanguard, validator, eth2stats-client, **all**] |
| stop      | Stops all or specific client(s)     | [orchestrator, pandora, vanguard, validator, eth2stats-client, **all**] |
| reset     | Clears client(s) datadirs (this also removes chain-data) | [orchestrator, pandora, vanguard, validator, all, **none**]
| config    | Interactive tool for creating config file | |
| keygen    | Runs `eth2deposit-cli` | |
| wallet    | Imports `eth2deposit-cli` keys | |
| logs      | Show logs | [orchestrator, pandora, vanguard, validator, eth2stats-client] |
| bind-binaries      | sets client(s) to desired version | 
> In **bold** is a behaviour when argument is skipped (default)

### start

| name      | description            | Argument  |
|-----------|------------------------|---|
| --network | Picks which setup to use | Name of network from list: `mainnet, l15, l15-staging, l15-dev`
| --l15 | Shorthand alias for `--network l15` | <none\>
| --l15-staging | Shorthand alias for `--network l15-staging` | <none\>
| --l15-dev | Shorthand alias for `--network l15-dev` | <none\>
| --config | Path to config file     | Path ex. `config.yaml` |
| --validate | Starts validator      | <none\>
| --coinbase | Sets pandora coinbase. This is public address for block mining rewards (default = first account created) (default: "0") | ETH1 addres ex. `0x144a9533B3d759d647597762d33a1cD6f9Bf118c`
| --node-name  | Name of node that's shown on pandora stats and vanguard stats | String ex. `johnsmith123` 
| --logsdir  | Sets the logs path | String ex. `/mnt/external/lukso-logs` 
| --datadir  | Sets datadir path | String ex. `/mnt/external/lukso-datadir`
| --home  | Sets path for datadir and logs in a single location (--datadir and --logs take priority) | String ex. `/var/lukso` 
| --orchestrator-verbosity  | Sets orchestrator logging depth | String ex. `silent, error, warn, info, debug, trace` 
| --pandora-verbosity  | Sets pandora logging depth (note: pandora uses integers for that flag, script will convert those to proper values) | String ex. `silent, error, warn, info, debug, trace` 
| --pandora-bootnodes  | Sets pandora bootnodes | Strings of bootnodes separated by commas: `enode://72caa...,enode://b4a11a...`
| --pandora-http-port  | Sets pandora RPC (over http) port | Number between 1023-65535
| --pandora-metrics  | Enables pandora metrics server | <none\>
| --pandora-nodekey  | P2P node key file | Path to file (relative or absolute)
| --pandora-external-ip  | Sets external IP for pandora (overrides --external-ip if present) | String ex. `72.122.32.234`
| --vanguard-verbosity  | Sets vanguard logging depth | String ex. `silent, error, warn, info, debug, trace`
| --vanguard-bootnodes  | Sets vanguard bootnodes | Strings of bootnodes separated by commas: `enr:-Ku4QAmY...,enr:-M23QLmY...`
| --vanguard-p2p-priv-key  | The file containing the private key to use in communications with other peers. | Path to file (relative or absolute)
| --vanguard-p2p-host-dns  | Sets host DNS vanguard (overrides --external-ip AND --vanguard-external-ip if present) | String ex. `72.122.32.234`
| --validator-verbosity  | Sets validator logging depth | String ex. `silent, error, warn, info, debug, trace`
| --external-ip  | Sets external IP for pandora and vanguard | String ex. `72.122.32.234`
| --allow-respin  | Deletes all datadirs IF network config changed (based on genesis time) | <none\>

How to use flags with values? Provide a flag and value like: `lukso start --datadir /data/network-node`

### stop
| name      | description            | Argument  |
|-----------|------------------------|---|
| --force   | Adds force option to kill commands (may result in corruption of node data)     | <none\> |

### bind-binaries 
| name      | description            | Argument  |
|-----------|------------------------|---|
| --orchestrator   | download and set `orchestrator` to given tag  | Tag, ex. `v0.1.0-rc.1` |
| --pandora   | download and set `pandora` to given tag  | Tag, ex. `v0.1.0-rc.1` |
| --vanguard   | download and set `vanguard` to given tag  | Tag, ex. `v0.1.0-rc.1` |
| --validator   | download and set `validator` to given tag  | Tag, ex. `v0.1.0-rc.1` |

