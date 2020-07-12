# Command Line Interface

  - [Overview](#overview)
  - [Group **Contract**](#group-contract)
    - [Contract.New](#contractnew)
    - [Contract.Templates](#contracttemplates)
    - [Contract.Build](#contractbuild)
    - [Contract.Clean](#contractclean)
    - [Contract.Deploy](#contractdeploy)
    - [Contract.Call](#contractcall)
    - [Contract.Upgrade](#contractupgrade)
    - [Contract.Query](#contractquery)
  - [Group **Transactions**](#group-transactions)
    - [Transactions.New](#transactionsnew)
    - [Transactions.Send](#transactionssend)
  - [Group **Validator**](#group-validator)
    - [Validator.Stake](#validatorstake)
    - [Validator.Unstake](#validatorunstake)
    - [Validator.Unjail](#validatorunjail)
    - [Validator.Unbond](#validatorunbond)
    - [Validator.ChangeRewardAddress](#validatorchangerewardaddress)
    - [Validator.Claim](#validatorclaim)
  - [Group **Account**](#group-account)
    - [Account.Get](#accountget)
    - [Account.GetTransactions](#accountgettransactions)
  - [Group **Wallet**](#group-wallet)
    - [Wallet.Derive](#walletderive)
    - [Wallet.Bech32](#walletbech32)
  - [Group **Network**](#group-network)
    - [Network.NumShards](#networknumshards)
    - [Network.BlockNonce](#networkblocknonce)
    - [Network.Chain](#networkchain)
  - [Group **Cost**](#group-cost)
    - [Cost.GasPrice](#costgasprice)
    - [Cost.TxTransfer](#costtxtransfer)
    - [Cost.ScDeploy](#costscdeploy)
    - [Cost.ScCall](#costsccall)
  - [Group **Dispatcher**](#group-dispatcher)
    - [Dispatcher.Enqueue](#dispatcherenqueue)
    - [Dispatcher.Dispatch](#dispatcherdispatch)
    - [Dispatcher.DispatchContinuously](#dispatcherdispatchcontinuously)
    - [Dispatcher.Clean](#dispatcherclean)
  - [Group **BlockAtlas**](#group-blockatlas)
    - [BlockAtlas.CurrentBlockNumber](#blockatlascurrentblocknumber)
    - [BlockAtlas.BlockByNumber](#blockatlasblockbynumber)
    - [BlockAtlas.Transactions](#blockatlastransactions)
  - [Group **Dependencies**](#group-dependencies)
    - [Dependencies.Install](#dependenciesinstall)
    - [Dependencies.Check](#dependenciescheck)
  - [Group **Configuration**](#group-configuration)
    - [Configuration.Dump](#configurationdump)
    - [Configuration.Get](#configurationget)
    - [Configuration.Set](#configurationset)

## Overview

**erdpy** exposes a number of CLI **commands**, organized within **groups**.


```
$ erdpy --help
usage: erdpy [-h] [-v] [--verbose] COMMAND-GROUP [-h] COMMAND ...

-----------
DESCRIPTION
-----------
erdpy is part of the elrond-sdk and consists of Command Line Tools and Python SDK
for interacting with the Blockchain (in general) and with Smart Contracts (in particular).

erdpy targets a broad audience of users and developers.
https://docs.elrond.com/tools/erdpy.
        

COMMAND GROUPS:
  {contract,tx,validator,account,wallet,network,cost,dispatcher,blockatlas,deps,config}

TOP-LEVEL OPTIONS:
  -h, --help            show this help message and exit
  -v, --version         show program's version number and exit
  --verbose

----------------------
COMMAND GROUPS summary
----------------------
contract                       Build, deploy and interact with Smart Contracts
tx                             Create and broadcast Transactions
validator                      Stake, Unjail and other actions useful for Validators
account                        Get Account data (nonce, balance) from the Network
wallet                         Derive private key from mnemonic, bech32 address helpers etc.
network                        Get Network parameters, such as number of shards, chain identifier etc.
cost                           Estimate cost of Transactions
dispatcher                     Enqueue transactions, then bulk dispatch them
blockatlas                     Interact with an Block Atlas instance
deps                           Manage dependencies or elrond-sdk modules
config                         Configure elrond-sdk (default values etc.)

```
## Group **Contract**


```
$ erdpy contract --help
usage: erdpy contract COMMAND [-h] ...

Build, deploy and interact with Smart Contracts

COMMANDS:
  {new,templates,build,clean,deploy,call,upgrade,query}

OPTIONS:
  -h, --help            show this help message and exit

----------------
COMMANDS summary
----------------
new                            Create a new Smart Contract project based on a template.
templates                      List the available Smart Contract templates.
build                          Build a Smart Contract project using the appropriate buildchain.
clean                          Clean a Smart Contract project.
deploy                         Deploy a Smart Contract.
call                           Interact with a Smart Contract (execute function).
upgrade                        Upgrade a previously-deployed Smart Contract
query                          Query a Smart Contract (call a pure function)

```
### Contract.New


```
$ erdpy contract new --help
usage: erdpy contract new [-h] ...

Create a new Smart Contract project based on a template.

positional arguments:
  name

optional arguments:
  -h, --help             show this help message and exit
  --template TEMPLATE    the template to use
  --directory DIRECTORY  🗀 the parent directory of the project (default: current directory)

```
### Contract.Templates


```
$ erdpy contract templates --help
usage: erdpy contract templates [-h] ...

List the available Smart Contract templates.

optional arguments:
  -h, --help  show this help message and exit

```
### Contract.Build


```
$ erdpy contract build --help
usage: erdpy contract build [-h] ...

Build a Smart Contract project using the appropriate buildchain.

positional arguments:
  project            🗀 the project directory (default: current directory)

optional arguments:
  -h, --help         show this help message and exit
  --debug            set debug flag (default: False)
  --no-optimization  bypass optimizations (for clang) (default: False)

```
### Contract.Clean


```
$ erdpy contract clean --help
usage: erdpy contract clean [-h] ...

Clean a Smart Contract project.

positional arguments:
  project     🗀 the project directory (default: current directory)

optional arguments:
  -h, --help  show this help message and exit

```
### Contract.Deploy


```
$ erdpy contract deploy --help
usage: erdpy contract deploy [-h] ...

Deploy a Smart Contract.

positional arguments:
  project                                🗀 the project directory (default: current directory)

optional arguments:
  -h, --help                             show this help message and exit
  --metadata-upgradeable                 ⚙ whether the contract is upgradeable (default: False)
  --outfile OUTFILE                      where to save the output (default: stdout)
  --pem PEM                              🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE                      🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE                    🔑 a file containing keyfile's password, if keyfile provided
  --proxy PROXY                          🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --nonce NONCE                          # the nonce for the transaction
  --recall-nonce                         ⭮ whether to recall the nonce when creating the transaction (default: False)
  --gas-price GAS_PRICE                  ⛽ the gas price (default: 200000000000)
  --gas-limit GAS_LIMIT                  ⛽ the gas limit
  --value VALUE                          the value to transfer (default: 0)
  --chain CHAIN                          the chain identifier (default: testnet-elrond-all-in-one-test)
  --version VERSION                      the transaction version (default: 1)
  --arguments ARGUMENTS [ARGUMENTS ...]  arguments for the contract transaction, as numbers or hex-encoded. E.g.
                                         --arguments 42 0x64 1000 0xabba

```
### Contract.Call


```
$ erdpy contract call --help
usage: erdpy contract call [-h] ...

Interact with a Smart Contract (execute function).

positional arguments:
  contract                               🖄 the address of the Smart Contract

optional arguments:
  -h, --help                             show this help message and exit
  --pem PEM                              🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE                      🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE                    🔑 a file containing keyfile's password, if keyfile provided
  --proxy PROXY                          🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --nonce NONCE                          # the nonce for the transaction
  --recall-nonce                         ⭮ whether to recall the nonce when creating the transaction (default: False)
  --gas-price GAS_PRICE                  ⛽ the gas price (default: 200000000000)
  --gas-limit GAS_LIMIT                  ⛽ the gas limit
  --value VALUE                          the value to transfer (default: 0)
  --chain CHAIN                          the chain identifier (default: testnet-elrond-all-in-one-test)
  --version VERSION                      the transaction version (default: 1)
  --function FUNCTION                    the function to call
  --arguments ARGUMENTS [ARGUMENTS ...]  arguments for the contract transaction, as numbers or hex-encoded. E.g.
                                         --arguments 42 0x64 1000 0xabba

```
### Contract.Upgrade


```
$ erdpy contract upgrade --help
usage: erdpy contract upgrade [-h] ...

Upgrade a previously-deployed Smart Contract

positional arguments:
  contract                               🖄 the address of the Smart Contract
  project                                🗀 the project directory (default: current directory)

optional arguments:
  -h, --help                             show this help message and exit
  --metadata-upgradeable                 ⚙ whether the contract is upgradeable (default: False)
  --pem PEM                              🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE                      🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE                    🔑 a file containing keyfile's password, if keyfile provided
  --proxy PROXY                          🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --nonce NONCE                          # the nonce for the transaction
  --recall-nonce                         ⭮ whether to recall the nonce when creating the transaction (default: False)
  --gas-price GAS_PRICE                  ⛽ the gas price (default: 200000000000)
  --gas-limit GAS_LIMIT                  ⛽ the gas limit
  --value VALUE                          the value to transfer (default: 0)
  --chain CHAIN                          the chain identifier (default: testnet-elrond-all-in-one-test)
  --version VERSION                      the transaction version (default: 1)
  --arguments ARGUMENTS [ARGUMENTS ...]  arguments for the contract transaction, as numbers or hex-encoded. E.g.
                                         --arguments 42 0x64 1000 0xabba

```
### Contract.Query


```
$ erdpy contract query --help
usage: erdpy contract query [-h] ...

Query a Smart Contract (call a pure function)

positional arguments:
  contract                               🖄 the address of the Smart Contract

optional arguments:
  -h, --help                             show this help message and exit
  --proxy PROXY                          🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --function FUNCTION                    the function to call
  --arguments ARGUMENTS [ARGUMENTS ...]  arguments for the contract transaction, as numbers or hex-encoded. E.g.
                                         --arguments 42 0x64 1000 0xabba

```
## Group **Transactions**


```
$ erdpy tx --help
usage: erdpy tx COMMAND [-h] ...

Create and broadcast Transactions

COMMANDS:
  {new,send}

OPTIONS:
  -h, --help  show this help message and exit

----------------
COMMANDS summary
----------------
new                            Create a new transaction
send                           Send a previously saved transaction

```
### Transactions.New


```
$ erdpy tx new --help
usage: erdpy tx new [-h] ...

Create a new transaction

optional arguments:
  -h, --help             show this help message and exit
  --pem PEM              🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE      🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE    🔑 a file containing keyfile's password, if keyfile provided
  --nonce NONCE          # the nonce for the transaction
  --recall-nonce         ⭮ whether to recall the nonce when creating the transaction (default: False)
  --receiver RECEIVER    🖄 the address of the receiver
  --gas-price GAS_PRICE  ⛽ the gas price (default: 200000000000)
  --gas-limit GAS_LIMIT  ⛽ the gas limit
  --value VALUE          the value to transfer (default: 0)
  --data DATA            the payload, or 'memo' of the transaction (default: )
  --chain CHAIN          the chain identifier (default: testnet-elrond-all-in-one-test)
  --version VERSION      the transaction version (default: 1)
  --data-file DATA_FILE  a file containing transaction data
  --outfile OUTFILE      where to save the output (signed transaction, hash) (default: stdout)
  --send                 ✓ whether to broadcast (send) the transaction (default: False)
  --proxy PROXY          🖧 the URL of the proxy (default: http://104.248.107.195:8080)

```
### Transactions.Send


```
$ erdpy tx send --help
usage: erdpy tx send [-h] ...

Send a previously saved transaction

optional arguments:
  -h, --help         show this help message and exit
  --infile INFILE    input file (a previously saved transaction)
  --outfile OUTFILE  where to save the output (the hash) (default: stdout)
  --proxy PROXY      🖧 the URL of the proxy (default: http://104.248.107.195:8080)

```
## Group **Validator**


```
$ erdpy validator --help
usage: erdpy validator COMMAND [-h] ...

Stake, Unjail and other actions useful for Validators

COMMANDS:
  {stake,unstake,unjail,unbond,change-reward-address,claim}

OPTIONS:
  -h, --help            show this help message and exit

----------------
COMMANDS summary
----------------
stake                          Stake value into the Network
unstake                        Unstake value
unjail                         Unjail a Validator Node
unbond                         Unbond
change-reward-address          Change the reward address
claim                          Claim rewards

```
### Validator.Stake


```
$ erdpy validator stake --help
usage: erdpy validator stake [-h] ...

Stake value into the Network

optional arguments:
  -h, --help                             show this help message and exit
  --proxy PROXY                          🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --pem PEM                              🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE                      🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE                    🔑 a file containing keyfile's password, if keyfile provided
  --nonce NONCE                          # the nonce for the transaction
  --recall-nonce                         ⭮ whether to recall the nonce when creating the transaction (default: False)
  --gas-price GAS_PRICE                  ⛽ the gas price (default: 200000000000)
  --gas-limit GAS_LIMIT                  ⛽ the gas limit
  --estimate-gas                         ⛽ whether to estimate the gas limit (default: 0)
  --value VALUE                          the value to transfer (default: 0)
  --chain CHAIN                          the chain identifier (default: testnet-elrond-all-in-one-test)
  --version VERSION                      the transaction version (default: 1)
  --number-of-nodes NUMBER_OF_NODES      number of nodes to register
  --nodes-public-keys NODES_PUBLIC_KEYS  the public keys of the nodes as CSV (addrA,addrB)
  --reward-address REWARD_ADDRESS        the reward address

```
### Validator.Unstake


```
$ erdpy validator unstake --help
usage: erdpy validator unstake [-h] ...

Unstake value

optional arguments:
  -h, --help                             show this help message and exit
  --proxy PROXY                          🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --pem PEM                              🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE                      🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE                    🔑 a file containing keyfile's password, if keyfile provided
  --nonce NONCE                          # the nonce for the transaction
  --recall-nonce                         ⭮ whether to recall the nonce when creating the transaction (default: False)
  --gas-price GAS_PRICE                  ⛽ the gas price (default: 200000000000)
  --gas-limit GAS_LIMIT                  ⛽ the gas limit
  --estimate-gas                         ⛽ whether to estimate the gas limit (default: 0)
  --value VALUE                          the value to transfer (default: 0)
  --chain CHAIN                          the chain identifier (default: testnet-elrond-all-in-one-test)
  --version VERSION                      the transaction version (default: 1)
  --nodes-public-keys NODES_PUBLIC_KEYS  the public keys of the nodes as CSV (addrA,addrB)

```
### Validator.Unjail


```
$ erdpy validator unjail --help
usage: erdpy validator unjail [-h] ...

Unjail a Validator Node

optional arguments:
  -h, --help                             show this help message and exit
  --proxy PROXY                          🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --pem PEM                              🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE                      🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE                    🔑 a file containing keyfile's password, if keyfile provided
  --nonce NONCE                          # the nonce for the transaction
  --recall-nonce                         ⭮ whether to recall the nonce when creating the transaction (default: False)
  --gas-price GAS_PRICE                  ⛽ the gas price (default: 200000000000)
  --gas-limit GAS_LIMIT                  ⛽ the gas limit
  --estimate-gas                         ⛽ whether to estimate the gas limit (default: 0)
  --value VALUE                          the value to transfer (default: 0)
  --chain CHAIN                          the chain identifier (default: testnet-elrond-all-in-one-test)
  --version VERSION                      the transaction version (default: 1)
  --nodes-public-keys NODES_PUBLIC_KEYS  the public keys of the nodes as CSV (addrA,addrB)

```
### Validator.Unbond


```
$ erdpy validator unbond --help
usage: erdpy validator unbond [-h] ...

Unbond

optional arguments:
  -h, --help                             show this help message and exit
  --proxy PROXY                          🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --pem PEM                              🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE                      🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE                    🔑 a file containing keyfile's password, if keyfile provided
  --nonce NONCE                          # the nonce for the transaction
  --recall-nonce                         ⭮ whether to recall the nonce when creating the transaction (default: False)
  --gas-price GAS_PRICE                  ⛽ the gas price (default: 200000000000)
  --gas-limit GAS_LIMIT                  ⛽ the gas limit
  --estimate-gas                         ⛽ whether to estimate the gas limit (default: 0)
  --value VALUE                          the value to transfer (default: 0)
  --chain CHAIN                          the chain identifier (default: testnet-elrond-all-in-one-test)
  --version VERSION                      the transaction version (default: 1)
  --nodes-public-keys NODES_PUBLIC_KEYS  the public keys of the nodes as CSV (addrA,addrB)

```
### Validator.ChangeRewardAddress


```
$ erdpy validator change-reward-address --help
usage: erdpy validator change-reward-address [-h] ...

Change the reward address

optional arguments:
  -h, --help                       show this help message and exit
  --proxy PROXY                    🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --pem PEM                        🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE                🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE              🔑 a file containing keyfile's password, if keyfile provided
  --nonce NONCE                    # the nonce for the transaction
  --recall-nonce                   ⭮ whether to recall the nonce when creating the transaction (default: False)
  --gas-price GAS_PRICE            ⛽ the gas price (default: 200000000000)
  --gas-limit GAS_LIMIT            ⛽ the gas limit
  --estimate-gas                   ⛽ whether to estimate the gas limit (default: 0)
  --value VALUE                    the value to transfer (default: 0)
  --chain CHAIN                    the chain identifier (default: testnet-elrond-all-in-one-test)
  --version VERSION                the transaction version (default: 1)
  --reward-address REWARD_ADDRESS  the new reward address

```
### Validator.Claim


```
$ erdpy validator claim --help
usage: erdpy validator claim [-h] ...

Claim rewards

optional arguments:
  -h, --help             show this help message and exit
  --proxy PROXY          🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --pem PEM              🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE      🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE    🔑 a file containing keyfile's password, if keyfile provided
  --nonce NONCE          # the nonce for the transaction
  --recall-nonce         ⭮ whether to recall the nonce when creating the transaction (default: False)
  --gas-price GAS_PRICE  ⛽ the gas price (default: 200000000000)
  --gas-limit GAS_LIMIT  ⛽ the gas limit
  --estimate-gas         ⛽ whether to estimate the gas limit (default: 0)
  --value VALUE          the value to transfer (default: 0)
  --chain CHAIN          the chain identifier (default: testnet-elrond-all-in-one-test)
  --version VERSION      the transaction version (default: 1)

```
## Group **Account**


```
$ erdpy account --help
usage: erdpy account COMMAND [-h] ...

Get Account data (nonce, balance) from the Network

COMMANDS:
  {get,get-transactions}

OPTIONS:
  -h, --help            show this help message and exit

----------------
COMMANDS summary
----------------
get                            Query account details (nonce, balance etc.)
get-transactions               Query account transactions

```
### Account.Get


```
$ erdpy account get --help
usage: erdpy account get [-h] ...

Query account details (nonce, balance etc.)

optional arguments:
  -h, --help         show this help message and exit
  --proxy PROXY      🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --address ADDRESS  🖄 the address to query
  --balance          whether to only fetch the balance
  --nonce            whether to only fetch the nonce

```
### Account.GetTransactions


```
$ erdpy account get-transactions --help
usage: erdpy account get-transactions [-h] ...

Query account transactions

optional arguments:
  -h, --help         show this help message and exit
  --proxy PROXY      🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --outfile OUTFILE  where to save the output (default: stdout)
  --address ADDRESS  🖄 the address to query

```
## Group **Wallet**


```
$ erdpy wallet --help
usage: erdpy wallet COMMAND [-h] ...

Derive private key from mnemonic, bech32 address helpers etc.

COMMANDS:
  {derive,bech32}

OPTIONS:
  -h, --help       show this help message and exit

----------------
COMMANDS summary
----------------
derive                         derive a PEM file from a mnemonic or generate a new PEM file (for tests only!)
bech32                         Helper for encoding and decoding bech32 addresses

```
### Wallet.Derive


```
$ erdpy wallet derive --help
usage: erdpy wallet derive [-h] ...

derive a PEM file from a mnemonic or generate a new PEM file (for tests only!)

positional arguments:
  pem         path of the output PEM file

optional arguments:
  -h, --help  show this help message and exit
  --mnemonic  whether to derive from an existing mnemonic

```
### Wallet.Bech32


```
$ erdpy wallet bech32 --help
usage: erdpy wallet bech32 [-h] ...

Helper for encoding and decoding bech32 addresses

positional arguments:
  value       the value to encode or decode

optional arguments:
  -h, --help  show this help message and exit
  --encode    whether to encode
  --decode    whether to decode

```
## Group **Network**


```
$ erdpy network --help
usage: erdpy network COMMAND [-h] ...

Get Network parameters, such as number of shards, chain identifier etc.

COMMANDS:
  {num-shards,block-nonce,chain}

OPTIONS:
  -h, --help            show this help message and exit

----------------
COMMANDS summary
----------------
num-shards                     Get the number of shards.
block-nonce                    Get the latest block nonce, by shard.
chain                          Get the chain identifier.

```
### Network.NumShards


```
$ erdpy network num-shards --help
usage: erdpy network num-shards [-h] ...

Get the number of shards.

optional arguments:
  -h, --help     show this help message and exit
  --proxy PROXY  🖧 the URL of the proxy (default: http://104.248.107.195:8080)

```
### Network.BlockNonce


```
$ erdpy network block-nonce --help
usage: erdpy network block-nonce [-h] ...

Get the latest block nonce, by shard.

optional arguments:
  -h, --help     show this help message and exit
  --proxy PROXY  🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --shard SHARD  the shard ID (use 4294967295 for metachain)

```
### Network.Chain


```
$ erdpy network chain --help
usage: erdpy network chain [-h] ...

Get the chain identifier.

optional arguments:
  -h, --help     show this help message and exit
  --proxy PROXY  🖧 the URL of the proxy (default: http://104.248.107.195:8080)

```
## Group **Cost**


```
$ erdpy cost --help
usage: erdpy cost COMMAND [-h] ...

Estimate cost of Transactions

COMMANDS:
  {gas-price,tx-transfer,sc-deploy,sc-call}

OPTIONS:
  -h, --help            show this help message and exit

----------------
COMMANDS summary
----------------
gas-price                      Query minimum gas price
tx-transfer                    Query cost of regular transaction (transfer)
sc-deploy                      Query cost of Smart Contract deploy transaction
sc-call                        Query cost of Smart Contract call transaction

```
### Cost.GasPrice


```
$ erdpy cost gas-price --help
usage: erdpy cost gas-price [-h] ...

Query minimum gas price

optional arguments:
  -h, --help     show this help message and exit
  --proxy PROXY  🖧 the URL of the proxy (default: http://104.248.107.195:8080)

```
### Cost.TxTransfer


```
$ erdpy cost tx-transfer --help
usage: erdpy cost tx-transfer [-h] ...

Query cost of regular transaction (transfer)

optional arguments:
  -h, --help     show this help message and exit
  --proxy PROXY  🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --data DATA    a transaction payload, required to estimate the cost

```
### Cost.ScDeploy


```
$ erdpy cost sc-deploy --help
usage: erdpy cost sc-deploy [-h] ...

Query cost of Smart Contract deploy transaction

positional arguments:
  project                                🗀 the project directory (default: current directory)

optional arguments:
  -h, --help                             show this help message and exit
  --proxy PROXY                          🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --arguments ARGUMENTS [ARGUMENTS ...]  arguments for the contract transaction, as numbers or hex-encoded. E.g.
                                         --arguments 42 0x64 1000 0xabba

```
### Cost.ScCall


```
$ erdpy cost sc-call --help
usage: erdpy cost sc-call [-h] ...

Query cost of Smart Contract call transaction

positional arguments:
  contract                               🖄 the address of the Smart Contract

optional arguments:
  -h, --help                             show this help message and exit
  --proxy PROXY                          🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --function FUNCTION                    the function to call
  --arguments ARGUMENTS [ARGUMENTS ...]  arguments for the contract transaction, as numbers or hex-encoded. E.g.
                                         --arguments 42 0x64 1000 0xabba

```
## Group **Dispatcher**


```
$ erdpy dispatcher --help
usage: erdpy dispatcher COMMAND [-h] ...

Enqueue transactions, then bulk dispatch them

COMMANDS:
  {enqueue,dispatch,dispatch-continuously,clean}

OPTIONS:
  -h, --help            show this help message and exit

----------------
COMMANDS summary
----------------
enqueue                        Enqueue a transaction
dispatch                       Dispatch queued transactions
dispatch-continuously          Continuously dispatch queued transactions
clean                          Clear queue of transactions

```
### Dispatcher.Enqueue


```
$ erdpy dispatcher enqueue --help
usage: erdpy dispatcher enqueue [-h] ...

Enqueue a transaction

optional arguments:
  -h, --help             show this help message and exit
  --receiver RECEIVER    🖄 the address of the receiver
  --gas-price GAS_PRICE  ⛽ the gas price (default: 200000000000)
  --gas-limit GAS_LIMIT  ⛽ the gas limit
  --value VALUE          the value to transfer (default: 0)
  --data DATA            the payload, or 'memo' of the transaction (default: )
  --chain CHAIN          the chain identifier (default: testnet-elrond-all-in-one-test)
  --version VERSION      the transaction version (default: 1)

```
### Dispatcher.Dispatch


```
$ erdpy dispatcher dispatch --help
usage: erdpy dispatcher dispatch [-h] ...

Dispatch queued transactions

optional arguments:
  -h, --help           show this help message and exit
  --proxy PROXY        🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --pem PEM            🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE    🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE  🔑 a file containing keyfile's password, if keyfile provided

```
### Dispatcher.DispatchContinuously


```
$ erdpy dispatcher dispatch-continuously --help
usage: erdpy dispatcher dispatch-continuously [-h] ...

Continuously dispatch queued transactions

optional arguments:
  -h, --help           show this help message and exit
  --proxy PROXY        🖧 the URL of the proxy (default: http://104.248.107.195:8080)
  --pem PEM            🔑 the PEM file, if keyfile not provided
  --keyfile KEYFILE    🔑 a JSON keyfile, if PEM not provided
  --passfile PASSFILE  🔑 a file containing keyfile's password, if keyfile provided
  --interval INTERVAL  the interval to retrieve transactions from the queue, in seconds

```
### Dispatcher.Clean


```
$ erdpy dispatcher clean --help
usage: erdpy dispatcher clean [-h] ...

Clear queue of transactions

optional arguments:
  -h, --help  show this help message and exit

```
## Group **BlockAtlas**


```
$ erdpy blockatlas --help
usage: erdpy blockatlas COMMAND [-h] ...

Interact with an Block Atlas instance

COMMANDS:
  {current-block-number,block-by-number,transactions}

OPTIONS:
  -h, --help            show this help message and exit
  --url URL             🖧 URL of Block Atlas instance
  --coin COIN           coin identifier (e.g. erd, bnb)

----------------
COMMANDS summary
----------------
current-block-number           Get latest notarized metablock (number / nonce)
block-by-number                Get block by number (nonce)
transactions                   Get transactions by address

```
### BlockAtlas.CurrentBlockNumber


```
$ erdpy blockatlas current-block-number --help
usage: erdpy blockatlas current-block-number [-h] ...

Get latest notarized metablock (number / nonce)

optional arguments:
  -h, --help  show this help message and exit

```
### BlockAtlas.BlockByNumber


```
$ erdpy blockatlas block-by-number --help
usage: erdpy blockatlas block-by-number [-h] ...

Get block by number (nonce)

optional arguments:
  -h, --help       show this help message and exit
  --number NUMBER  the number (nonce)

```
### BlockAtlas.Transactions


```
$ erdpy blockatlas transactions --help
usage: erdpy blockatlas transactions [-h] ...

Get transactions by address

optional arguments:
  -h, --help         show this help message and exit
  --address ADDRESS  🖄 the address to query
  --outfile OUTFILE  where to save the output (default: stdout)

```
## Group **Dependencies**


```
$ erdpy deps --help
usage: erdpy deps COMMAND [-h] ...

Manage dependencies or elrond-sdk modules

COMMANDS:
  {install,check}

OPTIONS:
  -h, --help       show this help message and exit

----------------
COMMANDS summary
----------------
install                        Install dependencies or elrond-sdk modules.
check                          Check whether a dependency is installed.

```
### Dependencies.Install


```
$ erdpy deps install --help
usage: erdpy deps install [-h] ...

Install dependencies or elrond-sdk modules.

positional arguments:
  {clang,cpp,rust,arwentools}  the dependency to install

optional arguments:
  -h, --help                   show this help message and exit
  --overwrite                  whether to overwrite an existing installation
  --tag TAG                    the tag or version to install

```
### Dependencies.Check


```
$ erdpy deps check --help
usage: erdpy deps check [-h] ...

Check whether a dependency is installed.

positional arguments:
  {clang,cpp,rust,arwentools}  the dependency to check

optional arguments:
  -h, --help                   show this help message and exit
  --tag TAG                    the tag or version to check

```
## Group **Configuration**


```
$ erdpy config --help
usage: erdpy config COMMAND [-h] ...

Configure elrond-sdk (default values etc.)

COMMANDS:
  {dump,get,set}

OPTIONS:
  -h, --help      show this help message and exit

----------------
COMMANDS summary
----------------
dump                           Dumps configuration.
get                            Gets a configuration value.
set                            Sets a configuration value.

```
### Configuration.Dump


```
$ erdpy config dump --help
usage: erdpy config dump [-h] ...

Dumps configuration.

optional arguments:
  -h, --help  show this help message and exit

```
### Configuration.Get


```
$ erdpy config get --help
usage: erdpy config get [-h] ...

Gets a configuration value.

positional arguments:
  name        the name of the configuration entry

optional arguments:
  -h, --help  show this help message and exit

```
### Configuration.Set


```
$ erdpy config set --help
usage: erdpy config set [-h] ...

Sets a configuration value.

positional arguments:
  name        the name of the configuration entry
  value       the new value

optional arguments:
  -h, --help  show this help message and exit

```