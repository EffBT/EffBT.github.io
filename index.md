---
layout: default
---
   
**EffBT** is an effective behavior tree synthesis and execution framework, that fills the gap []. Besides, we optimized the execution efficiency of generated BTs by applying the **Parallel** node, while few prior focused on this aspect.

* * *

*   [**Introduction**](introduction)

<!-- *   [**Manual**](manual) -->

<!-- *   [**Tutorial**](tutorial) -->

*   [**Scenarios and Specifications**](specification)

*   [**Evaluation results**](evaluation)

*   [**Proofs**](proof)

* * *

# [](#header-1)**Features**

*   `Efficient`: The runtime overhead of **CCMOP** is acceptable, and the average runtime overhead is less than 10x compared to the original C/C++ programs. See more details in [**Evaluation results and reproduction**](evaluation).

*   `Source-level Instrumentation`: **CCMOP** provides an AOP framework implemented by source-level instrumentation carried out on abstract syntax trees (ASTs).

*   `Transparent Compilation`: **CCMOP** provides a transparent compilation framework that avoids the tedious compilation configuration.


* * *
# [](#header-1)**Demonstration Vedio**

<video width="860" height="485" controls>
  <source src="resources/effbt.demo.mp4" type="video/mp4">
</video>

* * *

# [](#header-1)**Usage**

We provide the runnable JAR package of our tools [Download](resources/effbt_V1.0.jar) (50MB). 

By the way, the recommonded JDK version is JDK 17 or greater. The JDK 13 is not supported and we didn't test it on other JDK versions.

```
usage: java -jar spectra-cli.jar
    --counter-strategy               Generate counter-strategy for an unrealizable specification
    --counter-strategy-jtlv-format   Generate counter-strategy for an unrealizable specification 
                                     and print in JTLV format
    --disable-grouping               Disable reorder with grouping
    --disable-opt <arg>              Disable optimizations
    --display                        Display generated controllers,
                                     default flase
 -i,--input <arg>                    Spectra input file name
    --jtlv                           Use JTLV package instead of CUDD
 -o,--output <arg>                   Ouptut folder
    --reorder                        Reorder BDD before save for reduced
                                     size
 -s,--synthesize <arg>               Synthesize symbolic controller
 -sim,--simulate <arg>               Simulate n (from input) times of the
                                     FDS by calculate succs
    --static                         Synthesize static symbolic controller
 -synthBT,--synthBT <arg>            Synthesis a BT, while parms meaning
                                     the synthesized BT type.
 -v,--verbose                        Verbose logging
    --well-separation                Check well-separation considering
                                     system guarantees
    --well-separation-ignore-sys     Check well-separation ignoring system
                                     guarantees

```


* * *

# [](#header-1)**Contacts**

Please feel free to contact us if you have any questions about our **EffBT**.

*   <font color="#0000FF" size="4">Ziji Wu (wuziji@nudt.edu.cn)</font>

<!-- *   <font color="#0000FF" size="4"> Zhenbang Chen (zbchen@nudt.edu.cn)</font> -->

* * *
<!-- <span id="jump1">[1]</span>. Yongchao Xing, Zhenbang Chen, Shibo Xu, Yufeng Zhang. CCMOP: A Runtime Verification Tool for C/C++ Programs[C] International Conference on Runtime Verification. Cham: Springer Nature Switzerland, 2023: 339-350.([PDF](https://zbchen.github.io/files/rv2023.pdf)) -->

<span id="jump1">[1]</span>. EffBT: An Effective Behavior Tree Reactive Synthesis and Execution Framework.([PDF](https://zbchen.github.io/files/rv2023.pdf))

* * *