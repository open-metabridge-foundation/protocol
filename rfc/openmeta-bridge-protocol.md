---
title: "OpenMeta Bridge Protocol (OMBP)"
abbrev: "OMBP"
category: info

docname: draft-openmeta-dinrg-protocol-latest
v: 3
area: "IRTF"
workgroup: "Decentralized Internet Infrastructure"
keyword: Internet-Draft
venue:
  group: "Decentralized Internet Infrastructure"
  type: "Research Group"
  mail: "din@irtf.org"
  arch: "https://www.ietf.org/mail-archive/web/din/current/maillist.html"
  github: "project-metatag/internet-draft"
  latest: "https://project-metatag.github.io/internet-draft/draft-metatag-dinrg-protocol.html"

author:
 -
    fullname: Yannik Goldgräbe
    organization: yannik.gold
    email: "hi@yannik.gold"
 -
    fullname: Marco Lewandowsky
    email: "marco.lewandowsky@gmail.com"

normative:

informative:


--- abstract

TODO Abstract


--- middle

# Status
This document is fully work in progress.

# Introduction
This protocol family extends upon any non-fungible token (NFT) standard. It enables these digital assets to become connected with a physical counterpart, as well as the other way around; physical assets can be immortalized on any distributed ledger that supports smart contracts by minting a cryptographically connected token.

This specification defines the core functionalities: registering and claiming the digital ownership of a physical object. It also describes the security and privacy considerations for usage.

Additionally, the protocol family includes specifications on physical object verification and the management of the physical object manufactures in the context of this novel ecosystem.

From a philosophical perspective, this protocol family is aiming to merge and connect objects from the real (tangible and physical) world into digital universes, following the interconnected metaverse principles. Through these protocols, it is possible to create eternal references in the metaverse possibly going way beyond the lifetime of the physical object. Common terms for such approaches are often referred to as digital twins or totality.
The authors are aware that this is an ambitious project, though multiple other parties are working on similar approaches which commonly are proprietary, closed source and not agnostic.
The goal with this specification is to lay out a common standardized foundation that allows to be extended upon in a collaborative approach.

## Roles
The following participants are involved as part of the protocol communication flows.

### Item / Object / Asset
The physical Object lies at the core of the protocol. An Object is brought to life by an Creator. For example Fashion Brand XYZ designing and producing Fashion Item 123. This protocol and an implementation thereof probably only makes sense for items of higher value, though the protocol is laid out to be as generic as possible and can work with any item, independently from its value.
This protocol can work with any item wherein a NFC tag can be fully integrated and be readable with an external device. The removal of an NFC tag should require force and result in visible damage to the item, such that tampering is recognizable.

### Token / NFT
Once a physical Item has passed through the protocol, a tokenized version is created. It is now fully representable by this token. The intention of the token is to be traded on the open market. It could even be used as a collateral for borrowing/lending applications if enough liquidity exists.

### Creator / Originator / Author / Designer / Inventor / Manufacturer
Any physical item with integrity requirements has been thoughtfully designed by an creator. It can originate from an artist, company or just any person. The creator kicks of the lifespan of an item once he decides to produce it and bring his idea or invention to life. It is in his responsibility to actively decide whether or not the item is intended to become tokenized on the blockchain and thereby requires the item to walk through the different stages of the protocol in conjunction with the creator and user.

If he chooses to do so, he will need to responsibly implement the protocol at hand (or choose an appropriate and certified implementation at hand for his specific use-case) and ensure that the NFC chip is fully integrated into the product and becomes part of the identity. Most likely, this kind of integration and intervention into the product makes sense with newly designed items that already have the advantages and aspects of the protocol in mind. Though, it is also possibly to "upgrade" old items to support the protocol simply by finding an appropriate spot to attach the NFC chip on.

Unlike other protocols, the creator does not become the original owner of the item. Instead, he only registers the item in the smartcontract and keeps it open for the user to claim and thereby mint the first genesis NFT/Token. The creator could of course also claim the item himself, though this is not necessarily the intention of this protocol. Instead, once the item has been registered, gaining the ownership of the item is intentionally not based on the key pair of the creator. As described in section XXX, the user can follow a simple two factor process that does not require the creator to access his key pair anymore after he has handed out the claiming code.

This allows for a more trustless environment when reselling items in for example stores, etc. where the security of the operations might not be on par with the centralistic key management of the creator. Instead, he can freely produce his items, hand them out to resellers and stores together with the claiming codes, without providing access and the necessitiy for his key pair to be interacted with. This requires a lower level of trust in the merchants.


