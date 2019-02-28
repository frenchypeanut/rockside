# Tell me more about Vault features

### What is a vault ?

A Vault is a tool powered for the storing, managing and accessing secrets. In our case, Rocskside can use a vault for handling private keys.

### Why use a vault ?

The best way to protect a private keys is to store them in one place and never share them or expose them directly to the outside world. Vaults provides such features for your private keys, insuring that only people with the right access can you use but can't have it in clear.

### Which vaults are compatible with Rockside ?

Rockside is using [Hashicorp Vault](https://www.vaultproject.io/) solution. We developed an open-source plugin for Hashicorp Vault that enabled transactions signing inside it. That way your users only send unsigned transactions with their vault credentials, and they get back signed transactions.

The best way to understand and mastering Vault is by reading [the official vault documentation](https://www.vaultproject.io/docs/).

### How to configure the vault ?

Policies are not handled by the plugin or by Rockside. It is the client's responsibility to configure them and affect them to theirs users.

See [the official vault documentation](https://www.vaultproject.io/docs/concepts/policies.html).

### Which authentication provider is supported ?

We provide an javascript sdk for github authentification but you have to configure it in your vault first.
See [the official vault documentation](https://www.vaultproject.io/docs/auth/github.html).

### Process of the solution

![alt text](vault_simplified.png)
