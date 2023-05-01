Download Link: https://assignmentchef.com/product/solved-caa-homework-5
<br>
<h1>1           Programming</h1>

<strong>The programming part is only for practice, you have no need to hand in this part of this homework.</strong>

<strong>But if you are interested in this part, it is free to email TAs to have some discussion.</strong>

In this homework, we are going to examine the cache effect. The tool we’ll use is <a href="https://github.com/chipsalliance/rocket-chip">rocket-chip</a><a href="https://github.com/chipsalliance/rocket-chip">. </a>You can either build rocket-chip yourself or use the image provided

docker pull ntuca2020/hw5 # size ~ 8.28G docker run –name=test -it ntuca2020/hw5 cd /root ls

Folder structure for this homework:

<table width="460">

 <tbody>

  <tr>

   <td colspan="2" width="237">emulator/</td>

   <td width="223">// link to rocket-chip emulator</td>

  </tr>

  <tr>

   <td colspan="2" width="237">|– benchmarks/</td>

   <td width="223">// link to riscv-tests benchmark</td>

  </tr>

  <tr>

   <td width="49">|</td>

   <td width="188">|– Makefile</td>

   <td width="223">// complie all benchmarks</td>

  </tr>

  <tr>

   <td width="49">|</td>

   <td width="188">|– qsort/</td>

   <td width="223">// qsort benchmark folder</td>

  </tr>

  <tr>

   <td width="49">|</td>

   <td width="188">|– qsort.riscv</td>

   <td width="223">// riscv executable</td>

  </tr>

  <tr>

   <td width="49">|</td>

   <td width="188">|– qsort.riscv.dump</td>

   <td width="223">// objdump riscv executable</td>

  </tr>

  <tr>

   <td width="49">|</td>

   <td width="188">|– mt-matmul/</td>

   <td width="223">// mt-matmul benchmark</td>

  </tr>

  <tr>

   <td width="49">|</td>

   <td width="188">|– mt-matmul.riscv</td>

   <td width="223">// riscv executable</td>

  </tr>

  <tr>

   <td width="49">|</td>

   <td width="188">|– mt-matmul.riscv.dump</td>

   <td width="223">// objdump riscv executable</td>

  </tr>

  <tr>

   <td width="49">|</td>

   <td width="188">|– mt-matmul_4/</td>

   <td width="223">// for part2</td>

  </tr>

  <tr>

   <td width="49">|</td>

   <td width="188">|                ‘– matmul.c</td>

   <td width="223">&lt;– need to be handed in</td>

  </tr>

  <tr>

   <td width="49">|</td>

   <td width="188">|– mt-matmul_4.riscv</td>

   <td width="223">// riscv executable</td>

  </tr>

 </tbody>

</table>

|                     |– mt-matmul_4.riscv.dump // objdump riscv executable

|             |– …                                                     // other benchmarks

|           ‘– common

|                           |– …

|                           ‘– crt.S                                          // specify number of cores available

|– system/                                                            // link to rocket-chip system

|              |– test.scala                                            // first part SoC settings

|            |– HW5.scala                                                                   &lt;– used for matrix multiplication and need to be handed in

|              ‘– *.scala                                                   // other default scala settings

|– build.sh                                                          // build all settings

|– test.sh                                                            // test all settings

|– spike_test.sh                                                 // can test on spike first

|– Config1                                                        // Configuration1

|– generated-src_Config1        // Layout, RTL, mappings, dts, etc, for Config1 |– …

‘– Makefile                                                          // Build the configuration

<h2>Part 1: Observing cache behavior</h2>

Run test.sh and fill in cycle counts for each benchmark and each setting in the following form

Answer the following questions (answers should be based your observation on the cache configurations and the program behavior)

<ul>

 <li>Why are (1) the same or different?</li>

 <li>Why are (2) the same or different?</li>

 <li>Why are (3) the same or different?</li>

 <li>Why are (4) the same or different?</li>

 <li>Why are (5) the same or different?</li>

 <li>See the pmp.c in /root/emulator/benchmarks/pmp, what does this program want to do? And how does it make it?</li>

 <li>Change the number of cores available in crt.S file (line 125) in /root/emulator/benchmarks/common and recompile the mt-matmul program (for this question, matrix size is 32×32).

  <ul>

   <li>Report the cycle count of configuration17 on 1-core, configuration19 on 2-core, and configuration20 on 4-core (1%)</li>

   <li>Describe whether the cycle count decreases linearly, why or why not.</li>

  </ul></li>

</ul>

