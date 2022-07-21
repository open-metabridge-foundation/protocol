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

TODO Introduction

## Roles

## Protocol Flow

## Interoperability

## Notional conventions

# Tag/Object registration

## Tag types

## Tag requirements

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
