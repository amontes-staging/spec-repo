---
eep: <to be assigned>
title: Enhanced Token
author: <a list of the author's or authors' name(s) and/or username(s), or name(s) and email(s), e.g. (use with the parentheses or triangular brackets): FirstName LastName (@GitHubUsername), FirstName LastName <foo@bar.com>, FirstName (@GitHubUsername) and GitHubUsername (@GitHubUsername)>
discussions-to: <URL>
status: Draft
type: <Standards Track (Core, Networking, Interface)  | RFC | Meta>
category (*only required for Standard Track): <Core | Networking | Interface>
created: <date created on, in ISO 8601 (yyyy-mm-dd) format>
requires (*optional): <EEP number(s)>
replaces (*optional): <EEP number(s)>
---

<!--You can leave these HTML comments in your merged EEP and delete the visible duplicate text guides, they will not appear and may be helpful to refer to if you edit it again. This is the suggested template for new EEPs. Note that an EEP number will be assigned by an editor. When opening a pull request to submit your EEP, please use an abbreviated title in the filename, `eep-draft_title_abbrev.md`. The title should be 44 characters or less.-->

## Simple Summary
<!--"If you can't explain it simply, you don't understand it well enough." Provide a simplified and layman-accessible explanation of the EEP.-->

## Abstract
<!--A short (~200 word) description of the technical issue being addressed.-->

subaccounts
extended asset
notifications
a memo replacement?
cover RAM charging issues for subaccounts?

This proposal does not recommend any particular table structures; we expect to cover balance query issues in a future EEP.

## Motivation
<!--The motivation is critical for EEPs that want to change the EOSIO protocol. It should clearly explain why the existing protocol specification is inadequate to address the problem that the eep solves. EEP submissions without sufficient motivation may be rejected outright.-->

## Specification
<!--The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations for any of the current EOSIO platforms.-->

```c++
using account = std::variant<eosio::name, eosio::subaccount>;

void create(eosio::name issuer, eosio::asset maximum_supply);                       notifies
void create2(account issuer, eosio::extended_asset maximum_supply);                 extended? some other way to init foreign?

void issue(eosio::name to, eosio::asset quantity, std::string memo);                to==issuer
void issue2(eosio::extended_asset quantity, std::string memo);

void retire(eosio::asset quantity, std::string memo);
void retire2(eosio::extended_asset quantity, std::string memo);

void transfer(eosio::name from, eosio::name to, eosio::asset quantity, std::string memo);       is_account
void transfer2(account from, account to, eosio::extended_asset quantity, std::string memo);

void open(eosio::name owner, eosio::symbol symbol, eosio::name ram_payer);                      should probably check is_account
void open2(account owner, extended_symbol symbol, eosio::name ram_payer);                       require owner's auth if subaccount, else is_account; prevents accidental token burn.

void close(eosio::name owner, eosio::symbol symbol);
void close2(account owner, eosio::extended_symbol symbol);
```

## Rationale
<!--The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work, e.g. how the feature is supported in other languages. The rationale may also provide evidence of consensus within the community, and should discuss important objections or concerns raised during discussion.-->

## Backwards Compatibility
<!--All EEPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their severity. The EEP must explain how the author proposes to deal with these incompatibilities. EEP submissions without a sufficient backwards compatibility treatise may be rejected outright.-->

## Test Cases
<!--Test cases for an implementation are mandatory for EEPs that are affecting consensus changes. Other EEPs can choose to include links to test cases if applicable.-->

## Implementation
<!--The implementations must be completed before any EEP is given status "Final", but it need not be completed before the EEP is accepted. While there is merit to the approach of reaching consensus on the specification and rationale before writing code, the principle of "rough consensus and running code" is still useful when it comes to resolving many discussions of API details.-->

## Copyright