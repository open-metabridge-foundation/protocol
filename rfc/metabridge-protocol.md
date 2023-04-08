---
title: "MetaBridge Protocol (MBP)"
abbrev: "MBP"
category: exp

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
  github: "open-metabridge-foundation/protocol"
  latest: "https://open-metabridge-foundation.github.io/open-metabridge-foundation/protocol/metabridge-protocol.html"

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

The MetaBridge Protocol 1.0 is an extension of the [ERC-721: Non-Fungible Token Standard](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/) which was originally introduced to Ethereum with [EIP-721](https://eips.ethereum.org/EIPS/eip-721).  The protocol offers a hard cryptographic binding of physical assets to NFTs, as well as independent claiming of those assets. This is made possible by the introduction of a creator role, which enables the transmission of a claiming code to the user.

The protocol's core functionality involves binding a physical anchor to an NFT and using a claiming code to establish ownership. Additionally, the specification outlines important security and privacy considerations for using the MetaBridge Protocol.


--- middle

# Status
This document is fully work in progress.

# Introduction
The MetaBridge Protocol extends the ERC-721 Non-Fungible Token standard to enable the cryptographic binding of physical assets to their digital counterparts. Conversely, physical assets can also be represented on a distributed ledger by minting a connected token.

The protocol defines the core functionalities of registering and claiming the digital ownership of a physical item. It also includes specifications for physical item verification and the management of physical item creators in the ecosystem.

The protocol aims to merge physical and digital worlds by creating eternal references in the metaverse. This ambitious project follows the interconnected metaverse principles and enables the creation of digital twins or totality. While proprietary and closed-source approaches exist, the MetaBridge Protocol is open source and agnostic, providing a common standardized foundation that can be extended collaboratively.

The protocol prioritizes security and privacy, with cryptographic primitives that can be audited publicly. By fostering an inclusive ecosystem and maintaining a non-profit approach, the MetaBridge Protocol aims to establish long-term trust in the protocols and their implementations.

The name "MetaBridge" is a combination of two parts: "Meta" and "Bridge".

The "Meta" part comes from the concept of the "metaverse", which refers to a collective virtual shared space that is created by the convergence of physical and virtual reality. The metaverse is often associated with virtual reality, gaming, and other online experiences.

The "Bridge" part refers to the protocol's ability to link physical assets to their digital counterparts, essentially bridging the gap between the physical and digital worlds. This ability to connect the physical and digital worlds is a key feature of the MetaBridge protocol, and is reflected in its name.

## Roles
The MetaBridge protocol involves several participants in its communication flows.

### Item
The physical Item is at the core of the protocol. A Creator brings an Item to life, such as a fashion brand designing and producing a fashion Item. The value of the protocol implementation increases linearly with the value of the physical Item, although the protocol is designed to be as generic as possible and can work with any Item, regardless of its value.
This protocol can work with any Item that can integrate an NFC tag and is readable with an external device. The NFC tag removal should require force and result in visible damage to the item to detect any tampering.

### ancNFT
After a physical Item has gone through the MetaBridge Protocol, it is transformed into a tokenized version known as an anchored NFT (ancNFT). The ancNFT is intended to be tradable on the open market, while also potentially serving as collateral for borrowing and lending applications in decentralized finance (DeFi) platforms, provided that there is enough liquidity available.

### Creator
The Creator plays a vital role in the MetaBridge Protocol as they are responsible for bringing the physical Item to life and deciding whether it should be tokenized on the blockchain in the form of a ancNFT. The Creator can be a designer, artist, company, or any person who creates Items with integrity requirements. It is their responsibility to implement the MetaBridge Protocol, or choose a certified implementation, and ensure that the listed Tag requirements are followed.

Implementing the MetaBridge Protocol during the design phase of a new Item is ideal, but it is also possible to "upgrade" old Items to support the protocol by attaching an NFC chip in an appropriate spot. Unlike other protocols, the Creator does not become the original owner of the item. Instead, they register the item in the smart contract and keep it open for the User to claim and mint the first genesis ancNFT. The Creator could also claim the item, but this is not necessarily the intention of the MetaBridge Protocol. Once the item has been registered, gaining ownership is intentionally not based on the key pair of the Creator. The User can follow a simple two-factor process described in section XXX that does not require the Creator to access their key pair after they have handed out the claiming code.
<!-- How does this compare to whitelist minting? -->

This approach creates a more trustless environment for reselling items in stores and other locations where the security of operations may not be as secure as centralized key management. By providing claiming codes instead of direct access to the key pair, the creator can freely produce and distribute items without the need for his key pair to be accessed. This reduces the level of trust required in merchants, as they are only able to claim items for which they have been provided with the claiming codes. However, there is still a loophole as resellers and stores may use the claiming codes to claim the items for themselves, limited only to those for which the Creator has provided the codes. Therefore, the Creator still needs to be able to trust the merchant not to misuse the claiming codes.

### User
Users of the protocol are able to verify, claim, and transfer ownership of items between each other. Once a user claims an item and takes physical possession of it, they become the owner. They are an independent party from the Creator and are interested in gaining ownership of either the physical item or its corresponding token.

### Distributed Ledger (Smart Contract Platform)
The MetaBridge protocol is designed to be implemented on a distributed ledger to ensure that ownership rights are not managed in centralized databases. The goal is to prevent anyone, including the state, from altering or manipulating a user's belongings. The protocol is intended to serve as a template for independent hyperstructures on multiple distributed ledgers, and as such, it is designed to be implemented as a smart contract platform agnostic.

## Protocol Flow
The MetaBridge Protocol can be broken down into the following steps:

0. The Creator registers the physical Item with the smart contract.
1. An out-of-band transaction occurs between the Creator and the User.
2. The Creator provides the User with a unique Claim Code associated with the physical Item.
3. The User verifies the authenticity of the physical Item through the blockchain ledger.
4. The User requests a proof of physical possession for the Item.
5. The User submits the Claim Code and proof of physical possession to the ledger to claim ownership of the corresponding anchored NFT (ancNFT).

<!-- (diagram) TODO -->

## Interoperability
The main objective of this specification is to establish a foundation of interoperability that is not limited to any particular distributed ledger or smart contract platform, unlike other protocols that follow a closed and non-accessible approach. This protocol is designed to act as a model for future implementations and can be expanded upon by the community. As a result, certain aspects of the description are general and are open to interpretation by the implementor based on the technical details of the platform they are using. However, the underlying principles and protocol steps should always remain consistent.


# NFC-Tag registration

## NFC-Tag requirements

To link physical Items to the digital world, each Item is equipped with an NFC-Tag. This tag contains information that unambiguously identifies the product and provides the core functionality for digital transfer. The following requirements must be fulfilled:

### General Requirements

- Must be capable of securely storing an asymmetric key pair to prevent secret extraction.
- Must be able to produce digital signatures of arbitrary messages on request.
- Can be capable of storing certificates.

These requirements ensure that the tag is capable of securely storing and providing access to the necessary cryptographic keys and signatures required for the protocol to function effectively. While NFC-Tags are currently the preferred technology for this purpose, the protocol is open to the possibility of using other suitable technologies in the future.

### Hardware Requirements
The NFC-Tag that connects the physical Item with the digital world must fulfill the following hardware requirements:

- It must have NFC capabilities, including the antenna, with a size that allows it to be scanned by a mobile phone.
- It must be highly durable and able to withstand washing, bending, heat, and other potential hazards.
- It may have tamper detection capabilities.

### Additional Assumptions
In addition to the hardware requirements, the following assumptions are also made:
- The tag is fully integrated into the Item.
- The tag is not removable without force, which results in visible damage to either the Item or the tag, making any tampering immediately recognizable.

## NFC-Tag identifier

A crucial requirement for seamless tracking of tangible products in the digital world is the tag's ability to store a cryptographic key pair consisting of a private and public key. During production, the key pair is associated with the tag, and the public key uniquely identifies the tag.

### Lookup Metadata

During product registration, the Creator reads the public key from the tag and stores it as part of a certificate along with other metadata on the ledger. The User can later retrieve this data by querying the ledger using the public key as an identifier.

### Verify Proof-of-Possession

To claim ownership of an Item digitally, a User must provide two components: a Claim Code obtained through purchase and a Proof-of-Possession (PoP) of the physical Item. The PoP is a signature generated by the Item and serves as evidence of physical possession. When the User sends the Claim Code and PoP to the ledger, the public key of the Item is used to verify the PoP's authenticity.


<!-- ## Tag authentication
(How to authenticate the tag and when it's recommended to do so) TODO -->


# Protocol/Smartcontract endpoints
This section outlines the minimum interfaces that a smart contract must implement to comply with the protocol specification.

## Query identifier

~~~~~~~~
@notice Retrieve item information
@param pk_hash_item Compact representation of the item's public key
@return Data associated with the item
function queryItem(pk_hash_item) returns (ItemMetadata);
~~~~~~~~

This function enables the retrieval of item information stored on the ledger. It requires the public key of the item in a compact form (i.e., hashed) and returns a struct containing the metadata associated with the item. The function uses the hash of the public key to look up the metadata that was registered with the item during the registration process.

## Register item
The following function describes the process of registering a new item on the ledger, ensuring that it is properly authenticated and authorized.

~~~~~~~~
@notice Register an item on the ledger
@param pk_item The public key of the item 
@param c_hash The hash of the claim code
@param i_reg A signature of claim_code and c_hash, signed by the creator
@param pk_creator The public key of the creator
@return A boolean indicating whether the registration was successful
function registerItem(pk_item, c_hash, i_reg, pk_creator);
~~~~~~~~

The function takes in the public key of the item, the hash of the claim code, a signature of the claim code and c_hash signed by the creator, and the public key of the creator. Upon execution, the function first checks whether an item with the same public key has already been registered. If so, it returns false. If not, the function proceeds to verify whether the creator is authorized to register items by fetching a list from an external service or requesting it from another smart contract. Next, the function verifies whether the i_reg signature is valid, ensuring that an authorized creator submitted the item for registration. If any of the previous checks fail, the function returns false. Otherwise, the function returns true, indicating a successful registration, and the item is ready to be claimed.

## Claim item
This function enables users to claim ownership of a registered item.

~~~~~~~~
@notice Claim ownership of a registered item.
@param pk_item The public key of the item.
@param pk_user The public key of the user.
@param claim_code The secret required to claim the item.
@param u_pop A signature of claim_code and public key of the user, signed by the item.
@param i_claim A signature of u_pop, signed by the user.
@return A boolean indicating whether the claiming process was successful.
function claimItem(pk_item, pk_user, claim_code, u_pop, i_claim) returns (bool) {
    // Check if the c_hash registered with the item matches the provided claim_code.
    if (c_hash(pk_item) != hash(claim_code)) {
        return false;
    }
    
    // Validate that u_pop is a valid signature of the claim_code and public key of the user, signed by the item.
    if (!verifySignature(u_pop, claim_code, pk_user, pk_item)) {
        return false;
    }
    
    // Check if the item is claimable.
    if (!isClaimable(pk_item)) {
        return false;
    }
    
    // Validate that i_claim is a valid signature of u_pop under the public key of the user.
    if (!verifySignature(i_claim, u_pop, pk_user)) {
        return false;
    }
    
    // Give ownership of the item to the user.
    transferOwnership(pk_item, pk_user);
    
    return true;
};
~~~~~~~~

It requires the public keys of both the item and the user, along with the claim_code, u_pop (a signature of the claim_code and the public key of the user, signed by the item), and i_claim (a signature of u_pop, created by the user). Upon completion, it returns a boolean value indicating whether the claiming process was successful or not.

To verify whether a claim can be made, the function first checks whether the c_hash that was registered with the item corresponds to the hash of the claim_code. It then validates whether u_pop is a valid signature of the claim_code concatenated with the user's public key, as signed by the item. The function must also confirm that the item is claimable - meaning that it is correctly registered and has not been previously claimed. Finally, i_claim must be validated as a signature of u_pop under the public key of the user.

If all checks are successful, the ownership of the item is transferred to the user, and the function returns true. Otherwise, it returns false.

## Transfer item

~~~~~~~~
@notice Allows the owner of an item to transfer its ownership to another user.
@param pk_item The public key of the item.
@param pk_user The public key of the receiving user.
@param trans_req The transfer request signed by the owner.
@return True if the transfer process was successful, false otherwise.
function transferItem(pk_item, pk_user, trans_req);
~~~~~~~~

This function allows the current owner of an item to transfer its ownership to another user. It takes pk_user and pk_item as inputs, which respectively represent the public key of the receiving user and the item's public key, serving as their unique identifiers. The third parameter, trans_req, is a signature created by the current owner of the item, over the receiving user's public key concatenated with the public key of the item and a unique counter. This counter is the number of previous transfers of this item, increased by one, and can be obtained from the smart contract. It ensures that only valid transfers from the current owner are recognized by the smart contract, effectively preventing replay attacks.

To transfer ownership, the smart contract checks whether the owner submitting the transfer request is the actual owner of the item. If the transfer request is valid, meaning that the counter is set as the old counter plus one, the transfer is considered successful, and ownership is transferred to the receiving user. If any of the checks fail, the transfer process is aborted, and the function returns a flag indicating failure.

# Claiming ownership

The claiming-protocol is a crucial component of the system that aims to transfer ownership rights of an item and its representative on the blockchain from the creator to a user. This process requires a balance between practical considerations, such as store purchases, and high-security demands, especially when transferring luxury goods, to ensure the safety of all participating members. To achieve this, the protocol uses cryptographically secure hash functions and unforgeable digital signatures to enable a two-factor authorization system that includes knowledge- and ownership-factors.

To claim ownership of an item, the user needs to demonstrate two things: (1) ownership of the item itself, which is done by using the item's signature capabilities, and (2) knowledge of a claiming code issued during the purchase phase.
By this stage, the item has already been registered on the blockchain, and its identity *pk_i* has been linked to the hash value of the claiming code *c_hash = Hash(claim_code)*. However, the *claim_code* itself is a secret known only to the creator.

The process of claiming ownership of the item involves the following steps:

0. During the out-of-band trade, the user is given the *claim_code*, which is a secret known only to the creator.
1. The user uses the items's signing features to create a proof-of-possession, *u_pop*, which is a signature over the *claim_code* concatenated with the user's public key *pk_u*. This is created using the secret key of the item *sk_i*.
2. To create a binding between the user and the item, *u_pop* is signed by the user using the private key *sk_u*. This results in a signature, *i_claim*.
3. The *claim_code*, *i_claim*, and *u_pop* are then transferred to the ledger.

To verify the user's access to claim the item and knowledge of the claiming code, the ledger performs the following checks:

0. The *claim_code* is the correct preimage of the *c_hash*.
1. The proof-of-possession *u_pop* can be verified using the item's public key *pk_i*.
2. The signature *i_claim* can be verified using the user's public key *pk_u*.

# Transfering ownership

After an item has been claimed, it can be further transferred to another user if the physical item is given away or sold. To keep this process simple and minimize the interaction between the current owner and the receiver, the following requirements need to be met:

0. Possession of the private key *sk_ow*, which corresponds to the public key *pk_ow* to which the item is registered.
1. Knowledge of the public key *pk_re* of the receiver.

If the above requirements are met, the owner can initiate the transfer without requiring any input from the receiver. This means that the receiver is not required to accept the transfer, but also cannot deny it. The owner sends a signed transfer request (the specification needs to be provided) to the ledger, which verifies the validity of the signature under *pk_ow*. If the signature is valid, the new owner of the item becomes *pk_re*.

# Verifying ownership

This protocol enables users to verify the authenticity of a product. The verification process involves different cycles depending on the availability of internet connectivity and the tag's capability to store certificates. Online verification is preferred as it provides the most up-to-date information and the highest level of security. However, offline verification can serve as a backup solution in remote locations.

To perform a *High level (online)* verification, the user should follow these steps:

0. Read the public key *pk_i* from the tag.
1. Query the ledger using *pk_i* to obtain claiming transaction artifacts.
2. Obtain a list of creators from a reliable source such as the ledger or an external web server.
3. Verify the received certificates against the list of brands.

To perform a *Medium level (offline)* verification, the user should follow these steps:

0. Read the product certificate from the tag.
1. Verify the received certificate against a previously stored list of creators.


# Security Considerations

The OMBF protocol family incorporates a number of security considerations in its design to ensure the integrity and authenticity of the objects and transactions. Some of the key security measures include:

- **Secure Signing**: All transactions are signed using cryptographic signatures, which provides integrity and non-repudiation of the transaction.
- **Public/Private Key Infrastructure**: The use of public/private key infrastructure ensures that only authorized parties are able to perform certain operations, such as claiming ownership or transferring possession.
- **Proof-of-Possession**: By requiring proof-of-possession, the protocol ensures that only the rightful owner of an object can claim ownership or transfer possession.
- **Ledger Verification**: Transactions are verified against the ledger to prevent double-spending and ensure that all transactions are valid.
- **Online/Offline Verification**: The protocol supports both online and offline verification, which enables verification in both connected and disconnected environments.
- **Secure Tag Authentication**: The protocol uses secure tag authentication to ensure that only legitimate tags can participate in the protocol.
- **Secure Key Management**: The protocol ensures secure key management practices, including the use of hardware security modules (HSMs) and key rotation policies.

Overall, the OMBF protocol family incorporates a range of security measures to protect against common attack vectors and ensure the integrity and authenticity of the transactions.

# Privacy considerations

In designing the OMBF protocol family, privacy was a key consideration in order to protect the personal data of users and prevent unauthorized tracking or monitoring. The following measures were considered to ensure privacy:

- **Data minimization**:  The protocols were created to gather only the necessary minimum data for verification and transfer processes. This reduces the amount of data available for profiling or misuse.
- **User pseudonymity**: Public keys are the only information required for verification and transfer processes, thus protecting user identity. Private keys are kept secret and not transmitted, reducing the risk of identity theft.
- **Tag pseudonymity**: Tags are designed to operate pseudonymously without the need for personal information or identity-bound identifiers, further enhancing user privacy.
- **Transparency**: Clear information is provided to users and implementers about what data is required and how it is used during verification and transfer processes. This empowers all parties to make informed decisions and retain control over their personal data.

By implementing these measures, the OMBF protocols are designed to provide users with confidence in their ability to manage their personal data and protect their privacy.

--- back

# References

# Appendix

## Syntax

## Item examples
<!-- (tangible examples of the items and communication packages) -->

## Acknowledgements
