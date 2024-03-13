---
layout: default
---
# Evaluation
We evaluated **CCMOP** for 100 real-world C/C++ programs. We collected the compilation time of each project for different properties. For runtime overhead, we evaluated CCMOP on the programs using **Use-afer-free** property. All the experiments were carried out on a laptop with a 2.60GHz CPU and 32G memory, and the operating system is Ubuntu 20.04. The result values are the averaged values of three runs within **-O3**.

## [](#header-2) **1. Benchmark**

The 50 real-world C++ programs are as follows.

Benchmark（CXX）|Category|Compile Command|Lines(K lines)
| :----: | :----: | :----: |:----: |
jsonCPP|Funzzbench|cmake ..;make|10.5
re2|Funzzbench|cmake ..;make|29
harfbuzz|Funzzbench|cmake ..;make|110
json|Funzzbench|cmake ..;make|102
bloty|Funzzbench|cmake ..;make|538.6
PROJ|Funzzbench|cmake ..;make|212
di|Github|cmake ..;make|24.6
cgbot|Github|cmake ..;make|12.6
spdlog|Github|cmake ..;make|24
fmt|Github|cmake ..;make|44
simdjson|Github|cmake ..;make|78
googletest|Github|cmake ..;make|42
flameshot|Github|cmake ..;make|50
sqlpp11|Github|cmake ..;make|59
2048|Github|cmake ..;make|2.7
SQLiteCPP|Github|cmake ..;make|156
git-crypt|Github|make|3.7
double-conversion|Github|cmake ..;make|322.9
tinyrendere|Github|cmake ..;make|1.2
tinyserver|Github|make|1
TinyWebServer|Github|make|2.1
abseil|Github|cmake ..;make|165
backward|Github|cmake ..;make|4
easy3D|Github|cmake ..;make|13.3
brpc|Github|cmake ..;make|239
capnproto|Github|cmake ..;make|210
Catch2-devel|Github|cmake ..;make|48.1
coost|Github|cmake ..;make|37
FasTC|Github|make|53.7
cxxopts|Github|cmake ..;make|12.3
docopt.cpp|Github|cmake ..;make|2.7
FTXUI|Github|cmake ..;make|24
glob|Github|cmake ..;make|10.4
guetzli|Github|cmake ..;make|8.3
lepton|Github|cmake ..;make|63
libfacedetection|Github|cmake ..;make|3
libutp|Github|make|4.1
libzmp|Github|cmake ..;make|62
nana|Github|cmake ..;make|72
Magic_enum|Github|cmake ..;make|19
simplejson|Github|cmake ..;make|1.5
muduo|Github|cmake ..;make|36
MyTinySTL|Github|cmake ..;make|19.3
ncnn|Github|cmake ..;make|675.2
pybind11|Github|cmake ..;make|25
Range-v3|Github|cmake ..;make|77
rapidjson|Github|cmake ..;make|30
tinyxmil2|Github|cmake ..;make|5.5
WebServer|Github|cmake ..;make|10.4
yaml-cpp|Github|cmake ..;make|80.4

The 50 real-world C programs and the programs in movec-minibench are as follows.

Benchmark（C）|Category|Compile Command|Lines(K lines)
| :----: | :----: | :----: | :----: |
cJSON|Fuzzbench|make build;cd build;cmake ..;make|15.2
libarchive|Fuzzbench|make build;cd build;cmake ..;make|154.4
libjpeg|Fuzzbench|make build;cd build;cmake ..;make|13.2
libgit2|Fuzzbench|make build;cd build;cmake ..;make|24.5
libcap|Fuzzbench|./configure;make|52
libtiff|Fuzzbench|make build;cd build;cmake ..;make|68.4
libpng|Fuzzbench|make build;cd build;cmake ..;make|24.7
libxml2|Fuzzbench|make build;cd build;cmake ..;make|228.5
mation|Fuzzbench|make build;cd build;cmake ..;make|21.6
mbedlts|Fuzzbench|make build;cd build;cmake ..;make|107.7
zlib|Fuzzbench|./configure;make|18.8
zstd|Fuzzbench|make|72.2
movec-msbench (126 small programs)|Movec|make|2.4
libuuid|Ferry|./configure;make|22
tcpdump|Ferry|./configure;make|79.5
ogg|Ferry|cmake ..;make|2.5
czmq|Github|cmake ..;make|51.3
libstrip|Github|cmake ..;make|19.1
libavf|Github|cmake ..;make|22.3
json-c|Github|cmake ..;make|11
glfw|Github|cmake ..;make|70.7
curl|Github|cmake ..;make|169.1
raylib|Github|cmake ..;make|239.5
kcp|Github|cmake ..;make|3.5
zaver|Github|cmake ..;make|2.6
naomsg|Github|cmake..;make|23.4
mozjpeg|Github|cmake..;make|63.5
brotil|Github|cmake..;make|34.8
parson|Github|cmake ..;make|3
libxlst|Github|cmake ..;make|34.8
cpu-feature|Github|cmake ..;make|2.1
luna|Github|make|3.8
mon|Github|make|1.8
gc|Github|make|1.5
pwnat|Github|make|2.1
adpcm|Github|make|0.51
basicmath|Github|make|3.5
Bitcount|Github|make|5.3
Blowfish|Github|make|1.4
CRC32|Github|make|0.12
Dijkstra|Github|make|0.28
FFT|Github|make|0.28
Gsm|Github|make|4.9
Patricial|Github|make|0.28
Qsort|Github|make|0.1
Rsynth|Github|make|5.5
Sha|Github|make|0.2
Stringsearch|Github|make|3
Susan|Github|make|1.4
typeset|Github|make|28.6
kilo|Github|make|1.1


