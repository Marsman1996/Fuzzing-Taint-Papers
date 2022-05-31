# All Papers
- [PATA: Fuzzing with Path Aware Taint Analysis (S&P'22)](#pata-fuzzing-with-path-aware-taint-analysis)  
- [GREYONE: Data Flow Sensitive Fuzzing (Usenix'20)](#greyone-data-flow-sensitive-fuzzing)
- [Angora: Efficient Fuzzing by Principled Search (S&P'18)](#angora-efficient-fuzzing-by-principled-search)
- [VUzzer: Application-aware Evolutionary Fuzzing (NDSS'17)](#vuzzer-application-aware-evolutionary-fuzzing)

# Details

## PATA: Fuzzing with Path Aware Taint Analysis
* [Paper](http://www.wingtecher.com/themes/WingTecherResearch/assets/papers/sp22.pdf) 

**Abstract:** 
Taint analysis assists fuzzers in solving complex fuzzing constraints by inferring the influencing input bytes. Execution paths in real-world programs often reach loops, where constraints in these loops can be visited and recorded multiple times. Conventional taint analysis techniques experience difficulties when distinguishing between multiple occurrences of the same constraint. In this paper, we propose PATA, a fuzzer that implements path-aware taint analysis, i.e. one that distinguishes between multiple occurrences of the same variable based on the execution path information. PATA does so using the following steps. First, PATA identifies variables used in constraints and constructs the Representative Variable Sequence (RVS), consisting of occurrences of all representative constraint variables and their values. Next, PATA perturbs the input, matches its RVS with that of the original input, and looks for value changes to identify the influencing input bytes for each entry in the RVS. Finally, PATA mutates the corresponding input bytes to solve constraints in the given path.

To demonstrate the effectiveness of PATA over conventional taint analysis methods, we evaluated its performance on the benchmarks Google’s fuzzer-test-suite and LAVA-M against AFL, MOPT, TortoriseFuzz, VUzzer, Angora, REDQUEEN, and GREYONE. On Google’s fuzzer-test-suite, PATA outperformed these state-of-the-art fuzzers by 29%–1830% and 7%–87% in the number of unique paths found and basic blocks covered, respectively. More importantly, it found more bugs than the comparison fuzzers, including 17 unlisted ones. On LAVA-M, PATA performed the best out of all evaluated fuzzers and found 2602 bugs. On open-source projects, PATA found 40 previously unknown bugs, with 12 of them confirmed as CVEs.

## GREYONE: Data Flow Sensitive Fuzzing
* [Paper](https://www.usenix.org/system/files/sec20-gan.pdf)
* [Slide](https://www.usenix.org/system/files/sec20_slides_gan.pdf)

**Abstract:** 
Data flow analysis (e.g., dynamic taint analysis) has proven to be useful for guiding fuzzers to explore hard-to-reach code and find vulnerabilities. However, traditional taint analysis is labor-intensive, inaccurate and slow, affecting the fuzzing efficiency. Apart from taint, few data flow features are utilized.

In this paper, we proposed a data flow sensitive fuzzing solution GREYONE. We first utilize the classic feature taint to guide fuzzing. A lightweight and sound fuzzing-driven taint inference (FTI) is adopted to infer taint of variables, by monitoring their value changes while mutating input bytes during fuzzing. With the taint, we propose a novel input prioritization model to determine which branch to explore, which bytes to mutate and how to mutate. Further, we use another data flow feature constraint conformance, i.e., distance of tainted variables to values expected in untouched branches, to tune the evolution direction of fuzzing.

We implemented a prototype of GREYONE and evaluated it on the LAVA data set and 19 real world programs. The results showed that it outperforms various state-of-the-art fuzzers in terms of both code coverage and vulnerability discovery. In the LAVA data set, GREYONE found all listed bugs and 336 more unlisted. In real world programs, GREYONE on average found 2.12X unique program paths and 3.09X unique bugs than state-of-the-art evolutionary fuzzers, including AFL, VUzzer, CollAFL, Angora and Honggfuzz, Moreover, GREYONE on average found 1.2X unique program paths and 1.52X unique bugs than a state-of-the-art symbolic exeuction assisted fuzzer QSYM. In total, it found 105 new security bugs, of which 41 are confirmed by CVE.

## Angora: Efficient Fuzzing by Principled Search
* [Paper](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiQq8_G_4j4AhUOAN4KHfYNDFkQFnoECAUQAQ&url=https%3A%2F%2Fweb.cs.ucdavis.edu%2F~hchen%2Fpaper%2Fchen2018angora.pdf&usg=AOvVaw3U-XA2isklvjM6rpvdE7LW)
* [Code](https://github.com/AngoraFuzzer/Angora)

**Abstract:** 
Fuzzing is a popular technique for finding software bugs. However, the performance of the state-of-the-art fuzzers leaves a lot to be desired. Fuzzers based on symbolic execution produce quality inputs but run slow, while fuzzers based on random mutation run fast but have difficulty producing quality inputs. We propose Angora, a new mutation-based fuzzer that outperforms the state-of-the-art fuzzers by a wide margin. The main goal of Angora is to increase branch coverage by solving path constraints without symbolic execution. To solve path constraints efficiently, we introduce several key techniques: scalable byte-level taint tracking, context-sensitive branch count, search based on gradient descent, and input length exploration. On the LAVA-M data set, Angora found almost all the injected bugs, found more bugs than any other fuzzer that we compared with, and found eight times as many bugs as the second-best fuzzer in the program who. Angora also found 103 bugs that the LAVA authors injected but could not trigger. We also tested Angora on eight popular, mature open source programs. Angora found 6, 52, 29, 40 and 48 new bugs in file , jhead , nm , objdump and size , respectively. We measured the coverage of Angora and evaluated how its key techniques contribute to its impressive performance.

## VUzzer: Application-aware Evolutionary Fuzzing
* [Paper](https://www.ndss-symposium.org/wp-content/uploads/2017/09/ndss2017_10-2_Rawat_paper.pdf)
* [Code](https://github.com/vusec/vuzzer)

**Abstract:** 
Fuzzing is an effective software testing technique to find bugs. Given the size and complexity of real-world applications, modern fuzzers tend to be either scalable, but not effective in exploring bugs that lie deeper in the execution, or capable of penetrating deeper in the application, but not scalable.

In this paper, we present an application-aware evolutionary fuzzing strategy that does not require any prior knowledge of the application or input format. In order to maximize coverage and explore deeper paths, we leverage control- and data-flow features based on static and dynamic analysis to infer fundamental properties of the application. This enables much faster generation of interesting inputs compared to an application-agnostic approach. We implement our fuzzing strategy in VUzzer and evaluate it on three different datasets: DARPA Grand Challenge binaries (CGC), a set of real-world applications (binary input parsers), and the recently released LAVA dataset. On all of these datasets, VUzzer yields significantly better results than state-of-the-art fuzzers, by quickly finding several existing and new bugs.