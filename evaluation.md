---
layout: default
---
# Evaluation
We evaluated **EffBT** and two running examples(**Naive BT**, **RawBT**) on the GR(1) synthesis tool [*Spectra*](https://github.com/SpectraSynthesizer). To evaluate our approach, we have four research questions: **RQ1** Are the NaiveBT and the RawBT methods inefficient? **RQ2** Does the EffBT method perform better in synthesis? **RQ3** How about the quality of synthesized BTs from EffBT? **RQ4** Does pruning strategies bring improvements?


We examine our methods in diffirent Scenarios: *FrozenLake+*, *Cinderella*, and *SYNTECH* scenarios. All the experiments were carried out on a Windows 10 computer equipped with an AMD Ryzen 9 5950X CPU. The maximum allowed time for synthesis is two hours, and the maximum allowed memory is 2048MB. Processes will be forcibly terminated if they exceed the allotted time or memory. To minimize the impact of JVM, all methods are executed on a single processor five times under each scenario and each setting, and the final results of evaluated metrics are the averages among them. Subsequently, our experiments consist of two parts along with an ablation study.


## [](#header-2) **1. Evaluation Metrics**
In order to answer the four research questions, we designed many sets of experiments. Specific indicators and descriptions are shown in the table below.

| Metric              | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| *#Nodes*            | the sum of nodes when checking realizability which indicates the scale of problems. |
| *Time~RC~*          | records the time spent on the realizability check            |
| *Construction Time* | records the duration from the time of starting synthesis to its completion, excluding the time taken for realizability checks |
| *BT Size*           | the total number of nodes of generated BTs, inclusive of both ControlFlow and Execution node |
| *Balance*           | consists of two parts: *Structural Balance* and *Node Balance*.  The former is defined as $\frac{N_{min}}{N_{max}}$, in which $N_{min}$ and $N_{max}$ represent the minimum and maximum node counts among subtrees under the root. The latter is defined as $\exp{(-&#124; N_{exec}/N_{ctrl} - 2 &#124;)}$, in which $N_{exec}$ and $N_{ctrl}$ denote the sum of Execution nodes and ControlFlow nodes, respectively. |


Moreover, to answer *RQ4*, we conducted an ablation study by disabling all pruning strategies in EffBT, which forms the *EffBT-NP*(or *EffBT#*) method. Then, we evaluate it and record metrics following the same procedure in the aforementioned two parts.

## [](#header-2) **2. Synthesis Efficiency Results**
### [](#header-3)**(1). Results of the NaiveBT Method**
The step-by-step evaluation results of the NaiveBT method under two Frozen+ settings are shown below.

|                   Task                   | FrozenLake+ 8X8 | FrozenLake+ 16X16 |
|:----------------------------------------:|:---------------:|:-----------------:| 
|       Nodes Num (Nodes Table Size)       |   0.25(4.68)    |    6.37(78.33)    |
| Step1: Checking Realizability Time (sec) |      0.05       |        2.1        |
|       Step2: FDS Construction Time       |      0.04       |       13.38       |
|       Step3: ITE Construction Time       |     #DIV/0!     |      #DIV/0!      |
|    **Step4: NaiveBT Synthesis Time**     |      0.67       |      144.45       |
|                Total Time                |     #DIV/0!     |      #DIV/0!      |
|               **BT Size**                |     104392      |       15346       |

Based on the results, it is found that the majority of the synthesis time was spent on ITE construction(Step 3) and NaiveBT generation(Step 4), which took much longer time than the Realizability Check(Step 1) and FDS Construction(Step 2). The inefficiency of these two steps lowers the overall method performance. Besides, we didn't present more outcomes of the NaiveBT method since we had already tested it under other scenarios, while it always ran out of time or memory. Moreover, both the generated BTs have a size of over 100,000, which is extremely large and results in low execution efficiency. 

***Answer to RQ1(NaiveBT)***: the NaiveBT method indeed suffers inefficiency problems as it consumes a large amount of time and memory, yet yields low-quality BTs.

### [](#header-3)**(2). Results of Synthesis**
The following table summarizes the evaluation results of the synthesis procedure of the original GR(1), RawBT, EffBT\#, and our EffBT methods under Frozen^+, Cinderella, and SYNTECH scenarios. In this table, OOT represents the process running out of the maximum allowed time. The time unit in this table is *seconds*.

***FrozenLake+ Senarios***

|        |                    |         | nodes  | nodes(10k) | time-rc-ms | time-rc-sec | construct-ms |
| ------ | ------------------ | ------- | ------ | ---------- | ---------- | ----------- | ------------ |
| gr1    | FrozenLake+8x8     | 2624    | 0.26   | 45.2236    | 0.05       | 33.4727     | 0.03         |
|        | FrozenLake+  16x16 | 63667   | 6.37   | 2109.8259  | 2.11       | 13705.4473  | 13.71        |
|        | FrozenLake+  24x24 | 495435  | 49.54  | 34631.8472 | 34.63      | 280623.5504 | 280.62       |
|        | FrozenLake+  32x32 | 1180989 | 118.1  | 133802.419 | 133.8      | -           | #VALUE!      |
|        |                    |         |        |            |            |             |              |
| rawbt  | FrozenLake+8x8     | 2439    | 0.24   | 60.5192    | 0.06       | 13.0238     | 0.01         |
|        | FrozenLake+  16x16 | 63652   | 6.37   | 2222.9441  | 2.22       | 4206.8737   | 4.21         |
|        | FrozenLake+  24x24 | 482475  | 48.25  | 23750.0794 | 23.75      | 417261.4369 | 417.26       |
|        | FrozenLake+  32x32 | 1181188 | 118.12 | 133654.419 | 133.65     | 2355654.259 | 2355.65      |
|        |                    |         |        |            |            |             |              |
| effbt  | FrozenLake+8x8     | 2427    | 0.24   | 53.1326    | 0.05       | 6.2838      | 0.01         |
|        | FrozenLake+  16x16 | 63645   | 6.36   | 2041.3472  | 2.04       | 2778.1917   | 2.78         |
|        | FrozenLake+  24x24 | 495302  | 49.53  | 32697.8483 | 32.7       | 37200.1463  | 37.2         |
|        | FrozenLake+  32x32 | 1181467 | 118.15 | 136459.419 | 136.46     | 575898.0268 | 575.9        |
|        |                    |         |        |            |            |             |              |
| effbt# | FrozenLake+8x8     | 2427    | 0.24   | 54.3925    | 0.05       | 6.268101    | 0.01         |
|        | FrozenLake+  16x16 | 63672   | 6.37   | 2431.1119  | 2.43       | 2980.262099 | 2.98         |
|        | FrozenLake+  24x24 | 495382  | 49.54  | 33687.4868 | 33.69      | 47622.3226  | 47.62        |
|        | FrozenLake+  32x32 | 1181004 | 118.1  | 123944.473 | 123.94     | 1015643.308 | 1015.64      |

***Cinderella Scenarios***

|        |               | nodes | nodes(10k) | time-rc-ms  | time-rc-sec | construct-ms | construct-sec |
| ------ | ------------- | ----- | ---------- | ----------- | ----------- | ------------ | ------------- |
| gr1    | cinderella  1 | 5922  | 0.59       | 325.5642    | 0.33        | 1462.1114    | 1.46          |
|        | cinderella  2 | 11002 | 1.1        | 1804.533    | 1.8         | 3425.3802    | 3.43          |
|        | cinderella  3 | 25268 | 2.53       | 17894.3193  | 17.89       | 35837.9303   | 35.84         |
|        | cinderella  4 | 94036 | 9.4        | 269553.0843 | 269.55      | 55453.3521   | 55.45         |
|        |               |       |            |             |             |              |               |
| rawbt  | cinderella  1 | 6049  | 0.6        | 440.5768    | 0.44        | 7.319        | 0.01          |
|        | cinderella  2 | 11072 | 1.11       | 1812.7352   | 1.81        | 22.3184      | 0.02          |
|        | cinderella  3 | 25424 | 2.54       | 22499.7412  | 22.5        | 113.0933     | 0.11          |
|        | cinderella  4 | 94057 | 9.41       | 315534.9454 | 315.53      | 760.3909     | 0.76          |
|        |               |       |            |             |             |              |               |
| effbt  | cinderella  1 | 5776  | 0.58       | 304.1481    | 0.3         | 8.1446       | 0.01          |
|        | cinderella  2 | 11002 | 1.1        | 1818.9884   | 1.82        | 20.2733      | 0.02          |
|        | cinderella  3 | 25515 | 2.55       | 18109.9033  | 18.11       | 79.2002      | 0.08          |
|        | cinderella  4 | 94169 | 9.42       | 243742.4152 | 243.74      | 577.0302     | 0.58          |
|        |               |       |            |             |             |              |               |
| effbt# | cinderella  1 | 5910  | 0.59       | 311.5813    | 0.31        | 10.8151      | 0.01          |
|        | cinderella  2 | 11002 | 1.1        | 1771.214701 | 1.77        | 20.346699    | 0.02          |
|        | cinderella  3 | 25505 | 2.55       | 17606.392   | 17.61       | 82.3647      | 0.08          |
|        | cinderella  4 | 94034 | 9.4        | 233034.5559 | 233.03      | 588.5614     | 0.59          |

***SYNTECH Scenarios***

|        |             | nodes  | nodes(10k) | time-rc-ms | time-rc-sec | construct-ms | construct-sec |
| ------ | ----------- | ------ | ---------- | ---------- | ----------- | ------------ | ------------- |
| gr1    | convoycar   | 5720   | 0.57       | 5.0865     | 0.01        | 18.484       | 0.02          |
|        | robotarm    | 48199  | 4.82       | 1538.0069  | 1.54        | 7920.1489    | 7.92          |
|        | humanoid    | 4159   | 0.42       | 43.2668    | 0.04        | 29.9232      | 0.03          |
|        | selfparking | 7099   | 0.71       | 483.7347   | 0.48        | 705.2767     | 0.71          |
|        | jobschedure | 19992  | 2          | 795.49     | 0.8         | 56055.6911   | 56.06         |
|        | hanoi       | 481256 | 48.13      | 18471.5259 | 18.47       | 48116.786    | 48.12         |
|        |             |        |            |            |             |              |               |
| rawbt  | convoycar   | 6008   | 0.6        | 5.0039     | 0.01        | 15.0219      | 0.02          |
|        | robotarm    | 48153  | 4.82       | 1535.4865  | 1.54        | 7149.038     | 7.15          |
|        | humanoid    | 4159   | 0.42       | 44.1562    | 0.04        | 62.0913      | 0.06          |
|        | selfparking | 7099   | 0.71       | 473.8749   | 0.47        | 97.9198      | 0.1           |
|        | jobschedure | 19587  | 1.96       | 680.2386   | 0.68        | 888653.4458  | 888.65        |
|        | hanoi       | 481256 | 48.13      | 17472.0856 | 17.47       | 98682.5191   | 98.68         |
|        |             |        |            |            |             |              |               |
| effbt  | convoycar   | 5852   | 0.59       | 13.23      | 0.01        | 3.8703       | 0             |
|        | robotarm    | 55617  | 5.56       | 2688.4279  | 2.69        | 1821.0535    | 1.82          |
|        | humanoid    | 4159   | 0.42       | 43.2671    | 0.04        | 20.87        | 0.02          |
|        | selfparking | 7099   | 0.71       | 475.5764   | 0.48        | 10.545       | 0.01          |
|        | jobschedure | 19614  | 1.96       | 645.4581   | 0.65        | 3022.5742    | 3.02          |
|        | hanoi       | 481607 | 48.16      | 18321.5309 | 18.32       | 37635.131    | 37.64         |
|        |             |        |            |            |             |              |               |
| effbt# | convoycar   | 5636   | 0.56       | 5.2453     | 0.01        | 2.885        | 0             |
|        | robotarm    | 48155  | 4.82       | 1450.39    | 1.45        | 1856.7935    | 1.86          |
|        | humanoid    | 4159   | 0.42       | 41.9802    | 0.04        | 20.8907      | 0.02          |
|        | selfparking | 7099   | 0.71       | 491.2401   | 0.49        | 10.4174      | 0.01          |
|        | jobschedure | 19997  | 2          | 639.8402   | 0.64        | 3405.0011    | 3.41          |
|        | hanoi       | 481256 | 48.13      | 18497.0543 | 18.5        | 38602.0373   | 38.6          |

From the construction time results, our method synthesizes much faster than the RawBT and GR(1) methods under every scenario and every setting. Besides, it grows much slower in time with the increasing problem scale. For instance, in the larger 32$\times$32 Frozen$^+$ environment, the GR(1) approaches timed out and the RawBT took almost one hour, whereas our method achieved results within approximately fifteen minutes as the problem size escalated. Besides, note that in the 64$\times$64 Frozen$^+$ scenario, none of these methods could synthesize a valid result as the realizability check had about 1.3 million nodes and timed out. 

The implementation of the RawBT method didn't follow the expected procedure that obtains FDS first(Step2) and then synthesizes RawBT(Step3$'$). Specifically, we construct BTs from Step 1 but follow the construction of FDS as mentioned in Step~3$'$. Hence, the construction time of RawBT would not be restricted by the original FDS construction as shown in Table.~\ref{tab: synthesis result}.

|        task        | nodes-10k-avg | time-rc-sec-avg |
| :----------------: | :-----------: | :-------------: |
|   FrozenLake+8x8   |     0.25      |      0.05       |
| FrozenLake+  16x16 |     6.37      |       2.2       |
| FrozenLake+  24x24 |     49.22     |      31.19      |
| FrozenLake+  32x32 |    118.12     |     131.96      |
|   cinderella  1    |     0.59      |      0.35       |
|   cinderella  2    |      1.1      |       1.8       |
|   cinderella  3    |     2.54      |      19.03      |
|   cinderella  4    |     9.41      |     265.46      |
|     convoycar      |     0.58      |      0.01       |
|      robotarm      |     5.01      |      1.81       |
|      humanoid      |     0.42      |      0.04       |
|    selfparking     |     0.71      |      0.48       |
|    jobschedure     |     1.98      |      0.69       |
|       hanoi        |     48.14     |      18.19      |



## [](#header-2) **3. Behavior Tree Quality Results**

### [](#header-3)**(1).Structural Results**
In terms of the BT Size, our method achieves a reduction of more than *half* compared to the RawBT method, primarily due to the pruning operations in EffBT. Regarding the balance of the tree, the EffBT method performs better horizontally but is weaker vertically. Hence, we analyzed the detailed structure of BTs from the EffBT method and found that their maximum depth was just five in the Frozen$^+$ scenario and three in the Cinderella scenario. Thus, the little weakness in tree balance indicates limited vertical complexity. In conclusion, our method performs much better in synthesis time and quality and grows slower when the problem becomes more complex.

Note that those obtained BTs under all settings of the Cinderella scenario have the same size and tree balance. To explain, we draw it out as shown in Fig.~\ref{fig: synthesized bt}. Its original root node *Parallel* was pruned since it has only one justice goal, thus, its root is the *Sequence* node from *subBT*. Then, because all the conditions in $BT_{\rho_2}$ and $BT_{\rho_3}$ are False, the root of $\rho$ transitions is also pruned making the current root come from $BT_{\rho_1}$. Finally, the synthesized result has such a structure. Although they have the same structure, the contents in each node are different.

***FrozenLake+ Senarios***

|        |                    | size | min  | max  | seq  | selector | leaf | stru-balance | node-balance | Balance | exec-raw | execution |
| :----: | :----------------: | :--: | :--: | :--: | :--: | :------: | :--: | :----------: | :----------: | :-----: | :------: | :-------: |
| EffBT  |   FrozenLake+8x8   |  41  |  38  |  38  |  13  |    2     |  26  |      1       |     0.77     |  1.77   | 47.31767 |    47     |
|        | FrozenLake+  16x16 | 408  |  53  |  65  | 131  |    15    | 262  |     0.82     |     0.81     |  1.63   | 194.7179 |    195    |
|        | FrozenLake+  24x24 | 1698 |  65  |  86  | 551  |    45    | 1102 |     0.76     |     0.86     |  1.62   | 444.7719 |    445    |
|        | FrozenLake+  32x32 | 3871 |  86  | 113  | 1264 |    79    | 2528 |     0.76     |     0.89     |  1.65   | 776.3278 |    776    |
|        |                    |      |      |      |      |          |      |              |              |         |          |           |
| RawBT  |   FrozenLake+8x8   |  89  |  5   |  43  |  28  |    6     |  55  |     0.12     |     0.68     |   0.8   | 63.28258 |    63     |
|        | FrozenLake+  16x16 | 839  |  29  | 415  | 276  |    18    | 545  |     0.07     |     0.86     |  0.93   | 256.493  |    256    |
|        | FrozenLake+  24x24 | 3464 |  89  | 1720 | 1146 |    48    | 2270 |     0.05     |     0.91     |  0.96   | 597.5344 |    598    |
|        | FrozenLake+  32x32 | 7861 | 157  | 3910 | 2606 |    82    | 5173 |     0.04     |     0.93     |  0.97   | 910.5353 |    911    |
|        |                    |      |      |      |      |          |      |              |              |         |          |           |
| EffBt# |   FrozenLake+8x8   |  95  |  94  |  94  |  39  |    4     |  52  |      1       |     0.45     |  1.45   | 79.09348 |    79     |
|        | FrozenLake+  16x16 | 939  | 122  | 150  | 393  |    22    | 524  |     0.81     |     0.48     |  1.29   | 302.5369 |    303    |
|        | FrozenLake+  24x24 | 3924 | 150  | 199  | 1653 |    67    | 2204 |     0.75     |     0.49     |  1.24   | 671.3761 |    671    |
|        | FrozenLake+  32x32 | 8966 | 192  | 255  | 3792 |   118    | 5056 |     0.75     |     0.49     |  1.24   | 1276.894 |   1277    |

***Cinderella Senarios***

|        |               | size | min  | max  | seq  | selector | leaf | stru balance | node balance | Balance | exec-raw | execution |
| ------ | :-----------: | :--: | :--: | :--: | :--: | :------: | :--: | :----------: | :----------: | :-----: | :------: | :-------: |
| EffBT  | cinderella  1 |  6   |  3   |  3   |  2   |    0     |  4   |      1       |      1       |    2    | 3983.275 |   3983    |
|        | cinderella  2 |  6   |  3   |  3   |  2   |    0     |  4   |      1       |      1       |    2    | 195725.9 |  195726   |
|        | cinderella  3 |  6   |  3   |  3   |  2   |    0     |  4   |      1       |      1       |    2    | 23814.21 |   23814   |
|        | cinderella  4 |  6   |  3   |  3   |  2   |    0     |  4   |      1       |      1       |    2    | 570717.8 |  570718   |
|        |               |      |      |      |      |          |      |              |              |         |          |           |
| RawBT  | cinderella  1 |  23  |  5   |  10  |  6   |    6     |  11  |     0.5      |     0.34     |  0.84   | 4591.658 |   4592    |
|        | cinderella  2 |  23  |  5   |  10  |  6   |    6     |  11  |     0.5      |     0.34     |  0.84   | 264817.8 |  264818   |
|        | cinderella  3 |  23  |  5   |  10  |  6   |    6     |  11  |     0.5      |     0.34     |  0.84   | 30232.89 |   30233   |
|        | cinderella  4 |  23  |  5   |  10  |  6   |    6     |  11  |     0.5      |     0.34     |  0.84   | 720199.9 |  720200   |
|        |               |      |      |      |      |          |      |              |              |         |          |           |
| EffBT# | cinderella  1 |  18  |  17  |  17  |  6   |    4     |  8   |      1       |     0.3      |   1.3   | 5616.404 |   5616    |
|        | cinderella  2 |  18  |  17  |  17  |  6   |    4     |  8   |      1       |     0.3      |   1.3   | 321088.6 |  321089   |
|        | cinderella  3 |  18  |  17  |  17  |  6   |    4     |  8   |      1       |     0.3      |   1.3   | 36218.92 |   36219   |
|        | cinderella  4 |  18  |  17  |  17  |  6   |    4     |  8   |      1       |     0.3      |   1.3   | 948331.9 |  948332   |

***SYNTECH Senarios***

|        |             | size  |  min  |  max  |  seq  | selector | leaf  | stru -balance | node -balance | Balance | exec-raw | execution |
| :----: | :---------: | :---: | :---: | :---: | :---: | :------: | :---: | :-----------: | :-----------: | :-----: | :------: | :-------: |
| EffBT  |  convoyvar  |  20   |  20   |  20   |   6   |    2     |  12   |       1       |     0.61      |  1.61   | 215.3147 |    215    |
|        |  robotarm   |  96   |  17   |  35   |  29   |    9     |  58   |     0.49      |     0.62      |  1.11   | 5203.535 |   5204    |
|        |  humanoid   |  110  |  48   |  61   |  39   |    7     |  64   |     0.79      |     0.54      |  1.33   | 572.8974 |    573    |
|        | selfparking |  201  |  38   |  65   |  72   |    13    |  116  |     0.58      |     0.53      |  1.11   | 700.4521 |    700    |
|        | jobschedure |  516  |  11   |  56   |  165  |    21    |  330  |      0.2      |      0.8      |    1    | 8955.821 |   8956    |
|        |    hanoi    | 12296 | 12296 | 12296 | 4098  |    2     | 8196  |       1       |       1       |    2    | 982.0763 |    982    |
|        |             |       |       |       |       |          |       |               |               |         |          |           |
| RawBT  |  convoyvar  |  47   |   5   |  22   |  14   |    6     |  27   |     0.23      |     0.52      |  0.75   | 267.2975 |    267    |
|        |  robotarm   |  206  |  17   |  100  |  66   |    12    |  128  |     0.17      |      0.7      |  0.87   | 6287.424 |   6287    |
|        |  humanoid   |  161  |   9   |  117  |  19   |    48    |  94   |     0.08      |     0.55      |  0.63   | 722.2061 |    722    |
|        | selfparking |  352  |  17   |  273  |  32   |   108    |  212  |     0.06      |     0.62      |  0.68   | 892.9473 |    893    |
|        | jobschedure | 1064  |  41   |  526  |  24   |   350    |  690  |     0.08      |     0.86      |  0.94   | 10524.35 |   10524   |
|        |    hanoi    | 24599 |   5   | 12298 | 8198  |    6     | 16395 |       0       |       1       |    1    | 1224.647 |   1225    |
|        |             |       |       |       |       |          |       |               |               |         |          |           |
| EffBT# |  convoyvar  |  46   |  45   |  45   |  18   |    4     |  24   |       1       |      0.4      |   1.4   | 339.2503 |    339    |
|        |  robotarm   |  216  |  38   |  80   |  87   |    13    |  116  |     0.48      |     0.43      |  0.91   | 6685.885 |   6686    |
|        |  humanoid   |  150  |  68   |  81   |  55   |    7     |  88   |     0.84      |     0.56      |   1.4   | 881.0291 |    881    |
|        | selfparking |  333  |  67   |  99   |  120  |    13    |  200  |     0.68      |     0.61      |  1.29   | 931.4821 |    931    |
|        | jobschedure | 1186  |  24   |  129  |  495  |    31    |  660  |     0.19      |     0.47      |  0.66   | 13417.73 |   13418   |
|        |    hanoi    | 28690 | 28689 | 28689 | 12294 |    4     | 16392 |       1       |     0.51      |  1.51   | 1495.735 |   1496    |



### [](#header-3)**(2).Execution Results**

Tables presents the execution results of the BTs (or FDS) synthesized by the RawBT, EffBT, and the original GR(1) methods. We didn't execute the BTs synthesized from the NaiveBT method because their sizes are extremely large (over 100,000). In this table, the symbol `-' denotes that the method cannot synthesize BTs (or FDS) under such a setting (caused by OOT or OOM) and thus has nothing to execute. Besides, note that the time is the average of the sum of fifty decision-making and its unit is *milliseconds*.

By analyzing the results, we have concluded that the complexity of the problems has a limited impact on the time taken for decision-making. Even in the most complex configurations, the time increment for the BTs in Frozen$^+$ and Cinderella-Stepmother is only 3$\times$ and 5$\times$ higher respectively compared to the simplest configurations. However, when we compare our methods with others, the EffBT method effectively reduces the execution time of decision-making, with more significant improvements observed especially in scenarios like Cinderella-Stepmother where the execution time is longer. As shown in Fig.~\ref{fig: synthesized bt}, there are no *Parallel* nodes in the synthesized BTs under the Cinderella scenario, hence, we suggest that its execution speed improvement is from our pruning strategies. indicating that our method owns better reactivity since it could decide and perform the next action much faster.



## [](#header-2) **3.  Ablation Study Results**





| task               | effbt# | effbt | % (裁剪比) | effbt# | effbt  | %（加速比） |
| ------------------ | ------ | ----- | ---------- | ------ | ------ | ----------- |
| FrozenLake+8x8     | 95     | 41    | 56.84      | 79     | 47     | 0.405063    |
| FrozenLake+  16x16 | 939    | 408   | 56.55      | 303    | 195    | 0.356436    |
| FrozenLake+  24x24 | 3924   | 1698  | 56.73      | 671    | 445    | 0.336811    |
| FrozenLake+  32x32 | 8966   | 3871  | 56.83      | 1277   | 776    | 0.392326    |
| cinderella  1      | 18     | 6     | 66.67      | 5616   | 3983   | 0.290776    |
| cinderella  2      | 18     | 6     | 66.67      | 321089 | 195726 | 0.390431    |
| cinderella  3      | 18     | 6     | 66.67      | 36219  | 23814  | 0.3425      |
| cinderella  4      | 18     | 6     | 66.67      | 948332 | 570718 | 0.398188    |
| convoyvar          | 46     | 20    | 56.52      | 339    | 215    | 0.365782    |
| robotarm           | 216    | 96    | 55.56      | 6686   | 5204   | 0.221657    |
| humanoid           | 150    | 110   | 26.67      | 881    | 573    | 0.349603    |
| selfparking        | 333    | 201   | 39.64      | 931    | 700    | 0.24812     |
| jobschedure        | 1186   | 516   | 56.49      | 13418  | 8956   | 0.332538    |
| hanoi              | 28690  | 12296 | 57.14      | 1496   | 982    | 0.343583    |