The properties used in the evaluation are as follws. 

Type|Property Name |Description
| :----: | :----: | :----: |
C|Use-after-free|Pointer is dereferenced after freed(**free**)
C|Memory leak|Memory is allocated(**malloc**) results but not freed(**free**)
C|Read-after-close|A **FILE** is read after close
C++|Use-after-free|Pointer is dereferenced after freed(**delete**)
C++|Memory leak|Memory is allocated(**new**) but not freed(**delete**)
C++|Safe Iterator|A collection should be updated when it is being iterated

There are two properties, i.e., use-after-free and memory-leak, are used for both C and C++ programs. However, the event definations of them are different. We weave monitors when calling **malloc** and **free** in C programs, and we weave monitors to the **new** and **delete** statements in C++ programs.


## [](#header-2) **2. Evaluation results**
The evaluation results contain the compilation time for 100 real-world C/C++ programs and the runtime overhead only for C/C++ programs with valid test drivers.
### [](#header-3)**(1).Compilation Time**
We evaluate each C/C++ program for three properties. For C programs, the properties are Use-after-free, Memory-leak, and Read-after-close. For C++ programs, the properties are Use-after-free, Memory-leak, and Safe-Iterator. In addition, the common properties have different pointcuts for different languages. The results of compilation time are shown as follows.

The columns labeled **Average-O**, **Average-U**, **Average-M**, and **Average-R/U** represent the average of three test values of Original compilation, RV for Use-after-free, RV for Memory-leak and RV for Read-afer-close or Safe-Iterator respectively. The rows labeled **Overhead-*** means the average compilation time with RV (denoted **C<sub>RV</sub>**) overhead compared with the average original compilation time (denoted **C<sub>O</sub>**); that is **(C<sub>RV</sub>-C<sub>O</sub>)/C<sub>O</sub>**. In addition, the former 50 programs are  C programs, and the latter 50 are C++ programs.  



The following figure shows the above data, where the X-axis shows the project names, and the Y-axis shows the value of compilation overhead.

<img src="resources/evaluation-res.PNG" alt="compileTime" style="display: block; margin:- auto;">

The above figure or table shows that the compilation overhead of the majority (78%) of the C/C++ programs is below 300%. There are some programs whose compilation overhead exceeds 500%, with most of the overall compilation time occupied by the monitor library building stage. You can download the original data of the three runs from the following link.  
[Download](resources/compilelist.csv)

### [](#header-3)**(2).Runtime Overhead**

We evaluate the runtime overhead for the Use-after-free property. We did experiments on **AddressSanitizer** within **-O3** for comparison. We use the below compilation options of **AddressSanitizer**; We expect these options to suppress other checkers.
```code
 -O3 -fsanitize=address  -fsanitize-recover=address  -mllvm -asan-stack=0 -mllvm -asan-globals=0 -fno-sanitize-address-use-after-scope 
export ASAN_OPTIONS=detect_container_overflow=0:detect_leaks=0:leak_check_at_exit=0:check_printf=0:detect_container_overflow=0:buffer_overflow=0:report_globals=0:detect_stack_use_after_return=0:new_delete_type_mismatch=0:alloc_dealloc_mismatch=0:poison_heap=0:poison_partial=0:protect_shadow_gap=0:check_malloc_usable_size=0:allow_user_poisoning=0:replace_intrin=0:replace_str=0
```
Out of the 100 real-world programs, those without drivers or a runtime overhead of AddressSanitizer or CCMOP lower than **5%** are not shown. In addition, the programs on which Sanitizer fails have not been listed. The evaluation results of valid C++ programs are shown below.
  
