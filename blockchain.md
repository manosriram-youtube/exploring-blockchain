Exploring BlockChain and Bitcoin

Bitcoin runs on blockchain tech.

p2p network, where every transaction is stored and is immutable.

[b1] -> [b2] -> [b3]

TODO:

1. proof-of-work algorithm
2. what is nonce?
3. how is difficulty target used in block header

## Block

block header -> metadata of the block: 80bytes
aggregate transactions to include in the ledger. avg block contains > 500 txns

block header contains previous (parent) block hash

identifying a block:

1. by its cryptographic hash. we obtain this hash by hashing the block header twice
   using SHA256 algorithm.

2. by its block height. each block is appended on top of the topmost block in the network.

(2) isn't unique exactly. there can be 2 block fighting for that block height, called as
blockchain forks.

### Genesis Block

first block in the blockchain. every node always knows the genesis block's hash.

a node is a peer. more nodes = more decentralization.

### Linking blocks in the blockchain

block has `previous_block_header_hash`. when a node sees this in a block, it links it thus
extending the blockchain.

## Merkle Trees

usecase: to summarize all transactions in a block.

tree is constructed using bottom-up approach.

each txn is a leaf node. intermediate hashes are calculated. makes it easier to reach the
destination txn.

1000s of txns can be stored under 512 bytes.

simplified payment verification (spv) uses merkle tree to verify if a transaction exists in a block.

## Transactions

#### lifecycle of a txn:

1. txn is signed by one or more signatures.
2. txn is broadcasted into the network.
3. each node validates this txn and propagates to other nodes.
4. txn is verified by a mining node and included in a block of transactions in the blockchain.

structure of a txn:
version
input counter
input
output counter
output
locktime -> earliest time when the txn was valid.

input = credit (money coming in)
output = debit (money going out)

balance = 10$

send 4$ from "abcde" to "fghij"

a. send 10$ from "abcde" to "fghij"
b. send (10-4 = 6$) from "fghij" to "abcde"

UTXO = unspent transaction outputs

## Network Discovery

seed nodes = long running stable nodes.

if a new node connects to a seed node, its easier to get other nodes.

new node sends its own IP addr to other nodes, and they to others and so on...

## Full nodes

nodes (or) computers (or) peers which have a complete blockchain with all transactions.
it takes over 20gb and 2-3 days to sync.

why does a node need to be a full node?

node usually relies on other peers inorder to do stuff, because that node doesn't have enough data.
a full node does have all the data, so its independent of any other node in the blockchain.

## Bloom Filters

why?
spv nodes use bloom filters to ask their peers for transactions matching a specific pattern.
bloom filters does this by protecting their privacy as well.