### User / Owner
Users of the protocol can verify, claim and transfer items between each other. Once he claims a item and comes in the physical posession of it, he also becomes an owner.
He is an independent party from the creator and is interested in gaining ownership of a physical item or the corresponding token.

### DAO / Notes about Trust Worthy List of Creators
(Removed as a role for now)

### Distributed Ledger (Smart Contract Platform)
This protocol is supposed to be implemented on a distributed ledger, since it is in the intention of the authors that ownwership rights are not managed in centralistic databases. Noone should be able to alter or manipulate your belongings -- not even the state. The idea of the protocol is to become the template for indenpendent hyper structures on several distributed ledgers. Thus, the protocol is supposed to be implemented as a smartcontract and the intention is to be smart contract platform agnostic.

## Protocol Flow
The protocol, in abstract, follows the following steps:

0. The creator registers the product with the smart contract
1. An out-of-band transaction between the creator and the user takes place
2. The creator transmits the claim code to the user
3. The user verifies the authenticity of the item in conjunction with the ledger
4. The user request a proof of physical possession from the item
5. Together with the claim code and the proof of physical possession, the user requests to claim the item at the ledger

(diagram)

## Interoperability
While other protocols follows very proprietary and non-accessible approaches, the goal for this specification is to outlay a foundation of interoperability which is distributed ledger and smart contract platform agnostic. This protocol shall serve as a template for future implementations and can be extended upon by the community. Therefor, some of the descriptions are also generic and are up to the implementor to define in more technical details depending on the platform he is using. Nevertheless, the principles and protocol steps should always remain at the core.

## Notional conventions

# Tag/Object registration

## Tag types

## Tag requirements
Note that the assumption is that the tag is integrated fully into the product, while still being readable via NFC.

## Tag identifier

## Object data

## Tag authentication

## Tag alternatives

# Protocol/Smartcontract endpoints

## Distributed Ledger agnosticisim

## Migration strategies

## Query identifier

## Claim object

The claiming-protocol intends to convey the ownership rights of an object, and its representative on the blockchain, from the manufacturer to a user. This process is one of the most critical parts of the whole system as it has to considerate practical aspects (like store purchases) on the one hand, but on the other hand also has high security demands due to possibly severe implications for participating member e.g. when transferring luxury goods. The key idea behind this protocol is to utilize cryptographically secure hash functions together with unforgeable digital signatures to build a system which allows for a two-factor authorization consisting of a knowledge- and an ownership aspect.

In short, to claim an object, the user has to prove:

(1) Ownership of the object, utilizing the object's capability to produce signatures
(2) Knowledge of a claiming code, issued to the user during the purchase phase

At this point in time, the object was already registered on the blockchain. During the aforementioned step, the object's identity *pk_o* was associated with the hash value of the claiming code *c_hash = Hash(claim_code)*. The *claim_code* however is a secret only known to the manufacturer. 

The process of transferring the object from the manufacturer to the user know works as follows:

(1) During the purchase, the *claim_code* is handed over to the user (e.g. on the receipt)
(2) The user now makes use of the object's signing features to create a proof-of-possession *u_pop*, which is a signature over the *claim code* concatenated with the user's public key *pk_u*, created with the secret key of the object *sk_o*
(3) In order to create a binding between user and object, *u_pop* is signed by the user using her private key *sk_u* resulting in a signature *o_claim*
(4) *claim_code*, *o_claim* and *u_pop* are then transferred to the ledger

In order to verify the user's access to the object and knowledge of the claiming code, the ledger now checks that:

(1) The *claim_code* is the preimage of the *c_hash*
(2) *u_pop* can be verified with the public key of the object *pk_o*
(3) *o_claim* can be verified with the public key of the user *pk_u*

## Transfer ownership

Once an object has been claimed, its possession rights can be further transferred to another user. This covers the case when the associated real world counterpart is given away or sold. The goal is to keep this process as simple as possible and to minimize the interaction between owner and receiver. In order to transfer an object, the owner needs:

(1) Possession of the private key *sk_ow*, which belongs to the public key *pk_ow* to which the object is registered
(2) Knowledge of the public key *pk_re* of the receiver

If those requirements are met, the owner can initiate a transfer without any further input of the receiver. This means that the receiver is not required to accept, but is also not able to deny, the object to be transferred. The owner issues a signed transfer request (specification needed) to the ledger which verifies whether the signature is valid under *pk_ow* and in case of success the new owner of the object is *pk_re*.

# Claiming ownership

# Transfering ownership

# Verifying ownership

## Additional metadata

# Extensibility

# Security Considerations

## (Mathematical proof)

# Privacy considerations

TODO Security

--- back

# References

# Appendix

## Syntax

## Object examples

## Acknowledgements
