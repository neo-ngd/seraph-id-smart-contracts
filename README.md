<p align="center">
<img
    src="https://github.com/swisscom-blockchain/seraph-id-landing-page/blob/master/assets/img/logo-dark.png"
    width="450px">
</p>
<h1></h1>
<p align="center">
  Seraph ID Smart Contract Templates.
</p>

<p align="center">      
  <a href="https://github.com/swisscom-blockchain/seraph-id-smart-contracts/blob/master/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-blue.svg?color=green">
  </a>
</p>

# Overview

This repository contains two smart contract templates for the SeraphID Self-Sovereign identity framework:

* Issuer (Dynamic on-chain claim registry)
* RootOfTrust (Enabling hierarchical trust topologies)

Visit the [Seraph ID](http://www.seraphid.io/) official web page to learn more about self-sovereign identity!

# Smart Contract Interface

## Issuer

```c#

string Name();
string DID();
string PublicKey(); // The public key used to sign claims
Result GetSchemaDetails(string schemaName); // Returns all attributes attached to a schema
Result RegisterSchema(string schemaName, bool revokable, params string[] attributes); // Registers a new schema and defines revokability
Result InjectClaim(string claimID); // Injects a claim to allow for revokability
Result RevokeClaim(string claimID); // Revokes a claim
Result IsValidClaim(string claimID); // Returns a claims revocation status

```

## Root Of Trust

```c#

string Name();
string DID();
Result IsTrusted(string issuerDID, string schemaName); // Checks if a did-schema pair is trusted
Result RegisterIssuer(string issuerDID, string schemaName); // Adds a trusted did-schema pair
Result DeactivateIssuer(string issuerDID, string schemaName); // Removes a did-schema pair
```

## Return Types

All smart contract calls (except for static information like name, DID, PublicKey) will return a `Result` object with the following structure:

```json
[
    {"type": "integer", "value": "<SUCCESSSTATUS>"},
    {"type": "<variable>", "value": "<variable>"}
]
```

If `<SUCCESSSTATUS>` is 0, an error has occured in the smart contract and the error reason will be listed as the value in the second object. The type of `<variable>` depends on the function being called.

# Deploying

Deploying the smart contract is a prerequisite to issue claims using the [Seraph ID SDK](https://github.com/swisscom-blockchain/seraph-id-sdk) and can be done using neo-cli or neo-gui. Make sure to note down the resulting scripthash as this will be used in the Seraph ID SDK.

## neo-cli

*Make sure your wallet is open and contains enough GAS to pay for the smart contract creation.*
```
neo> open wallet path\to\mywallet
neo> deploy Path\to\contract\seraph-id-issuer.avm 0710 10 true false false SeraphIssuer 2 Name Email Description
```

# Contributing



## Compiling

In order to compile the smart contracts into a avm file, the [Neon compiler](https://github.com/neo-project/neo-compiler) needs to be available in the PATH of your user. 

*Note: In order to build the smart contract the neon compiler needs to be run with the --compatibility flag. We recommend either building the compiler from source and changing the compatibility flag to always be on or running the neon compiler from the command line*

# References
- Seraph ID official page: http://seraphid.io
- Seraph ID demo application on [GitHub](https://github.com/swisscom-blockchain/seraph-id-demo)
- Seraph ID SDK [GitHub](https://github.com/swisscom-blockchain/seraph-id-sdk)

# License

- Open-source [MIT](https://github.com/swisscom-blockchain/seraph-id-smart-contracts/blob/master/LICENSE).
