---
layout: default
---

# Proofs

## [](#header-2) **1. RP1 and RP2**

In the NaiveBT method, four regular patterns (RPs) are designed to transform ITE to BTs. RP1 is the rule that describes the relation from P to P', and RP2 is the rule that describes the relation from P' to P. We match those two RPs into the same structure of BTs, and we try to explain and prove it by the truth table. Note that we swap the variable sequence of the truth table of $P'\rightarrow P$ for comparison.

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

Although their truth tables differ, assuming that P' is always true – a valid assumption since there is always a scenario where P' holds – the truth of the formula then hinges solely on the truth value of P, and consequently carries the same semantic meaning as $P \rightarrow P'$. Therefore, we have constructed identical behavior tree representations for these two patterns, reflecting their shared logical behavior under this particular assumption.

