# AWS Solo Stakers Taipei
Workshop held on Monday 31st 2025 at AWS HQ in Taipei.

## Introduction

We are going to leverage AWS to set a solo staking account. This repo contains the `.yaml` file for a quicker setup. _We're skipping the policies and security rules in this workshop for simplicity_.

The `.yaml` file loads in AWS the basic setup. Besides that, we must specify a notification email and an `SSHInboundCIDR`; which basically restricts the IPs that can access the machine. The IP address we set depends on the region seved by AWS, look for `EC2_INSTANCE_CONNECT` in `https://ip-ranges.amazonaws.com/ip-ranges.json`.

Connect to EC2 instance when the machine is built.

### What do Validators do?

#### Process Transactions

- **Proposer:** "_Hey guys, I checked these transactions and they **don't contradict with my records**, let's add them to the blockchain as a new block_.

- **Attester:** "_Ok, we checked and they also don't contradict with any previous transactions in out records_.

Consensus in transacrtion validity is reached when $>2/3$ agree.

#### Secure transactions

Once consensus is reached on a subsequent block, the previous block is now finalized. Attempts to **revert finalized transactions will result in slashing** (burning $2/3$ of the stacked ETH). Ethereum's economic securiy (the total amount of ETH staked by validators), is huge _(see `https://eth2book.info/capella/part2/incentives/slashing/` for more details on slashing)._

It's easily to see that more independent verifiers and enforcements imply more censorship resistance and economic security on the network, among others. **But the percentage of solo stakers is just $~6.5\%$** (which is not a low number in absolute values, given the vast amount of validators in Ethereum).

### Opportunities for Solo Stakers

We want (and should) increase the number of solo stakers to ensure the censorship resistance and network security of Ethereum. This comes, of course, with incentives and benefits for solo stakers.

In this session, we're going to talk about **LIDO CSM** (_lower capital required + higher stETH rewards_); but there are more like **SSV DVT** ($10\%$ _staking APR boost + Base Applications_) and **Obol DVT** (_additional Obol incentives + validation on other networks_).

### Anatomy of an Ethereum Validator Node

An Ethereum Validator Node consists of:
- Validator client (which contains a signer that makes use of the validator keystores).
- Consensis client.
- Execution client.

### Validator Rewards

| **Type** | **Source** | **Annual Rate** |
|----------|------------|-------------|
| Consensus issuance | Issued by the ethereum as inflation. Also, offset by base fee paid by users | 2.4% |
| Consensys sync comittee | _(see above)_ | 0.3% |
| Execution (transaction tips) | Direct fee paid by users for speeding up their transactions | 0.3% |
| Execution (MEV) | Indirect paid by users for "_leaving money on the table_" | 0.3% |
| **Total** | | **3.3%** |

### Validator Penalties

| **Type** | **Impact** | **How to prevent** |
|----------|------------|--------------------|
| Missed duties | **Low:** $80\%$ of hat you would otherwise have earnt as rewards | Keep your validator node synced and running 24/7. Implement a monitoring and alert system |
| Slashing | **High:** 1/32 of your total effective balance + leakage | Make sure only 1 instance of each validator keys is online at any point in time. Keep your keys secure. Follow slashing protection best practices |
| [Correlation penalties](https://eth2book.info/capella/part2/incentives/slashing/#the-correlation-penalty) _(when you and many other validators go down)_| **Critical:** Up to your entire stake! | Avoid using supermajority clients. Avoid delegating to a large centralized entity. |

## LIDO CSM _(LIDO Community Stacking Module)_

It allows home staking with 1.3 ETH Bonds and 2.3x organic rewards. It is a permissionless way to enter into the LIDO Node Operator set. The goal is to help achieve 5000 independent node operators.

### Key features

- Low ETH-only bond: 1.3 ETH
- 2 sources of rewards: the rewards from the bond rewards (stETH) and the node operator rewards. LIDO makes you a node operator, so you get a % of the rewards.
- There is a bulk discount on bonds. The first bond requires 1.5 ETH and the subsequent bonds cost 1.3 ETH.
- MEV Smoothing mechanism, to even-up the favorable components of variable rewards that come from the execution layer.
- Rewards socialization: as long as your validator performance is above a certain threshold, the rewards are socialized.

### Operator Requirements

- Bonds serves as collatera, this is to prevent bad behavior.
- You need to exit your validators if requested by the protocol.
- Set withdrawal address to the LIDO Withdrawal Vault.
- Set fee recipient address to LIDO EL Rewards Vault (_LIDO execution layer rewards vault_).
- Run MEV-Boost and only use LIDO-vetted MEV RELAYS.

There are multiple plug-and-play integrations for running LIDO CSM; we are using `eth-docker`. But here is `DAppNode`, `Sedge`, `Stereum` or `EthPillar` among others.

But CSM at capacity right now, that's why we're preparing for CSM v2.

- Practive on CSM testnet.
- Get identified as an Independent Staker (WIP).
- Upload keys anyway.

> 
> - Current Testnet, Hoodi: `https://github.com/eth-clients/hoodi`.
>     - `https://hoodi.launchpad.ethereum.org/en/`.

_See the docs to set up ETH Docker: `https://dvt-homestaker.stakesaurus.com/automation-tools/eth-docker`._

Chceck `https://dvt-homestaker.stakesaurus.com/bonded-validators-setup/lido-csm` too!