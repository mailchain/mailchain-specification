# Threat Model
Every application has some exposure to threats. In mailchain, possible threats include the following scenarios. Where possible, the application will work around or try to reduce the risks. Nonetheless, developers and users should be aware and understand known risks or limitations.

* Exhaust a user’s wallet balance through GAS usage by sending many messages.

*In order to maliciously spend a user's ETH, it could be possible to send many messages. Each message has a GAS price and eventually a user's balance would reach 0.
Because spent GAS cannot be recovered (except by the miner of a transaction), the attacker would not be likely to benefit from the attack.*
 
* Send Ether in a transaction without user authorisation [currently not possible because the tx amount is set to 0].

*In order to steal a victim's ETH, it could be possible to send a message to an attackers address with the value of the transaction set to be the victims entire balance. The transaction value is currently set to be 0.*

* Tracking/ inferring the existence of conversations between different accounts.

*Although encrypted, the message transaction is distinct. Monitoring the transaction history between two addresses may enable an adversary to infer that messages were exchanged in conversation.*

* Forward secrecy is compromised if the private key for an address becomes known by an adversary.

*If the private key is discovered and a user continues to receive messages, the attacker will be able to decrypt these messages.
This is also true for any other protocols that uses the same encryption method.
To work around this, a recipient may provide or rotate different public keys for encrypting messages*

* Backward secrecy is compromised if the private key for an address becomes known by an adversary.

*If the private key is discovered, the attacker will be able to decrypt all past messages.
This is also true for any other protocols that uses the same encryption method.
To work around this, a recipient may provide or rotate different public keys for encrypting messages*