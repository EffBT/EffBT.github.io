---
layout: default
---

# Proofs

## [](#header-2) **1. RP1 and RP2**

In the NaiveBT method, four regular patterns (RPs) are designed to transform ITE to BTs. RP1 is the rule that describes the relation from P to P', and RP2 is the rule that describes the relation from P' to P. We match those two RPs into the same structure of BTs, and we try to explain and prove it by the truth table. Note that we swap the variable sequence of the truth table of $P'\rarr P$ for comparison.

For the formula $P \rightarrow P'$ and $P' \rightarrow P$, their truth tables are as follows. 

|  $P$ |  $P'$ |  $P \rightarrow P'$ |
|:---:|:---:|:---:|
|  0 | 0  | 1  |
|  0 | 1  | 1  |
|  1 | 0  | 0  |
|  1 | 1  | 1  |


|  $P$ |  $P'$ |  $P' \rightarrow P$ |
|:---:|:---:|:---:|
|  0 | 0  | 1  |
|  0 | 1  | 0  |
|  1 | 0  | 1  |
|  1 | 1  | 1  |



