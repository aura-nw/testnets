# Euphoria: Incentivized staging environment for Aura Network

This document provides a draft version of the incentivized program for bootstrapping a staging environment for Aura Network with the codename: Euphoria. We are open to suggestions to make the program more fair and attractive to the Aura Network community.

If you have good suggestions, there are several channels where we are online almost all the time:

- Aura Network discord: either tag us on the main or dm @eledra or @kienvc.
- Twitter: [EledraNguyen](https://twitter.com/EledraNguyen)
- If you have access to the shared version of the document on Google docs, please just comment on it.

**TL;DR**

- Euphoria is Aura Network staging environment before launching mainnet.
- 50 validators limit, selection criterias are defined by Aura team.
- Incentivized, 60 Aura token / day and other benefits.
- Fill out this form and wait for the result: https://forms.gle/ACVNdmzeEcxcGqzX7

## 1. Context

### 1.1. About Aura Network
Aura Network is a layer-1, NFT-centric blockchain that focuses on expanding the use of NFTs across various industries. Our vision is to create a one-stop destination for minting, evaluating, querying, and transacting NFTs, to become a pioneer NFT infrastructure for the future.

Aura's unique selling point is that the Aura Network team is actively working with brands, game studios and major IP owners in Asian countries (Vietnam, Thailand, Indonesia, Japan, Korea, etc.) to bring more accessibility to NFT or cryptocurrencies in general to their existing portfolio. Aura is not “just another Stargaze or Omniflix on Cosmos”, Aura Network is an application focus chain with a clear targeted customer segment in the beginning and gradually will become a full ecosystem by itself.

Aura Network is backed by top-tier partners including crypto projects, VCs, DAO as well as traditional firms.
Find more information about Aura here: https://aura.network.

### 1.2. Network Environment

Currently, Aura Network has 2 main testing environments: **Serenity** testnet and **Halo** testnet. Both are tightly controlled networks with a limited number of validators controlled by the Aura team and some other partners. These are mostly for DApp testing purposes rather than a close resemblance to the production mainnet environment. DApp developers can freely use Serenity as a development and testing environment for their applications. Meanwhile, the Halo network can be used as a playground for validators to practice running their nodes.

In order to prepare for the mainnet launch, we decided to create another environment with real validators to evaluate the security and decentralization aspect of the product. This new environment is referred to as the **staging environment**, code name: **Euphoria**

Similar to the staging environment concept in traditional software development, Euphoria is the near exact replica of Aura Mainnet. This means we will try our best to bootstrap external validators, set up vesting, voting and operate the Euphoria bootstrap community as closely as we will do on Aura Mainnet in the future.

In the following sections, we describe in detail Euphoria and various aspects that we carefully consider when bootstrapping it.

## 2. Validator Bootstrapping

Getting validator involvement is the first step towards a good mainnet launch and a long-term decentralized network. To ensure a successful launch and a decentralized network, a group of validators must be chosen so that the network can always reach consensus as Tendermint requires at least ⅔ nodes online to reach consensus at any block. As Euphoria tokens are not mainnet tokens, we want to encourage validators to take part in the Euphoria network through our **Incentivized Validator Program (IVP).**

The point of incentivization is not about making money during the time of the program but to compensate validators for the time and resources they spend on the Euphoria environment. However, participating in this program will be a mandatory step to becoming a genesis validator in the Aura Network mainnet. Thus, there are several requirements.

### 2.1. Qualification

In order to participate in the IVP, validators must pass these following requirements:

- Participating in our KYC process. The KYC process is to make sure people don’t cheat the system by running multiple validator instances as well as ensuring that we aren't involved with criminal activities.
- Citizens of any UN sanctioned countries (Afghanistan, Cuba, Iran, North Korea and Syria) are **NOT eligible** to participate in the program. 

Demonstrate their capability in running a proof-of-stake validator node by providing their existing portfolio. We are very open to work with reputable Cosmos validators, but if you are experienced in other types of popular blockchain networks, it is acceptable.
Additionally, there can be exception if the validator is either:

- Have a recommendation from one of Aura Network seed backers.
- Get a direct invitation from the Aura Network team.

Validators who complete the qualification process will become **Qualified Validators** and will be eligible for our airdrop process in the IVP to be included in the active set at the genesis block of Euphoria.

### 2.2. Selection Criteria
The initial maximum slot for the active set of Euphoria is **50**, thus there should be criteria for selecting participants if the number of qualified validators is greater than 50. The final result is decided by the Aura team, taking into account the consultation of partners and major validators that we handpicked. However, we will try to maximize the diversity of the validator set in terms of:

- Experience in the Cosmos ecosystem.
- Recommendation of Aura’s partners or already bought our tokens.
- Community representation.
- Experience in running validators for other networks.
- Geological location.

We will also try to reserve some slots for Independent validators if they can demonstrate their skills and determination to work with Aura Network for the long term.

### 2.3. Schedule

Validators have 2 weeks to complete the KYC process, starting from: **22 June 2022**

The KYC process is carried out by [Synaps](https://synaps.io/), a reputable KYC service provider who has provided services for 

After completing KYC and collecting genesis resources, Euphoria network can be launched at: **TBD**

The IVP is expected to last until Aura Network launches its mainnet by early Q4 2022.

After launching mainnet, as we don’t need to maintain Euphoria at a large scale anymore, validators who are willing to continue running the testnet can work with us to make a new environment for future testing purposes. Developers can consider Euphoria to be their true staging environment before moving apps from Serenity to mainnet.

### 2.4. Requirements for validators

Selected validators for the IVP are required to participate in launching and operating the Euphoria network. In particular:

- Participating in all network activities that are announced by the Aura Network team. Details are in part 3 of this document.
- Maintaining Aura nodes to ensure a healthy network. 
- For each validator node, we expect there will be no more than **3 downtime slash events in each month**. The configuration for slashing threshold is **500 missed blocks over a window of 10000 blocks**. For a double sign fault, the validator will be removed immediately from the IVP.
- Also, the total time spent for recovering a node from jail to unjail status in a month should be no more than **36 hours**.
- These conditions only apply in time that there is no error on the software provided by the Aura Network team that prevents a validator from running.

If a validator fails to deliver these requirements, they should be removed from the IVP and we will arrange the vacant slot for the next in-line validator who has passed KYC but has not been selected. However, if the failed validator can clearly explain their problem, we will conduct a vote for the rest of the validator set to decide whether to retain the status of the failed one.  

All validators are welcome to contribute in promoting and governing the Aura Network. The team will take into account all contributions in a transparent manner.

### 2.5. Rewards

There are several benefits to validators participating in the IVP:
- **Compensation**: For each day running a validator node in the IVP, each validator will receive a reward of 60 Aura Tokens (IDO price: 0.065 USD) on mainnet. This amount is calculated by the Aura team, taking into consideration the valuation of the project, average spending for infrastructure and recommendations from various partners. The compensation amount is taken from the ecosystem growth fund. These tokens will be directly credited to genesis validators and bonded in the genesis block of Aura mainnet. 
- **Exception**: However, as we cannot give or sell tokens to US and mainland China, validators coming from these 2 countries will not receive IVP compensation. Instead, they will receive an equal amount of tokens to the IVP rewards with the purpose of bootstraping their nodes into the genesis set and self-bonding only. If later on they decide to leave the network these validators must return the initial bootstrap tokens to the eco growth fund.
- **Guarantee Genesis Validator slot**: All validators who complete the IVP will be included in the genesis block of Aura mainnet.
- **Chance to get delegation from Aura Network partners**: The Aura team will send all validator information and their contribution to the IVP to all Aura partners who own Aura tokens from strategic and private rounds. We will also recommend partners to choose several validators to delegate at the beginning of the mainnet phase to ensure decentralization.

## 3. Network activities

### 3.1. Performance test
To be announced after bootstrapping validators.

### 3.2. Mainnet launch test
This scenario is used for final testing before launching mainnet. The network setting will be exactly the same with mainnet configuration.
Plan:
- Stop Euphoria network
- Reset all data and states
- Launch it again with mainnet parameters

### 3.3 Others
Various activities will be announced in the future.

## 4. Launching procedures

### 4.1. Register for the program
Please fill in your validator information here:

https://forms.gle/ACVNdmzeEcxcGqzX7

After that, we will send out the KYC link to your registered email.

### 4.2. Setup network resources
Euphoria repository:
https://github.com/aura-nw/testnets/tree/main/euphoria-1

| #  | To-do                                                                                    | Aura | Partners | Docs |
|----|------------------------------------------------------------------------------------------|------|----------|------|
| 1  | Generate pre-launch genesis with custom parameters                                       |  ✅   |          |      |
| 2  | Upload pre-launch genesis and instructions to Euphoria repo                              |  ✅   |          |      |
| 3  | Generate validator transaction (gentx) with fixed bonded tokens using pre-launch genesis |      | ✅        | [Link](https://github.com/aura-nw/testnets/blob/main/euphoria-1/pre-lauch-setup.md#generate-genesis-transaction-pre-launch-only) |
| 4  | Submit gentx and logo by forking Euphoria repo and create a Pull Request                 |      |  ✅       | [Link](https://github.com/aura-nw/testnets/blob/main/euphoria-1/pre-lauch-setup.md#submit-gentx-and-logo) |
| 5  | Collect gentx, verify and finalize genesis                                               |  ✅   |          |      |
| 6  | Upload finalized genesis to Euphoria repo                                                |  ✅   |          |      |
| 7  | Replace pre-launch genesis by the finalized one                                          |  ✅   |  ✅       | [Link](https://github.com/aura-nw/testnets/blob/main/euphoria-1/pre-lauch-setup.md#download-finalized-genesis-and-setup-your-validator) |
| 8  | Setup validators (aurad, cosmovisor services)<br>Optional: seed mode, fullnode           |  ✅   |  ✅       | [Link](https://github.com/aura-nw/testnets/blob/main/euphoria-1/pre-lauch-setup.md#download-finalized-genesis-and-setup-your-validator) |
| 9  | Setup AuraScan                                                                           |  ✅   |          |      |
| 10 | Run node and wait for launching time                                                     |  ✅   |  ✅       |      |

