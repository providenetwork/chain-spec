# Network configuration

Each network must have a branch with `spec.json` and `bootnodes.txt`.

## Network IDs

- `100` (`0x64`) - mainnet
- `22` (`0x16`) - unicorn testnet


## Contribution guides

Make sure you know what you're doing before making changes to `spec.json`.


## Deployment steps

- Deploy Bootnodes
  `parity  --chain spec.json --base-path ./.datadir --force-sealing --reseal-on-txs all  --bootnodes enode://@unicorn-bootnode0.provide.network:30300,enode://@unicorn-bootnode1.provide.network:30300 --port 30300 --jsonrpc-port 8550 --ui-port 8180 --ws-port 8540 --jsonrpc-apis web3,eth,net,personal,parity,parity_set,traces,rpc,parity_accounts`

- Deploy "Fat" Bootnodes

    - Parity +Fat +Trace
      `parity --chain provide.network-spec.json --base-path ./provide.network --force-sealing --reseal-on-txs all --bootnodes enode://@unicorn-bootnode0.provide.network:30300 --fat-db on --pruning archive --tracing on --port 30300 --jsonrpc-interface all --jsonrpc-port 8050 --jsonrpc-cors all --ws-port 8051 --ws-interface all --ws-hosts all --ws-origins all --ui-interface all --ui-port 8052 --ui-hosts all --jsonrpc-apis web3,eth,net,personal,parity,parity_set,traces,rpc,parity_accounts`

    - Block Explorer
      `PORT=3001 npm start`

    - Netstats (eth-netstats)
      `PORT=3002 WS_SECRET=XXXX npm start`

    - Netstats Daemons (eth-net-intelligence-api)
      `pm2 start app.json`

- Deploy Master of Ceremony:
  `parity  --chain spec.json --base-path ./.datadir --bootnodes enode://@unicorn-bootnode0.provide.network:30300,enode://@unicorn-bootnode1.provide.network:30300 --force-sealing --port 30300 --jsonrpc-port 8550 --ui-port 8180 --ws-port 8540 --jsonrpc-apis web3,eth,net,personal,parity,parity_set,traces,rpc,parity_accounts --engine-signer 0x... --password ./.moc.key`
