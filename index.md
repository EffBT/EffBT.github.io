---
layout: default
---
   
**EffBT** is an effective behavior tree synthesis and execution framework, that fills the gap []. Besides, we optimized the execution efficiency of generated BTs by applying the **Parallel** node, while few prior focused on this aspect.

* * *

<!-- # [](#header-1)**Introduction** -->

<!-- # [](#header-2)**Motivation** -->

*   [**Introduction**](introduction)

*   [**Experiment Scenarios and Specifications**](specification)

*   [**Evaluation Results and Analysis**](evaluation)

*   [**Supporting Proofs**](proof)


* * *

# [](#header-1)**Features**

*   `Automatic Synthesis`:  **EffBT** takes as input the GR(1) specifications, and produce BTs that satisfy those specifications automatically. Compared to other synthesis methods, EffBT unifies the transition functions calculation. 

*   `Efficient Execution`: Moreover, **EffBT** optimize the execution of synthesized BTs by structure improvement and the adoption of *Parallel* nodes, while none of the prior works focused on it, to the best of our knowledge. Experiments have demonstrated the improvement in execution speed of BTs. See more details in [**Evaluation Results**](evaluation).

<!-- *   `Transparent Compilation`: **CCMOP** provides a transparent compilation framework that avoids the tedious compilation configuration. -->


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

*   <font color="#0000FF" size="4"> Anonymous Temporarily (Under Review)</font>


<span id="jump1">[1]</span>. EffBT: An Effective Behavior Tree Reactive Synthesis and Execution Framework.([PDF](resources/effbt-paper.pdf))

* * *