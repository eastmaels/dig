Remember the version is `v1.1.0`. Remember to run both mainnet and testnet on the same machine.
```
cd ~/dig
git checkout v1.1.0
make install
```
1. Init
```
cd $HOME && mkdir digtest
digd init <moniker> --chain-id digtest-5 --home digtest
```
2. Download new genesis:
```
wget -O ~/digtest/config/genesis.json https://github.com/notional-labs/dig/blob/master/networks/testnets/testnet-5/genesis.json
```
3. Join the testnet with new seeds:
```
digd start --p2p.seeds fec3524b68e228ac1f1f87ba287de9b4f04a8690@168.119.91.22:1230 --home /$HOME/digtest
```
4. Generate new keys or restore the existing one;
```
digd keys add <key-name> --home /$HOME/digtest
```
If you have validator address before, add `--recover` flag and type your mnemonic to recover.
5. Create validator! 
 ```
 digd tx staking create-validator \
  --amount=1500000000udig \
  --pubkey=$(digd tendermint show-validator) \
  --moniker=<moniker> \
  --chain-id=digtest-5 \
  --commission-rate="0.05" \
  --commission-max-rate="0.20" \
  --commission-max-change-rate="0.01" \
  --min-self-delegation=1 \
  --gas 200000 \
  --fees 250000udig \
  --from=<validator> \
  --home /$HOME/digtest
 ```