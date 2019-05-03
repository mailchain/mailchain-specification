# Mailchain Requirements
The following requirements set out how Mailchain can be implemented on top of a blockchain (See Appendix 1 - Ethereum Implementation for a sample implementation).

## Requirements Notation
This document occasionally uses terms that appear in capital letters. When the terms “MUST”, “SHOULD”, “RECOMMENDED”, “MUST NOT”, “SHOULD NOT”, and “MAY” appear capitalised, they are being used to indicate particular requirements of this specification. A discussion of the meanings of these terms appears in [RFC2119](https://tools.ietf.org/html/rfc2119).

### Definitions for the purpose of these requirements
| Term | Definition (in the context of mailchain) |
| - | - |
Centralized resource: | A single entity or group of entities could be said to have control of the resource. Responsibility for the integrity or availability or the resource falls on entity or entities.
Decentralized resource: | No single entity or group of entities could be said to have control of the resource. Responsibility for the integrity or availability or the resource falls on the participants in the decentralized system according to the set of rules that govern the system.

## Message Storage
### General
Messages SHOULD be stored ‘off-chain’. This minimises the volume of data stored on the blockchain.

### Permissions
The sender MUST have permissions to write the encrypted message.

The recipient MUST have permissions to read the encrypted message.

Access to the storage medium MAY be limited through access controls to particular public address or account.

### Availability
A message SHOULD be available for a reasonable duration for the recipient to read, save, take action.

The duration a message is stored MAY vary. A time-to-live (TTL) SHOULD be specified.

### Location
A sender MAY choose the storage location for a message. This permits the sender to select the storage most suitable for the use case.

A recipient MAY indicate a preference for a storage location of messages. For example a centralised object store that is under the control of the recipient or a trusted organization.

### Immutability
It MUST NOT be possible for anyone to overwrite or change an encrypted message.

It MAY be possible for a recipient to delete an encrypted message.

It SHOULD NOT be possible for anyone except the recipient to delete an encrypted message.

### Encryption
A message MUST be encrypted with a recipient public key when stored.

A message MUST be encrypted with a recipient public key when transmitted.

A message MUST specify the encryption method.

### Durability
Messages SHOULD not be lost unintentionally.

Messages SHOULD not be discarded until the TTL has expired.

### Naming
A message filename MUST be (probabilistically) unique within the address space. This is to prevent filename collisions.

A message filename MAY include a hash of the encrypted message. This can be used to check the integrity of the message.

A message filename SHOULD include the message-id field from the message.

### Hashing
The recipient SHOULD be able to check the integrity of the encrypted message before decrypting. This enables the recipient to ignore messages that have been tampered with.

The recipient SHOULD be able to check the integrity of the decrypted message after decrypting. This enables a way to verify the contents of an original message, for example in the event a dispute arises.

Integrity hashes SHOULD be encrypted when stored on-chain. This reduces the risk of inference of a message.

## Message Resource Locator (MRL)
The MRL MUST follow the [RFC1738 URL scheme](https://tools.ietf.org/html/rfc1738).

The MRL MUST be encrypted with a recipient public key when included in a transaction.

The recipient MUST be able to decrypt the MRL using the recipient private key.

The recipient MUST be able to retrieve messages using the MRL.

The protocol used for accessing the storage SHOULD be indicated in the MRL. For example, `ipfs:` or `https:`.

## Mailchain Addressing Format
Addressing SHOULD follow the standard mailchain format.

For example:

`recipient_public_address`@`network`.`protocol`, where:

* `recipient_public_address` SHOULD be a public address for the recipient.
* `@` MUST be the delimiter to separate address from protocol and network details.
* `network`, an optional parameter MAY be included to specify the network the transaction is broadcast to, for example a testnet or a mainnet.
* `protocol` SHOULD specify the blockchain protocol for the message, for example, bitcoin or ethereum.
* `.` (dot) MUST be the delimiter to separate the protocol from network details.

The recipient public address MUST follow the addressing specification for blockchain protocol that the message is intended.

## Private Keys
Private keys MUST be protected by a passphrase when stored.

Users MUST be able to add a private key (to be able decrypt messages).
The application SHOULD determine public keys when provided a private key.

To carry out arbitrary actions, a user MAY NOT need to enter their passphrase. An example of an arbitrary action is using GAS to send a message.

To carry out significant actions, a user SHOULD enter their passphrase. An example of an significant action is sending Eth attached to a message.

## Message Fees
The cost of sending a message SHOULD be paid by the sender of the message, but the cost of sending a message also MAY be paid by the recipient or another party.

The cost of storing a message SHOULD be paid by the sender of the message, but the cost of storing a message also MAY be paid by the recipient or another party. Examples of this may be for longer term storage or a particular storage medium requested by the recipient.

## Message Format
A message MUST contain the following fields:

| Field | Description
| - | -
Headers: | The message headers

A message SHOULD contain the following fields:

| Field | Description
| - | -
Subject: | The message subject
Body: | The message body

A message MUST have the following header fields:

| Field | Description
| - | -
To: | The recipient public address
From: | The sender public address
Message-id: | A unique message id
Date: | The [RFC1123](https://tools.ietf.org/html/rfc1123) date format
Content-Type: | As per [RFC6532](https://tools.ietf.org/html/rfc6532) content type for the contents of the 	message.
Content-Transfer-Encoding: | How the message body SHOULD encoded

A message SHOULD have the following header fields:

| Field | Description
| - | -
Subject: | The message subject

A message MAY contain the following header fields:

| Field | Description
| - | -
Reply-To: | The public address responses should be sent to
Reply-To-Public-Key: | The public key that should be used to encrypt a reply

A message body MUST be included after the headers.

A message body MUST follow the content-type specified in Content-Type header.

A message body MUST be encoded with the content-transfer-encoding specified in Content-Transfer-Encoding header.

A message body MAY be empty.

## Transmitting a message
A message location SHOULD be transmitted in a transaction to a recipient address.

The transaction value in a message transaction MAY contain a non-zero value.

The transaction MUST be compatible with the specification of the blockchain that messages are being sent on.

## Receiving a message
A recipient SHOULD be able to retrieve all message transactions from an address transaction history.

A recipient MUST be able to verify the message was sent by the public address claiming to be the sender.

Encrypted messages that do not match the encrypted or unencrypted message hash SHOULD be discarded.

A recipient MUST be able to decrypt the message location.

A recipient MUST be able to decrypt the message.

A recipient MUST be able to verify the message has not changed since being sent.

## Network Support
A blockchain protocol MUST have the ability to send data in a transaction.

A network MUST provide the transaction history for the recipient address.