<table width="523">

 <tbody>

  <tr>

   <td width="115"></td>

   <td width="74">dhrystone</td>

   <td width="60">median</td>

   <td width="65">multiply</td>

   <td width="46">qsort</td>

   <td width="57">rsort</td>

   <td width="55">towers</td>

   <td width="51">vvadd</td>

  </tr>

  <tr>

   <td width="115">Configuration 1</td>

   <td width="74">(4)</td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57">(3)</td>

   <td width="55"></td>

   <td width="51">(1)</td>

  </tr>

  <tr>

   <td width="115">Configuration 2</td>

   <td width="74"></td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57"></td>

   <td width="55"></td>

   <td width="51">(1)</td>

  </tr>

  <tr>

   <td width="115">Configuration 3</td>

   <td width="74"></td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57">(2),(3)</td>

   <td width="55"></td>

   <td width="51"></td>

  </tr>

  <tr>

   <td width="115">Configuration 4</td>

   <td width="74"></td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57">(2)</td>

   <td width="55"></td>

   <td width="51"></td>

  </tr>

  <tr>

   <td width="115">Configuration 5</td>

   <td width="74"></td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57"></td>

   <td width="55"></td>

   <td width="51"></td>

  </tr>

  <tr>

   <td width="115">Configuration 6</td>

   <td width="74">(4)</td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57"></td>

   <td width="55"></td>

   <td width="51"></td>

  </tr>

  <tr>

   <td width="115">Configuration 7</td>

   <td width="74">(4)</td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57"></td>

   <td width="55"></td>

   <td width="51"></td>

  </tr>

  <tr>

   <td width="115">Configuration 8</td>

   <td width="74"></td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57"></td>

   <td width="55"></td>

   <td width="51"></td>

  </tr>

  <tr>

   <td width="115">Configuration 9</td>

   <td width="74"></td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57"></td>

   <td width="55"></td>

   <td width="51"></td>

  </tr>

  <tr>

   <td width="115">Configuration 10</td>

   <td width="74"></td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57"></td>

   <td width="55"></td>

   <td width="51"></td>

  </tr>

  <tr>

   <td width="115">Configuration 11</td>

   <td width="74"></td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57"></td>

   <td width="55"></td>

   <td width="51"></td>

  </tr>

  <tr>

   <td width="115">Configuration 12</td>

   <td width="74">(5)</td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57"></td>

   <td width="55"></td>

   <td width="51"></td>

  </tr>

  <tr>

   <td width="115">Configuration 13</td>

   <td width="74">(5)</td>

   <td width="60"></td>

   <td width="65"></td>

   <td width="46"></td>

   <td width="57"></td>

   <td width="55"></td>

   <td width="51"></td>

  </tr>

 </tbody>

</table>

Tabelle 1: Benchmark on different configurations

<h2>Part 2: Cache and matrix multiplication</h2>

In this part, we revisit the matrix multiplication. You are asked to implement <strong>64×64 matrix multiplication </strong>on <strong>4-core, 128-B L1-D$, 128-B L1-I$ </strong>(no L2). The size of cache is fixed so that you can only change way-set setting in L1.

Change the dataset in <strong>/root/emulator/benchmarks/mt-matmul/mt matmul.c </strong>to the one with 64×64 (<strong>dataset2.h</strong>). The cache setting is specified in <strong>/root/emulator/system/HW5.scala </strong>and you can build the simulator using

make -j8 CONFIG=freechips.rocketchip.system.HW5Config

in /root/emulator.

The matrix multiplication program is located at <strong>/root/emulator/benchmarks/mt-matmul/matmul.c</strong>. Each thread will enter this function with its thread id and local storage (<strong>128KB</strong>) and exit once the task is finished. You may want to see the files under mt-matmul/ and common/.

The distribution of the workload and the cache behavior should be considered when you implement matrix multiplication. We will score based on the cycle count coming out from your <strong>HW5.scala </strong>and <strong>matmul.c</strong>.

Grading:

<ul>

 <li>Correctness</li>

 <li>Based on cycle count

  <ul>

   <li>Ranking: Top 5</li>

   <li>Ranking: 6∼20</li>

   <li>Ranking: 21∼40</li>

   <li>Ranking: 41∼80</li>

   <li>Ranking: <em>&gt; </em>80</li>

  </ul></li>

 <li>Report on how you make your matrix multiplication and maybe some cache miss rate statistics using spike</li>

</ul>

<h2>Architecture and Security (0%)</h2>

Although it is important to design a high-performance architecture, it is also crucial to design a secure architecture. Read the <a href="https://dl.acm.org/doi/pdf/10.1145/3399742">“Spectre Attacks: Exploiting Speculative Execution”</a> (or you may want to reference the original paper <a href="https://arxiv.org/pdf/1801.01203.pdf">here</a><a href="https://arxiv.org/pdf/1801.01203.pdf">)</a> and answer the questions.

<ul>

 <li>How to perform “exploiting conditional branch misprediction” attack?</li>

 <li>How to perform “poisoning indirect branches” attack?</li>

 <li>How to mitigate Spectre Attacks? (at least 3 methods)</li>

</ul>