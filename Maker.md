---
permalink: /
layout: page
title: Introduction to Maker
---


## Quick information
-------------------------------

Maker is a Decentralized Autonomous Organization (DAO) that backs the value of the dai stablecoin on the Ethereum blockchain. A DAO is an organization that is entirely blockchain-based using smart contracts to enforce its rules and business logic.

**Dai** is a stablecoin used for trade and transfers on Ethereum. A stablecoin is a cryptocurrency with price stability.

**MKR** is a speculative share that backs the value of the dai. Maker earns a continuous fee on all outstanding dai in return for governing the system and taking on the risk of bailouts. Maker's income is funnelled to MKR owners through Buy&Burn.

#### Quick links

* [Chat](https://chat.makerdao.com) - Primary platform of community interaction
* [Forum](https://forum.makerdao.com) - For debate and proposals
* [Subreddit](https://www.reddit.com/r/makerdao) - Best place to get latest news and links
* [GitHub](https://github.com/makerdao) - Repository of the public Maker code
* [TeamSpeak](https://ts.makerdao.com/) - For governance meeting conference calls
* [SoundCloud](https://soundcloud.com/makerdao) - Governance meeting recordings
* [Market](https://mkr.market) - MKR and DAI decentralized exchange


Introduction to the dai stablecoin and Maker
------------------------------------

### Dai and Maker

Dai is a stablecoin on Ethereum. Maker is the organization that backs the dai's stability by regulating its collateral requirements.

New dai enter the money supply when a *borrower* borrows dai by posting collateral with Maker. The collateral is held in a smart contract called a Collateralized Debt Position (CDP). A CDP is used to back the value of the dai in a fully transparent manner that anyone can verify.

Any Ethereum account is free to borrow dai without any requirements or restrictions beyond posting and maintaining adequate collateral. Dai borrowing has no term limits, and borrowers can open and cover CDPs at any time.

Dai *holders* buy dai from borrowers and use it as a stablecoin for transactions on Ethereum as well as a long-term store of value.

### MKR, the share of Maker

MKR is the name of the token that acts as shares in the Maker DAO. The price of MKR depends on the performance of the dai.

All dai borrowers pay a *stability fee* which is funneled to MKR owners with Buy&Burn. Buy&Burn means using income to buy up MKR and permanently destroying them. In return, Maker acts as a market maker of last resort that automatically liquidates risky CDPs.

The total MKR supply starts at 1,000,000 MKR. Before deployment of the system, 421,897 MKR (42.1897%) were distributed to founders and early buyers.

The remaining undistributed 578,103 MKR were given to the Maker Fund. The Maker Fund is a smart contract separate from the core system that holds money on behalf of the Maker DAO. It is controlled temporarily by MKR owners who participate in governance, called *governors*.

### The basic mechanics

The target price of the dai is denominated in Special Drawing Rights (SDR) - an international currency basket maintained by the IMF that has low volatility against all major world currencies. When the dai is launched, the value of 1 DAI will be pegged to an initial target price of 1 USD worth of SDR at [the exchange rate reported by the IMF](https://www.imf.org/external/np/fin/data/rms_sdrv.aspx). After launch, the dai will detach from this initial target and start to slowly fluctuate against the SDR. It will have a bias towards deflation under normal conditions over the long term while maintaining low volatility in the short term.

Borrowing new dai is done by locking an amount of collateral inside a CDP smart contract.  The CDP then sends newly borrowed dai to the borrower's wallet while also creating a corresponding amount of debt. Over time, the CDP accrues a stability fee ,"interest", which is added on top of the debt. The borrower can retrieve the posted collateral by *covering* the debt plus the stability fee accrued since the CDP was created. All stability fees from CDPs go into the Buy&Burn contract.

>*__Example 1:__ Bob wants to borrow 100 dai. He locks an amount of ETH worth significantly more than 100 dai into a CDP and uses it to borrow 100 dai. The 100 dai is instantly sent directly to his Ethereum account. Assuming that the stability fee is 0.5% per year, over the coming year Bob will need 100.5 dai to cover the CDP if he decides to retrieve his ETH after one year.*

The deflationary nature of the dai means that the market value (measured in SDR) of the debt also increases over time.  This adds an additional cost to borrowing beyond the stability fee. The dai deflation is a transfer of value from dai borrowers to dai holders, while the stability fee is a transfer of value from dai borrowers to MKR owners.

One of the primary use cases of CDPs is margin trading by borrowers.

>*__Example 2:__ Bob wishes to go margin long on the ETH/DAI pair, so he borrows 100 SDR worth of dai by posting 150 SDR worth of ETH to a CDP. He then buys another 100 SDR worth of ETH with his newly borrowed dai putting him at a net 1.66x ETH/SDR exposure. He’s free to do whatever he wants with the 100 SDR worth of ETH he obtained by selling the dai, while the original ETH collateral (150 SDR worth) remains locked until the debt plus the stability fee is covered.*

Although CDPs are not fungible with each other, the ownership of a CDP is transferable. This allows CDPs to be used in smart contracts that perform more complex methods of borrowing (for example, involving more than one actor).

>*__Example 3:__ Alice and Bob collaborate using an Ethereum OTC contract to issue 100 SDR worth of dai backed by ETH. Alice contributes 50 SDR worth of ETH, while Bob contributes 100 SDR worth. The OTC contract takes the funds and creates a CDP, thus borrowing 100 SDR worth of dai. The newly borrowed dai are automatically sent to Bob. From Bob's point of view, he is buying 100 SDR worth of dai by paying the equivalent value in ETH. The contract then transfers ownership of the CDP to Alice. She ends up with 100 SDR worth of debt (denominated in dai) and 150 SDR worth of collateral (denominated in ETH). Since she started with only 50 SDR worth of ETH, she is now 3x long ETH/SDR.*

How Maker keeps the dai stable
------------------------------

The stability of the dai around the target price is maintained by modifying the incentives for borrowing and holding Dai via *deflation rate adjustments*.

### Deflation rate adjustments

The deflation rate of the dai is continuously applied to the target price, increasing (or decreasing) it over time according to market demand. Deflation rate adjustments ensure that the dai market price remains stabilized around the target price. When the market price of the dai is below the target price, the deflation rate of the dai increases causing borrowing to become more expensive.  This leads to a corresponding reduction in supply of dai. At the same time, the increased deflation rate causes the capital gains from holding dai to go up, and leads to a corresponding increase in dai demand. This combination of reduced supply and increased demand causes the dai to appreciate in value, pushing it up towards the target price.

The same mechanism works in reverse if the market price is higher than the target price: the deflation rate decreases, leading to an increased demand for borrowing dai and a decreased demand for holding it. This causes the dai to depreciate in value, pushing it down towards the target price.

This mechanism is a negative feedback loop: Deviation away from the target price in one direction increases the force in the opposite direction. The magnitude of the deflation rate adjustments depends on how long the market price remains on the same side of the target price. Longer deviations result in aggressive adjustments, while shorter deviations result in small adjustments.

### Enforcing the target price: Liquidation

To directly enforce the target price in the marketplace, a CDP gets liquidated by Maker if it hits its *liquidation ratio*. Liquidation means Maker takes over the collateral and sells it off in a *continuous splitting auction*, a public auction mechanism that is specialized for automatic price discovery.

In order for Maker to take over the collateral so it can be sold off, *emergency debt* is instantly used to create dai that is backed by the ability of Maker to dilute the MKR supply. A reverse auction is used to find the lowest amount of MKR that needs to be diluted in order to raise enough dai to pay off the emergency debt. This type of auction is called a *debt auction*.

Simultaneously, the collateral is sold off in a continuous splitting auction for dai where all dai proceeds up until the *liquidation penalty* are immediately sent to the Buy&Burn contract. If enough dai has been bid to cover the liquidation penalty, the auction switches into a reverse auction to try to sell as little collateral as possible; any leftover collateral is returned to the borrower that originally created the CDP.

>*__Example 4:__ If we assume that Ether has a liquidation ratio of 145%, a penalty ratio of 105%, and an Ether-CDP is outstanding at 150% collateral ratio, the Ether price crashes 10% against the target price. This causes the collateral ratio of the CDP to fall to ~135%. As it falls below its liquidation ratio, traders can trigger its liquidation and begin bidding with dai for buying MKR in the debt auction.  Traders can also begin bidding with dai for buying the ~135 dai worth of collateral in the collateral auction. Once there is at least 105 dai being bid on the Ether collateral, traders reverse bid to take the least amount of collateral for 105 dai and the remainder is returned to the original borrower.*

Managing the stability of the system
---------------------------------------

Liquidations aren't guaranteed to be profitable even if triggered when the collateral ratio of the CDP is positive. Slippage or a market crash could cause the liquidation auction to burn less MKR than what was diluted from the debt auction resulting in net loss for Maker and a net increase of the MKR supply.

Maker has multiple risk parameters that ensure the system remains stable despite this risk. These parameters are controlled by the governors.

**Stability fee**

The stability fee is a fee paid by every CDP. It is defined as a yearly percentage that is calculated on top of the existing debt of the CDP. When the borrower covers their CDP, the dai used to cover the CDP debt is destroyed, but the dai used to pay the stability fee is sent to the Buy&Burn contract.

**Debt ceiling**

Debt ceiling is the maximum amount of debt that can be created by a single type of CDP. Once enough debt has been created by CDPs of a given type, it becomes impossible to create more unless existing CDPs are closed.

**Liquidation ratio**

Liquidation ratio is the collateralization ratio at which a CDP can be liquidated.

**Penalty ratio**

The penalty ratio is used to determined the maximum amount of dai raised from a liquidation auction that goes to Buy&Burn, with the remainder getting returned to the borrower who originally created the CDP.

How external agents assist Maker
--------------------------------

### Keepers: Keeping the system economically efficient

Traders that systematically earn an income from Maker and the dai by exploiting simple profit opportunities are a class of agents called **keepers**. In a general sense, a keeper is an economic agent that contributes to decentralized systems in exchange for built-in rewards. In the context of Maker, keepers perform several important functions:

**Participating in continuous splitting auctions**

Each keeper is constantly scanning the blockchain for CDPs that have gone below their liquidation ratio and can have a liquidation auction triggered. Keepers bid on auctions with the goal of getting a price that is better than the market rate so that they can instantly sell the earned asset for profit.

**Market making the dai around the target price**

Each keeper will want to try to sell dai when the market price is higher than the target price. Similarly, keepers buy dai when the price is below the target in order to profit from the known long-term convergence towards the target price and make money from the spread.

A keeper can additionally act as an Oracle by providing a price feed, as described in the following section:

### Oracles: Providing external price feeds

Another crucial group of external actors that Maker requires to function are price feed oracles. Oracles are mechanisms that provide information from the outside world onto the blockchain for smart contracts to consume. Maker needs information about the market price of the dai and its deviation from the target price in order to adjust the deflation rate. It also needs information about the market price of the various assets used as collateral for the dai in order to know when liquidations can be triggered.

### Capital Investment Firms: Dai backed by off-chain collateral

Capital Investment Firms (CIFs) are companies (legal entities) that specialize in repackaging legal securities into a format that can be used as collateral for borrowing dai. This is achieved through a smart contract called the *CIF Trap*, which enables Maker to give the CIF a debt ceiling based on its internal holdings of legal securities. CIFs increase the ability of the system to respond to dai demand shocks by borrowing dai and trading it for other assets.

Governance of Maker
-----------------------------------

### The voting process

*Direct governance* means controlling Maker directly through voting with an Ethereum account that holds MKR. An account gets a vote for each MKR token held. MKR owners who actively vote and participate in governance are called *governors*. A simple majority vote has full authority of the system to change the voting rules, alter the business logic, spend money from the Fund, and lock down Maker's smart contracts as the system matures.

There are four major phases when governors exercise direct governance over Maker through the voting process.

**The first phase** is deploying and publishing the *action proposal*, a smart contract that will change the status quo of Maker if it gets executed by directly modifying the state of its smart contracts.

**The second phase** is *initiating* the action proposal for public vote by the governors. This enables governors to vote on the action proposal with their MKR and starts the expiration timer of the action proposal.

**The third phase** is the voting process. Voting is done according to the voting rules of the system, that themselves are modifiable until they are locked down by the governance process. Each action proposal has an expiration time after which it is automatically abandoned.

**The fourth phase** is execution of the *action*, the transaction that modifies the state of the Maker smart contracts.

### Voter organization

An important part of direct governance is voter organization. To make it as straightforward as possible for governors to coordinate their votes and discuss action proposals, a weekly *formal governance meeting* is held as a conference call using the TeamSpeak platform, currently defined to happen every Sunday at 15:00 GMT.

While the contract system allows initiating proposals for vote at any time, during normal conditions it is in practice only done at the governance meeting. If a proposal is initiated for vote outside the social framework of the governance meeting, it indicates either an attack on the system, or a breakdown of the governance framework and a potential governance crisis.

All governance related discussion and debate that doesn't take place in the framework of the governance meeting is referred to as *informal governance*. The Maker chatroom and the Maker forum act as the primary communications platforms for shareholders to discuss and debate all aspects of the DAO and its governance, and for governors to schedule governance meetings.

### Governance in action: from idea to action proposal

**Informal governance proposal:** A new proposal will first be brought up and discussed on chat and the forum - in this setting of public and freeflowing information a proposal will be rapidly scrutinized and any obvious objections will be raised immediately by the community. The proposal can then be amended based on input and objections or abandoned.

**Formal governance proposal:** Once a proposal has been amended to a form that doesn't have any obvious objections, it can move on to formal governance. Formal governance ensures that every governor is present to weigh the proposal as it is presented in formal parlance that emphasizes the use of simple English with live translation to other major languages. If there is input and objections to the proposal they have to be properly articulated, and if necessary the proposal can be delayed until the next governance meeting to allow another week of informal governance. When a proposal no longer has any formal objections or input, an action proposal has to be created and published for scrutiny so that governors can ensure that it properly implements the spirit of the proposal.

**Direct governance vote:** When the action proposal is considered ready for vote, it is initiated by the proposer and governors can begin the process of voting for or against it. As mentioned above, the initiation has to be done during the governance meeting or it is considered either an attack or a governance crisis. The process of voting extends beyond the governance meeting where it was proposed, allowing plenty of time for every governor to vote even if they weren't present.
