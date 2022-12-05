---
title: "MetaBridge Protocol (MBP)"
abbrev: "MBP"
category: info

docname: draft-metabridge-dinrg-protocol-latest
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
This protocol extends upon the Non-Fungible Token (NFT) ERC-721 standard. It enables digital assets to become connected with a physical counterpart, as well as the other way around; physical assets can be immortalized on any distributed ledger that supports smart contracts by minting a cryptographically connected token.

This specification defines the core functionalities: registering and claiming the digital ownership of a physical item. It also describes the security and privacy considerations for usage.

Additionally, the protocol includes specifications on physical item verification and the management of the physical item manufactures in the context of this novel ecosystem.

From a philosophical perspective, this protocol is aiming to merge and connect items from the real (tangible and physical) world into digital universes, following the interconnected metaverse principles. Through this protocol and extensions thereof, it is possible to create eternal references in the metaverse possibly going way beyond the lifetime of the physical item. Common terms for such approaches are often referred to as digital twins or totality.
The authors are aware that this is an ambitious project, though multiple other parties are working on similar approaches which commonly are proprietary, closed source and not agnostic.
The goal with this specification is to lay out a common standardized foundation that allows to be extended upon in a collaborative approach.

<!-- TODO: MetaBridge Name explanation. -->

## Roles
The following participants are involved as part of the protocol communication flows.

### Item
The physical Item lies at the core of the protocol. An Item is brought to life by a Creator. For example Fashion Brand XYZ designing and producing Fashion Item 123. The value in the MetaBridge protocol and an implementation thereof rises linear to the value of the physical Item, though the protocol is laid out to be as generic as possible and can work with any Item, independently from its value.
This protocol can work with any Item wherein an NFC tag can be fully integrated and be readable with an external device. The removal of an NFC tag should require force and result in visible damage to the item, such that tampering is recognizable/detected.

### ancNFT / pNFT
Once a physical Item has passed through the protocol, a tokenized version is created. It is now fully representable by this alternate NFT, called a pNFT (physical NFT) or ancNFT ((crypto) anchored NFT) <!-- TODO: Choice! -->. The intention of the pNFT is to be traded on the open market. Additionally, it could be used as a collateral for borrowing/lending applications in DeFi applications, assuming enough liquidity exists.

### Creator
Any physical item with integrity requirements has been thoughtfully designed by a Creator. The Creator is synonymus for any designer, artist, company or person that creates Items. The Creator kicks of the lifespan of an Item once he decides to produce it and bring his idea or invention to life. It is in his responsibility to actively decide whether or not the Item is intended to become tokenized on the blockchain in the form of a pNFT and thereby requires the item to walk through the different stages of the MetaBridge Protocol in conjunction with the User <!-- LINK -->.

If he chooses to do so, he will need to responsibly implement the MetaBridge Protocol (or choose an appropriate and certified implementation at hand for his specific use-case) and ensure to follow the listed Tag requirements <!-- LINK -->. Most likely, this kind of integration and intervention into the product makes sense with newly designed Items that already have the advantages and aspects of the protocol in mind. Though, it is also possible to "upgrade" old Items to support the MetaBridge protocol simply by finding an appropriate spot to attach the NFC chip on.

Unlike other protocols, the creator does not become the original owner of the item. Instead, he only registers the item in the smartcontract and keeps it open for the user to claim and thereby mint the first genesis ancNFT. The creator could of course also claim the item himself, though this is not necessarily the intention of the MetaBridge protocol. Instead, once the item has been registered, gaining the ownership of the item is intentionally not based on the key pair of the Creator. As described in section XXX, the User can follow a simple two factor process that does not require the Creator to access his key pair anymore after he has handed out the claiming code.
<!-- How does this compare to whitelist minting? -->

This allows for a more trustless environment when reselling items in for example stores, etc. where the security of the operations might not be on par with the centralistic key management of the Creator. Instead, he can freely produce his items, hand them out to resellers and stores together with the claiming codes, without providing access and the necessitiy for his key pair to be interacted with. This requires a lower level of trust in the merchants.
<!-- Loophole: Resellers and stores can still just use the claiming codes to claim the Items for themselves, achieving the same goal as if they had access to the key pair of the Creator, though for limited amount of items; those who the Creator provided the claiming codes for. -->

### User
Users of the protocol can verify, claim and transfer items between each other. Once he claims a item and comes in the physical posession of it, he also becomes an owner.
He is an independent party from the creator and is interested in gaining ownership of a physical item or the corresponding token.

