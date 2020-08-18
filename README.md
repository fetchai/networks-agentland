# Fetch.ai Agentland network

This repo contains information on how to connect to the fetch.ai Agentland test network.

## Agent-land network API/endpoints and info
- **Chain ID:** agent-land
- **Coin denomination:** atestfet
- **Decimals:** 18 (i.e. 1 testfet = 10^18 atestfet)
- **RPC Endpoint:** [https://rpc-agent-land.fetch.ai:443](https://rpc-agent-land.fetch.ai:443)
- **Token Faucet:** [https://faucet-agent-land.fetch.ai/claim](https://faucet-agent-land.fetch.ai/claim)
- **REST Endpoit:** [https://rest-agent-land.fetch.ai:443](https://rest-agent-land.fetch.ai:443)

## Block explorer
The block explorer can be accessed by clicking [here](https://explore-agent-land.fetch.ai/)

## Installing wasmd

To install the wasmd and wasmcli executables, execute the following commands:

```bash
cd ~
git clone https://github.com/fetchai/cosmos-wasmd
cd cosmos-wasmd && git checkout tags/v0.2.0
make install
```



## Generating an account
Having installed wasmd, you can configure wasmcli to connect to the agent-land network by doing the following:
```bash
wasmcli config chain-id agent-land
wasmcli config trust-node false
wasmcli config node https://rpc-agent-land.fetch.ai:443
```

You can generate an account by executing the following line of code:
```bash
wasmcli keys add <Key name>
```

## Getting funds from the token faucet

Press the `Get Funds` button in the [block explorer](https://explore-agent-land.fetch.ai/). Target wallet address has to be specified.

## Steps for running an agent-land network node
- Initialize wasmd by running:
  ```shell script
  wasmd init <Moniker-name> --chain-id agent-land
  ```
- Execute the following command to get the genesis file:

  `curl https://rpc-agent-land.fetch.ai/genesis? | jq .result.genesis > ~/.wasmd/config/genesis.json`
- Change `allow_duplicate_ip = false` to `allow_duplicate_ip = true` in `~/.wasmd/config/config.toml`
  - on **macOS X**:
    ```bash
    sed -i  '' 's/allow_duplicate_ip = false/allow_duplicate_ip = true/' ~/.wasmd/config/config.toml
    ```
  - on **Linux**:
    ```bash
    sed -i  's/allow_duplicate_ip = false/allow_duplicate_ip = true/' ~/.wasmd/config/config.toml
    ```
- Start wasmd by connecting to the seed node:
  ```bash
  wasmd start --p2p.seeds=fac8c9cc4f94b30276437534d12a28dc6c0af420@connect-agent-land.fetch.ai:26656
  ```
