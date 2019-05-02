# Mailchain Proposal
Version 0.0.1 - Draft
## Introduction
Mailchain enables blockchain-based email-like messaging with plain or rich text and attachment capabilities. Using blockchain protocols and decentralized storage, Mailchain delivers a simple, secure, messaging experience.

Account holders or owners of a public address often need to communicate in the context of the account or public address. Communication may relate to transactions, account actions or some type of notification.

Examples of use cases for blockchain messaging include invoicing, receipts, contacting users of a service or application developers.

The majority of blockchain protocols provide no standard way to handle messaging. Some account holders have sent messages as an encrypted or unencrypted string included in transaction data. Some applications work around the problem by asking users to link another method of contact (e.g. email address, phone number etc.) to an application. This compromises anonymity by asking users to link or reveal an identity. It also increases exposure to security risks, and relies on additional centralized services.

This proposal outlines how Mailchain gives users the ability to send and receive rich-media HTML messages between public addresses through a simple, email-like interface. All message contents and attachments are encrypted so only the intended recipient of the message can decrypt and view messages.

## Mailchain Message Lifecycle
Mailchain is a simple, secure and practical standard which can be implemented across different blockchains. It uses underlying native blockchain protocol capabilities including addressing, immutability, data transmission, and cryptography.

The basic message flow is as follows:

* A user sends a message. The message is encrypted and stored using the recipient’s public key so that only the recipient can locate and decrypt the message contents. The encrypted location of the message is sent by the sender to the recipient in the data field of a transaction.

* To read a message, a recipient uses a corresponding private key to decrypt the location of the message from the data field of a transaction and decrypt the message contents.

## Anonymity, Privacy and Encryption
Mailchain considers anonymity of senders and recipients a high priority.

The Mailchain application handles encryption and decryption of data (see *Mailchain Message Lifecycle* for further details). All data is encrypted when transmitted or stored outside of the mailchain/mailchain-web application flow.

Anyone with the recipient account’s private key can decrypt messages, so it is important to secure private keys.

The underlying blockchain protocol (e.g. ethereum, bitcoin etc.) is responsible for dictating the sender & recipient privacy model.

## What's here

There are three important files in this repository:

[mailchain_requirements](https://github.com/mailchain/mailchain-specification/blob/master/mailchain_requirements.md)

[mailchain_tenets](https://github.com/mailchain/mailchain-specification/blob/master/mailchain_tenets.md)

[mailchain_threat_model](https://github.com/mailchain/mailchain-specification/blob/master/mailchain_threat_model.md)


# Compatibility
Mailchain implements Semantic Versioning (see  [https://semver.org](https://semver.org/)  for more information).

From version 1.0.0:
* New versions should be backwards compatible
* Software must be capable of reading old versions


## License

By contributing to the Mailchain Specification repository, you agree that your contributions will be licensed under its [Apache 2.0 License](https://github.com/mailchain/mailchain-specification/blob/master/LICENSE).