### Distributed Ledger (Smart Contract Platform)
This protocol is supposed to be implemented on a distributed ledger, since it is in the intention of the authors that ownwership rights are not managed in centralistic databases. Noone should be able to alter or manipulate your belongings -- not even the state. The idea of the protocol is to become the template for indenpendent hyper structures on several distributed ledgers. Thus, the protocol is supposed to be implemented as a smartcontract and the intention is to be smart contract platform agnostic.

## Protocol Flow
The protocol, in abstract, follows the following steps:

0. The Creator registers the Item with the smart contract
1. An out-of-band transaction between the Creator and the User takes place
2. The Creator transmits the Claim Code to the User
3. The User verifies the authenticity of the Item in conjunction with the ledger
4. The User request a proof of physical possession from the Item
5. Together with the Claim Code and the proof of physical possession, the User requests to claim the Item at the ledger

(diagram)

## Interoperability
While other protocols follows very proprietary and non-accessible approaches, the goal for this specification is to outlay a foundation of interoperability which is agnostic to any distributed ledger and smart contract platform. This protocol shall serve as a template for future implementations and can be extended upon by the community. Therefor, some of the descriptions are also generic and are up to the implementor to define in more technical details depending on the platform he is using. Nevertheless, the principles and protocol steps should always remain at the core.

## Notional conventions
(Typical RFC notional conventions)

# Tag/Object registration
(How to register a tag from the perspective of the creator)

## Tag requirements
(List all cryptographic and functional requirements that the tag needs in order to be operating with the protocol)
(Note that the assumption is that the tag is integrated fully into the product, while still being readable via NFC.)

In order to connect the physical Item with the digital world, every Item is augmented with an NFC-Tag (other options might be possible). The tag contains information that unambiguously identify the product and provides the core functionality for the digital transfer. The following requirements must be fulfilled:

**General Requirements**

- Capable of securely storing an asymmetric key pair
- Be able to produce digital signatures of arbitrary messages on request
- Optional: Capable of storing certificates

**Hardware Requirements**

- NFC capabilities including the antenna (with a minimum size to actually make it scannable via a mobile phone)
- High durability (washable, bendable, protected against heat, etc.)
- Optional: Tamper detection

**Additional Assumptions**

- The tag is fully integrated into the Item
- The removal of the tag should require force and result in visible damage to the Item, such that tampering is recognizable/detected.

## Tag identifier
(Introduce the public key as the unique tag identifier/DNA and what else it can be used for)

One of the key requirements that leverages a seamless tracking of the tangible product in the digital world, is the tags' capability of storing a cryptographic key pair consisting of a public and private key. The pair is associated with the tag during its production and besides its cryptographic purpose of signing and verifying messages using the private and public key respectively, the public key serves another important role, that is, it uniquely identifies the tag.

**Lookup Metadata:** In the course of the product registration, the Creator reads the public key from the tag and stores it on the ledger as part of a certificate alongside other metadata. The User, on the other side, can later retrieve this data by querying the ledger using the public key as an identifier.

**Verify Proof-of-Possession:** In order to digitally claim ownership over an Item, a User needs two components. First a Claim Code, which can be obtained with the Item purchase, and second, a Proof-of-Possession (PoP) of the physical Item. During this process, the Claim Code and PoP, which is a signature produced by the product, are sent to the ledger. The ledger later uses the public key of the Item to check the validity of the Proof-of-Possession.

## Item data (optional)
(Elaborate upon the additional information/data that can be attached to the tag on the distributed ledger)

