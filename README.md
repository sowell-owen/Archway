# Archway install guide

```shell
curl -s https://raw.githubusercontent.com/sowell-owen/Archway/main/archway > archway.sh && chmod +x archway.sh && ./archway.sh
```
When script is finished:

```shell
source $HOME/.bash_profile
```

Check logs:
```shell
journalctl -u archwayd -f -o cat
```

Wait for sync. Use this command (wait for "catching_up": false): 
```shell
curl -s localhost:26657/status
```

After sync ask for tokens in discord #faucet channel
Your archway address:
```shell
echo $ARCHWAY_ADDRESS
```

Check your balance:
```shell
archwayd query bank balances $ARCHWAY_ADDRESS
```

Create validator:
```shell
archwayd tx staking create-validator \
  --amount 9000000uaugust \
  --from $ARCHWAY_WALLET \
  --commission-max-change-rate "0.01" \
  --commission-max-rate "0.20" \
  --commission-rate "0.01" \
  --min-self-delegation "1" \
  --pubkey $(archwayd tendermint show-validator) \
  --moniker $ARCHWAY_NODENAME \
  --chain-id $ARCHWAY_CHAIN \
  --gas 200000 \
  --fees 1uaugust
```
