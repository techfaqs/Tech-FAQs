# BitCoin Block-chain


A block of one or more new transactions is collected into the
transaction data part of a block. Copies of each transaction are hashed,
and the hashes are then paired, hashed, paired again, and hashed
again until a single hash remains, the merkle root of a merkle tree.

The merkle root is stored in the block header. Each block also stores
the hash of the previous block’s header, chaining the blocks together.
This ensures a transaction cannot be modified without modifying the
block that records it and all following blocks.

Transactions are also chained together. Bitcoin wallet software gives
the impression that satoshis are sent from and to wallets, but bitcoins
really move from transaction to transaction. Each transaction spends
the satoshis previously received in one or more earlier transactions,
so the input of one transaction is the output of a previous

### satoshis
Denominations of Bitcoin value, usually measured in fractions of a bitcoin
but sometimes measured in multiples of a satoshi. One bitcoin equals 100,000,000 satoshis.


Reference: [BitCoin Dev Guide](https://bitcoin.org/en/glossary/denominations)
