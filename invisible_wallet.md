# Invisible Wallets on Telegram

## Introduction

Invisible wallets allow users to send transactions from a Web3 address while using Web2 credentials, without publicly linking the two
identities.

Most Web2 credentials, such as [OAuth credentials](https://datatracker.ietf.org/doc/html/rfc6749), are used by major providers like
Google, Apple, and Microsoft. There are existing solutions for creating invisible wallets using these credentials. However, Telegram
uses a unique authentication method based on HMAC256 cryptography, which requires a different solution.

In this document, we will first explain the existing solution for OAuth providers. Then, we will discuss several approaches to solving
the challenges with Telegram's authentication. Although we have not yet developed a complete solution, we hope this guide will help
others find one.

The following sections are organized as follows:

- Section 2: OIDC Solution
- Section 3: Telegram Auth Mechanism and Its Challenges

## OIDC Solution

When building invisible wallets for OIDC-compatible authentication providers like Google or Apple, the general flow is as
follows [^1] [^2]:

![invisible_wallets_oidc.png](attachments/invisible_wallets_oidc.png)

1. The user generates an ephemeral wallet, which will later interact with the blockchain. Upon authenticating with an OIDC provider
   (e.g., Google), the user requests the provider to sign a JWT token that includes the user's ephemeral public key. This JWT is signed
   using the
   provider's private key, generating a signature based on the RS256 algorithm.
2. The user information, the ephemeral public key, and the provider's signature are passed into a Zero-Knowledge circuit, along with
   the provider's public key (embedded inside the circuit), to verify the authenticity of the signature without revealing sensitive
   information.
3. If the signature is valid, the smart contract links the ephemeral public key to the user's identity. This enables the user to
   seamlessly interact with the blockchain using the ephemeral wallet without the need for traditional private keys.

[^1]: [zkLogin](https://docs.sui.io/concepts/cryptography/zklogin)
[^2]: [Keyless Account](https://aptos.dev/en/build/guides/aptos-keyless/introduction)