name|Avg-Origin(s)|Avg-AddressSanitizer(s)|Avg-CCMOP(s)|Overhead-SAN|Overhead-CCMOP
| :----: | :----: | :----: | :----: | :----: | :----: |
backward-cpp|0.55|0.59|0.6|0.072727273|0.090909091
MyTinySTL|196.7266667|208.0233333|247.5933333|0.057423159|0.258565184
jsoncpp|2.393333333|4.853333333|2.726666667|1.027855153|0.139275766
json|452.1333333|577.8033333|509.71|0.277948983|0.127344441
di-cpp14|60.88666667|73.74666667|71.91|0.211212088|0.181046754
muduo|63.58333333|80.92333333|68.67666667|0.272712975|0.080104849
magic_enum|0.05|0.136666667|0.06|1.733333333|0.2
FasTC|0.11|0.213333333|0.46|0.939393939|3.181818182
yaml-cpp|0.22|0.676666667|0.34|2.075757576|0.545454545
flameshot|0.596666667|0.746666667|0.636666667|0.251396648|0.067039106
re2|1.163333333|2.003333333|3.41|0.722063037|1.931232092
rapidjson|0.62|1.98|2.95|2.193548387|3.758064516
Avg||||0.819614379|0.88007121


We draw a figure to represent the above data as follows. The X-axis is the project name, and the Y-axis is **log<sub>10</sub><sup>Overhead-RV+1</sup>**.  

<img src="resources/fig2.png" alt="cxx_runtime" style="display: block; margin:- auto;">

If you are interested in the data from the three test runs, you can download it by clicking the following link.  
[Download](resources/cxx_runtime.csv)  

The evaluation results of the C programs are shown below.  


name|Avg-Origin(s)|Avg-AddressSanitizer(s)|Avg-CCMOP(s)|Overhead-SAN|Overhead-CCMOP
| :----: | :----: | :----: | :----: | :----: | :----: |
qsort|0.05|0.06|0.06|0.2|0.2
adpcm|0.323333333|0.44|0.913333333|0.360824742|1.824742268
blowfish|0.12|0.176666667|1.25|0.472222222|9.416666667
libpng-1.2.56|0.02|0.04|0.04|1|1
susan|0.296666667|1.573333333|1.27|4.303370787|3.280898876
libxml2|0.493333333|3.06|13.09|5.202702703|25.53378378
libsrtp|14.39|16.10333333|20.77666667|0.119064165|0.443826732
json-c|21.96333333|35.37666667|30.61666667|0.610714828|0.393989983
cJSON|0.06|0.143333333|0.07|1.388888889|0.166666667
glfw|0.06|0.07|0.086666667|0.166666667|0.444444444
typeset|0.07|0.2|0.12|1.857142857|0.714285714
gsm|0.116666667|0.196666667|4.093333333|0.685714286|34.08571429
bitcount|0.066666667|0.07|0.44|0.05|5.6
brotli|0.523333333|0.786666667|6.653333333|0.503184713|11.7133758
dijkstra|0.023333333|0.05|1.183333333|1.142857143|49.71428571
FFT|0.07|0.08|0.413333333|0.142857143|4.904761905
libtiff|1.03|1.056666667|1.116666667|0.025889968|0.084142395
rsynth|0.13|0.15|3.286666667|0.153846154|24.28205128
zlib|0.02|0.03|0.1|0.5|4
mozjpeg|3.503333333|6.113333333|54.41333333|0.745004757|14.53187441
Avg||||0.981547601|9.616775546


Some programs listed above frequently involve memory operations and have a higher overhead for CCMOP, which increases the average value. Besides, the figure is as follows.

<img src="resources/fig3.png" alt="c_runtime" style="display: block; margin:- auto;">  

If you are interested in the data from the three test runs, you can download it by clicking the following link.  
[Download](resources/c_runtime.csv)

## [](#header-2)**3.Evaluation reproduction**

We provide the scripts for reproducing our evaluation. Before running the following command, you need to confirm that **wac, CCMOP/bin** in your **PATH** and export the **<CCMOP/lib>** to **ASPECT_LIB**. For the evaluation of the compilation test, you can run the following command:
```shell
python3 test_compileTime.py
```
If the above command succeeds, you can see **compilelist.csv** and **compilelist.pdf** in your current directory. For the evaluation of the runtime overhead test, you can run the following command:
```shell
python3 test_runtimeOverhead.py
```
If the above command succeeds, you could see **c_runtime.csv**,**cxx_runtime.csc**,**c_runtime.pdf** and **cxx_runtime.pdf** in your current directory.  In addition, the runtime PDF is a figure drawn with the data in the CSV file and filters out some invalid data.

# [](#header-1)**Contacts**

Please feel free to contact us if you have any questions about **CCMOP**.

*   <font color="#0000FF" size="4">Yongchao Xing (xingyc0979@nudt.edu.cn)</font>

*   <font color="#0000FF" size="4"> Zhenbang Chen (zbchen@nudt.edu.cn)</font>