## Tag authentication
(How to authenticate the tag and when it's recommended to do so)

## Tag alternatives (optional)
(Mention future alternatives such as crypto anchors, AI camera object identification or modern types of fabric scanners)

# Protocol/Smartcontract endpoints
(Define the fixed endpoints that every smartcontract intending to follow the protocol should have)

## Distributed Ledger agnosticisim (optional)
(Explain that this can work on any distributed ledger and it is not limited to a specific one. List the requirements that a distributed ledger should have in order to be able to run the protocol as a smartcontract, i.e. support of specific cryptographic primitives, algorithms, etc.)

## Migration strategies (optional)
(Elaborate how to upgrade/maintain the smartcontract and move inbetween ledgers)

## Query identifier
(The very first smart contract function; describe how you can query an item by it's identifier/public key and which data you expect in return)

```
/// @notice Retrieve object information
/// @param pk_hash_object A compact representation of the object's public key
/// @return Data associated with the object
function queryObject(bytes32 pk_hash_object) external view returns (object memory);
```

This function allows the retrieval of object information stored on the ledger. It requires the public key of the object within a compact form (i.e. hashed) and returns a struct containing metadata of the aforementioned. This is a straight forward function, that uses the hash of the public key to look up the metadata that was registered together with the object.

## Register object
(smart contract function; which parameters do you need to send in order to be able to register an object in your name for others to claim)

```
/// @notice Register an object on the ledger
/// @param pk_object The public key of the object 
/// @param c_hash The hash of the claim_code
/// @param o_reg A Signature of claim_code and c_hash, signed by the creator
/// @param pk_creator Public key of the creator
/// @return Indicates whether the registration was successful
function registerObject(pkey pk_object, bytes32 c_hash, sig o_reg, pkey pk_creator) external view returns (bool);
```

This function can be used to register a new object in the ecosystem. It requires the public keys of both, object and creator, together with the c_hash, which basically is the hashed claim_code and a signature over the concatenation of object public key and c_hash. It returns a bool, indicating whether the registering process was a successful. As a first step the function has to check whether there was an object already registered with the same public key, in that case function just returns false. Otherwise, it has to verify whether the creator is approved in some way, i.e. by fetching a list from an external service or requesting it from another smart-contract. Now it has to be checked whether the issued o_reg-signature is valid. This ensures that in fact an authorized creator submitted the object for registration. If any of the previous checks failed the function returns false otherwise it returns true and the object is ready to be claimed. 

## Claim object
(The second smart contract function; which parameters do you need to send in order to be able to claim this item for yourself)

```
/// @notice Claim an object for the given user
/// @param pk_object The public key of the object 
/// @param pk_user The public key of the user 
/// @param claim_code The secret required to claim the object 
/// @param u_pop A Signature of claim_code and public key of the user, signed by the object
/// @param o_claim A Signature of u_pop, signed by the user
/// @return Indicates whether the claiming process was successful
function claimObject(pkey pk_object, pkey pk_user, byte32 claim_code, sig u_pop, sig o_claim) external view returns (bool);
```

This function allows a user to claim a previously registered object. It requires the public keys of object and user, together with the secret claim_code. Additionally, to u_pop, a signature of claim_code and public key of the user, signed by the object and o_claim which is a signature of u_pop, created by the user. It returns a flag that indicates success or failure. In order to verify whether a claiming is possible, the function first checks whether c_hash, which was registered together with the object, is an actual hash of the claim_code. Next, it validates whether u_pop is a valid signature of the same claim_code, concatenated with the public key of the user created by the object. The function must also check at this point, if the object is indeed claimable, which means correctly registered and not claimed before. As a next step, o_claim has to be validated as a signature of u_pop under the public key of the user. If all checks have passed, give ownership to the user and return true otherwise return false.

## Transfer ownership
(Third smart contract function; how do you transfer your item from yourself to someone else)

# Claiming ownership

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

# Transfering ownership

Once an object has been claimed, its possession rights can be further transferred to another user. This covers the case when the associated real world counterpart is given away or sold. The goal is to keep this process as simple as possible and to minimize the interaction between owner and receiver. In order to transfer an object, the owner needs:

(1) Possession of the private key *sk_ow*, which belongs to the public key *pk_ow* to which the object is registered
(2) Knowledge of the public key *pk_re* of the receiver

If those requirements are met, the owner can initiate a transfer without any further input of the receiver. This means that the receiver is not required to accept, but is also not able to deny, the object to be transferred. The owner issues a signed transfer request (specification needed) to the ledger which verifies whether the signature is valid under *pk_ow* and in case of success the new owner of the object is *pk_re*.
# Verifying ownership
(from a protocol perspective, describe the steps necessary in order to be sure that this item belongs to x i.e. the person in front of you)

With the help of this protocol, the user is able to verify the validity of the product in hand. The specification thereby provides distinct verification cycles depending on whether there is an active internet connection available and/or the tag is able to store certificates. Inherently, the online verification process is the preferred variant due to the availability of the most recent data, providing the highest level of security. In contrast, the offline verification protocol relies on cached data and acts a backup solution for remote places.

To perform the *High level (online) verification*, the user follows the subsequent steps:

(1) Read the public key *pk_o* from the tag
(2) Query the ledger by *pk_o* in order to obtain claiming transaction artifacts
(3) Get a list of brands from a suitable source (ledger, external webserver, ...) 
(4) Verify the received certificates against the list of brands 

To perform the *Medium level (offline) verification*, the user follows the subsequent steps:

(1) Read the product certificate from the tag
(2) Verify the received certificate against a previously stored list of brands

## Additional metadata (optional)
(describe the openess for any additional data fields that can be attached to the tag during registration)

# Extensibility (optional)
(Mention that these protocols are intended to be extended upon, possibly with some ideas?)

# Security Considerations

## Assumptions

0. The cryptographic key pair on the chip is stored securely
1. The Creator and User are responsible for their own secure key management

## (Mathematical proof)

# Privacy considerations

TODO Security

--- back

# References

# Appendix

## Syntax

## Object examples
(tangible examples of the items and communication packages)

## Acknowledgements
