# DecentPost
Protocol for decentralized postal/shipping services and apps, with Proof of Delivery, bonded shipping, and bounty slashing.

DecentPost is designed to incentivize Senders and Couriers to transact in trustless shipping engagements, allowing for global participation in the New Economy.

Concretely, it implements the OpenZeppelin ERC721 contract to allow a Sender to mint a non-fungible Package token. The token contains the public key of the intended Recipient, which is recoverable later. Metadata regarding the Package is stored on IPFS. And we implement a State Channel to allow for an expedient delivery experience + flexibility in choosing when to sign a transaction to the blockchain.

A Package represents an Offer for Shipment, and the tokens are discoverable on decentralized exchanges or special listing services.

The views in our React app, excluding the public discovery view, show Packages related to the wallet account signed-in to Metamask.

# Parties
* Sender - creates Packages, which constitute an Offer for Shipment
* Courier - agrees to Offers, transmits Packages, and collects Proofs of Delivery
* Receiver - can dispute receipt of package

# Incentives

A Shipper can specify a Bond, which a Courier must place in escrow to accept the Offer for Shipment.

They are incentivized by a Bounty, which the Shipper places in escrow on Package creation.

The Shipper also specifies a Deliver-by date, after which the Bounty will be slashed every second.

Finally, the Shipper specifies a public key address of the intended Recipient.

# Proof of Delivery
The experience of receiving a package under ideal conditions from a modern centralized courier is excellent: typically you sign a digital handheld device or show ID, and the transaction is over quickly.

Couriers and Recipients are busy, and neither party wants to wait, but it can sometimes take some time to have a transaction mined in a new block, or fees may be temporarily high.

To facilitate transactions, we have developed a concept we call Proof of Delivery, where the Recipient must prove to the Courier they are the intended Recipient.

When the package arrives, the Recipient must sign a transaction with their private key, proving they control the address the Shipper addressed the Package to.

This Proof of Delivery is saved, and can later be added to the blockchain at the discretion of the Courier. When a Proof of Delivery is mined, the Courier's is paid out their Bond + Bounty.

Should the Recipient dispute receipt of the package, the Courier can prove otherwise.

# Adversarial Conditions
If the timestamp in a Proof of Delivery is after the Deliver-By date, the Bounty is slashed.
When the Drop-Dead time arrives, the Sender is paid out the Bounty + Bond.
If a package is undeliverable, a Courier can ReturnToSender.

# Business Cases and Opportunities
multi-party carriers, i.e. international shipping + last-leg
yield management for long haul trucking and other container services
bike couriers for legal letters
local marketplaces for neighbourhood deliveries
Couriers can pay for duties and require payment during the generation of Proof of Delivery
