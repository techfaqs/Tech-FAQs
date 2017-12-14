# Blockchain concepts

### Merkel Tree

In cryptography and computer science, a hash tree or Merkle tree is a tree
 in which every leaf node is labelled with the hash of a data block and every
 non-leaf node is labelled with the cryptographic hash of the labels of its
 child nodes. Hash trees allow efficient and secure verification of the contents
 of large data structures. Hash trees are a generalization of hash lists
 and hash chains.

 
Demonstrating that a leaf node is a part of a given binary hash tree requires
 computing a number of hashes proportional to the logarithm of the number of
 leaf nodes of the tree; this contrasts with hash lists, where the number is
 proportional to the number of leaf nodes itself.

The concept of hash trees is named after Ralph Merkle who patented it in 1979.


### 'forks' of the blockchain

Forks are created when nodes disagree on what the full sequence of blocks looks like.
Generally when there are two forks, it ends up in deprecation of one of the forks.


----


> ### A blockchain must have all of the following properties:
>
>    It's a merkle tree, or a construct with equivalent properties.
>    There is no single point of trust.
>    Multiple 'forks' of the blockchain may exist - that is, nodes may disagree on what the full sequence of blocks looks like.
>    In the case of such a fork, there must exist a deterministic consensus algorithm of some sort to decide what the "real" blockchain looks like (ie. which fork is "correct").
>    The consensus algorithm must be executable with only the information contained in the blockchain (or its forks), and no external input (eg. no decisionmaking from a centralized 'trust node').
>
> If your blockchain is missing any of the above properties, it is not a blockchain, it is just a ledger.
