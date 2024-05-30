# [](#header-1)**Introduction to EffBT**

## **Motivation**
Behavior Trees originate from the control of Non-Player-Characters (NPCs) and have been widely used in robotics because of their advantages in modularity, reactivity, and some others. Research on constructing BTs automatically has received widespread attention and lots of methods have been applied to it. Reactive synthesis obtains correct-by-construct BTs from formal specifications and has the advantage of a correction guarantee compared to other approaches. 
However, the model-checking-based reactive synthesis suffers an EXPTIME complexity and the synthesis on fragment specifications needs to calculate different functions for each formula. Hence, we propose EffBT, which improves the synthesis efficiency by unifying the function calculation. Benefiting from the unification, we optimize the execution efficiency of obtained BTs by structure change and add the \textit{Parallel} node, while none of the prior works focused on this. Experiments have proved the effectiveness of our method.


## **EffBT's Framework**
<!-- Insides **CCMOP**, we designed the framework based on JavaMOP and implemented the instrumentation at the AST level. The framework of **CCMOP** is shown in the following figure.   -->

<!-- <br>

<img src="resources/framework.png" alt="framework" style="display:block; margin:- auto;">

<br> -->

The input of our method is the same as GR(1), which takes input as $(GS, \varphi)$.

<!-- The inputs of **CCMOP** are a program and the property to verify. **CCMOP** accepts the property and generates an AOP Declaration and Monitor code in C++. The AOP Declaration will be fed to Weaver, which weaves the monitor interface to the input program at the AST level. The instrumented AST will be passed to the compiler's backend and compiled into an object. The Monitor code will be compiled as a monitor binary with compilation option **-O3**. In the linking stage, the binaries mentioned above will be linked together to generate an executable with monitors. -->

# [](#header-1)**Contacts**

Please feel free to contact us if you have any questions about **EffBT**.

*   <font color="#0000FF" size="4"> Anonymous Temporarily (Under Review)</font>


