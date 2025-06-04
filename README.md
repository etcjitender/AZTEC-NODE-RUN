
<h2 align=center>Aztec Sequencer Node Guide</h2>

Aztec is building a decentralized, privacy-focused network and the sequencer node is a key part of it. Running a sequencer helps produce and propose blocks using regular consumer hardware. This guide will walk you through setting one up on the testnet.

**Note : There’s no official confirmation of any rewards, airdrop, or incentives. This is purely for learning, contribution and being early in a cutting-edge privacy project.**

## 💻 System Requirements

| Component      | Specification               |
|----------------|-----------------------------|
| CPU            | 8-core Processor            |
| RAM            | 16 GiB                      |
| Storage        | 1 TB SSD                    |
| Internet Speed | 25 Mbps Upload / Download   |

> [!Note]
> **You can start running this node on a `4-core CPU`, `6 GB of RAM` and `25 GB of storage`. However, as uptime increases, it's important to meet the recommended system requirements—otherwise, your node may eventually crash.**



COMMANDS

- Install `curl` and `wget` first
```bash
(command -v curl >/dev/null 2>&1 && command -v wget >/dev/null 2>&1) || sudo apt-get update; command -v curl >/dev/null 2>&1 || sudo apt-get install -y curl; command -v wget >/dev/null 2>&1 || sudo apt-get install -y wget
```
- Execute either of the following commands to run your Aztec node

```
[ -f "aztec.sh" ] && rm aztec.sh; curl -sSL -o aztec.sh https://raw.githubusercontent.com/zunxbt/aztec-sequencer-node/main/aztec.sh && chmod +x aztec.sh && ./aztec.sh
```
or
```
[ -f "aztec.sh" ] && rm aztec.sh; wget -q -O aztec.sh https://raw.githubusercontent.com/zunxbt/aztec-sequencer-node/main/aztec.sh && chmod +x aztec.sh && ./aztec.sh
```
## ⚡Commands
- You can use this command to check logs of your node
```
sudo docker logs -f --tail 100 $(docker ps -q --filter ancestor=aztecprotocol/aztec:latest | head -n 1)
```
- You can stop this node using this command
```
sudo docker stop $(docker ps -q --filter ancestor=aztecprotocol/aztec:latest | head -n 1)
```
## 🧩 Post-Installation
> [!Note]
> **After running node, you should wait at least 10 to 20 mins before your run these commands**

- Use this command to get `block-number`
```
curl -s -X POST -H 'Content-Type: application/json' -d '{"jsonrpc":"2.0","method":"node_getL2Tips","params":[],"id":67}' http://localhost:8080 | jq -r '.result.proven.number'
```
- After running this code, you will get a block number like this : 66666

- Use that block number in the places of `block-number` in the below command to get `proof`
    
![Screenshot 2025-05-02 120017](https://github.com/user-attachments/assets/ed5ba08e-a1a9-48bc-8518-b23211ac7588)

```
curl -s -X POST -H 'Content-Type: application/json' -d '{"jsonrpc":"2.0","method":"node_getArchiveSiblingPath","params":["block-number","block-number"],"id":67}' http://localhost:8080 | jq -r ".result"
```

- Now navigate to `operators | start-here` channel in [Aztec Discord Server](https://discord.com/invite/aztec)
- Use the following command to get `Apprentice` role
```
/operator start
```
- It will ask the `address` , `block-number` and `proof` , Enter all of them one by one and you will get `Apprentice` instantly

## 🚀 Register as Validator
>[!WARNING]
>You may see an error like `ValidatorQuotaFilledUntil` when trying to register as a validator, which means the daily quota has been reached—convert the provided Unix timestamp to local time to know when you can try again to register as Validator.

- Replace `SEPOLIA-RPC-URL` , `YOUR-PRIVATE-KEY` , `YOUR-VALIDATOR-ADDRESS` with actual value and then execute this command
```
aztec add-l1-validator \
  --l1-rpc-urls SEPOLIA-RPC-URL \
  --private-key YOUR-PRIVATE-KEY \
  --attester YOUR-VALIDATOR-ADDRESS \


# ⚙️ Aztec Public Testnet — Governance Voting Setup Guide

Welcome! If you're operating a **sequencer node** on Aztec's Public Testnet, you're part of an essential decentralized infrastructure. Your node must **participate in governance voting** to help shape the future of the protocol.

Proposals are **only accepted** if the **majority of active sequencers** vote in favor. This guide walks you through how to enable governance payloads and troubleshoot common issues.

---

## 🧾 Enable Governance Voting

### ✅ Option A: Using a CLI Flag

Add the governance payload directly to your `aztec` CLI command:

```bash
--sequencer.governanceProposerPayload 0x54F7fe24E349993b363A5Fa1bccdAe2589D5E5Ef
```
![image](https://github.com/user-attachments/assets/f929e5b0-c14f-49d4-860d-d7dc22055c4f)



## 📦 Example full command:

```bash
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls "" \
  --l1-consensus-host-urls "" \
  --sequencer.validatorPrivateKey "" \
  --p2p.p2pIp "" \
  --p2p.maxTxPoolSize 1000000000 \
  --sequencer.governanceProposerPayload 0x54F7fe24E349993b363A5Fa1bccdAe2589D5E5Ef
```


## 🧬 Option B: Using an Environment Variable
Use an environment variable to persist the payload configuration.


## 🧪 Temporary Session:
```bash
export GOVERNANCE_PROPOSER_PAYLOAD_ADDRESS=0x54F7fe24E349993b363A5Fa1bccdAe2589D5E5Ef
```


## 💾 Persistent Configuration:
Edit your .bashrc file:

```bash
nano ~/.bashrc
```

Add this line at the bottom:

```bash
export GOVERNANCE_PROPOSER_PAYLOAD_ADDRESS=0x54F7fe24E349993b363A5Fa1bccdAe2589D5E5Ef
```

Reload the configuration:

```bash
source ~/.bashrc
```


  --proposer-eoa YOUR-VALIDATOR-ADDRESS \
  --staking-asset-handler 0xF739D03e98e23A7B65940848aBA8921fF3bAc4b2 \
  --l1-chain-id 11155111
```



