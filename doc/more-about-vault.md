# Tell me more about Vault features

### What is a vault ?

A Vault is a tool powered for the storing, managing and accessing secrets. In our case, Rocskside can use a vault for handling private keys.

### Why use a vault ?

The best way to protect a private key is to store it in one place and never share it or expose it directly to the outside world. Vault provides such features for your private keys. With the Rockside Ethereum Vault plug-in, we guarantee that only people with the right access can sign a transaction without having direct access with the private key.

### Which vaults are compatible with Rockside ?

You can connect an [Hashicorp Vault] (https://www.vaultproject.io/) to Rockside. We have developed an open-source plug-in for Hashicorp Vault. This plugin provide transaction signing on the Vault. In this way, your users only send unsigned transactions with their vault credentials and they retrieve the signed transactions.

The best way to understand and master Vault is to consult the official Vault documentation (https://www.vaultproject.io/docs/).

### How to configure the vault  policies?

Policies are not handled by the plugin or by Rockside. It is the client's responsibility to configure them and affect them to theirs users.

See [the official Vault documentation](https://www.vaultproject.io/docs/concepts/policies.html).

### Hashicorp Vault installation

See [the official Vault documentation](https://learn.hashicorp.com/vault/getting-started/install).

### Rockside Hashicorp Vault plugin

The purpose of this plugin is to provide the vault with a connector to the rockside engine and some features to manage Ethereum account.

####  Build and Install Rockside Ethereum Vault Plugin

For more details and install process, see the readme on the [project github](https://github.com/blockchain-studio/rockside-hashicorp-vault-plugin).

#### Connect your vault to Rockside
After installing and configuring your vault and the Rockside Ethereum Vault plugin, you can connect your vault to Rockside.

Edit **~/.rockside/engine/rockside.env** and add:

```
VAULT_HOST=<YOUR_VAULT_ADDRESS>/v1/rockside/
```

Relaunch Engine with new configuration:
```
sudo rockside engine reconfigure
```

#### Send unsigned transaction to Rockside

  You can send an unsigned transaction with Rockside in the same way as with a signed transaction. You simply need to add the vault access token at the end of your node's RPC URL.
  
  ```
https://<ENGINE_URL>/api/nodes/rpc/<NODE_TOKEN>/<VAULT_TOKEN>
```

### Features

#### create an account

```sh
vault write -f rockside/account/new
```

#### import an account

```sh
vault write -f rockside/account/import private_key="f5a200fea608820dc411bc212ff4ec76d331e6efd39ac1bf30aca066fb3c6807"
```

#### list accounts

```sh
vault list rockside/account
```

#### read an account (and get its private key)

```sh
vault read rockside/account/0x62b1d469a3ae3bb5669ea69c933bb1649ff02439
```

### Policies creation

#### policy for accounts creation

```sh
vault policy write account_creator -<<EOF
path "rockside/account/new" {
  capabilities = ["create"]
}
path "rockside/account/import" {
  capabilities = ["create"]
}
EOF
```

#### policy for transactions signing

On all accounts

```sh
vault policy write all_signer -<<EOF
path "rockside/transaction/*" {
  capabilities = ["create"]
}
EOF
```

On a specific account

```sh
vault policy write unique_signer -<<EOF
path "rockside/transaction/0x62b1d469a3ae3bb5669ea69c933bb1649ff02439" {
  capabilities = ["create"]
}
EOF
```

#### policy reading accounts

On all accounts

```sh
vault policy write all_reader -<<EOF
path "rockside/account/*" {
  capabilities = ["read"]
}
EOF
```

On a specific account

```sh
vault policy write unique_reader -<<EOF
path "rockside/account/0x62b1d469a3ae3bb5669ea69c933bb1649ff02439" {
  capabilities = ["read"]
}
EOF
```

#### create a token for a policy

```sh
vault token create -policy=<policy name>
```

This token allows you to connect to the vault and have access to all the route accessible with the associated policy.

### Example: contract deployment with truffle

First generate an account. You will need to transfert some ether to that address.

```sh
vault write -f rockside/account/new
# return the address: 0xabcdef00000000000000000000000000000000000
```

Create a policy for this account

```sh
vault policy write sign-transaction -<<EOF
path "rockside/transaction/0xabcdef00000000000000000000000000000000000" {
  capabilities = ["create"]
}
EOF
```

Derivate a token from this policy

```sh
vault token create -policy=sign-transaction
# return the token: VAULT_TOKEN
```

Add your rockside node RPC, VAUlT_TOKEN and sender address in your truffle.js.

```sh
var Web3 = require("web3");

module.exports = {
    networks: {
        development: {
            provider: function() {
                return new Web3.providers.HttpProvider('https://<ENGINE_URL>/api/nodes/rpc/<NODE_TOKEN>/<VAULT_TOKEN>');
            },
            network_id: "*",
            from: "0xabcdef00000000000000000000000000000000000",
        },
    }
}
```

Then launch truffle.

```sh
truffle migrate
```

And that's it ! You just sended an unsigned tx with your vault token, the vault has identified you and signed the tx with the good privatekey and then the tx was sent to the network. Keep in mind that the privatekey was never exposed.

### Understand how it work

![alt text](vault_simplified.png)

<!--- COMMENTED FOR LATER
### Which authentication provider is supported ?

We provide an javascript sdk for github authentification but you have to configure it in your vault first.
See [the official Vault documentation](https://www.vaultproject.io/docs/auth/github.html).

### Github identity provider configuration
You will need a github personal access token. If your not sure on how to get one look at the [official Vault documentation](https://www.vaultproject.io/docs/auth/github.html).

#### Vault config

```sh
# enable github auth
vault auth enable github

# link your github org to the vault
vault write auth/github/config organization=YOUR_ORG_GIT

# create a policy linked to an address
vault policy write POLICY_NAME -<<EOF
path "rockside/sign-tx/ADDRESS" {
  capabilities = ["create"]
}
EOF

# link the policy to a team of your github org
vault write auth/github/map/teams/GIT_TEAM value=sign-policy
```

#### sdk config

Create a file `rockside_sdk.js`.

```sh
touch rockside_sdk.js
```

And put this inside.

```js
const request = require('sync-request');
const VAULT_AUTH_PATH= '/v1/auth/github/login'

// TO COMPLETE WITH YOUR VAULT ADDRESS
const VAULT_ADDR = 'http://127.0.0.1:8200'

exports.getVaultToken = function(token) {
  let res = request('POST', VAULT_ADDR + VAULT_AUTH_PATH, {
    json: {token: token},
  });
  return JSON.parse(res.getBody('utf8')).auth.client_token;
}
```


#### truffle config

Edit `truffle-config.js` and put this instead.

```js
const Web3 = require('web3');
const rockside_sdk = require('./rockside_sdk');
let VAULT_TOKEN = ''

// TO COMPLETE WITH YOUR INFORMATION
const RPC_PROVIDER = 'YOUR_RPC_PROVIDER'
const SENDER = 'YOUR_ADDRESS'
const GITHUB_TOKEN = 'YOUR_GITHUB_TOKEN'

module.exports = {
  networks: {
    development: {
      provider: () => {
        if (VAULT_TOKEN == '') {
          VAULT_TOKEN = rockside_sdk.getVaultToken(GITHUB_TOKEN);
        }
        return new Web3.providers.HttpProvider(RPC_PROVIDER + '/' + VAULT_TOKEN)
      },
      from: SENDER,
      network_id: '*',
    },
  },
}
```

#### install dependencies

```sh
npm install web3 -s
npm install sync-request -s
```

#### run truffle

```sh
truffle migrate
```
--->

