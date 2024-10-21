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
- Section 4: References