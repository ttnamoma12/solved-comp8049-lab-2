Download Link: https://assignmentchef.com/product/solved-comp8049-lab-2
<br>
<strong>Question 1</strong>

The attached game-lab directory which contains a basic “game” code for the versatilepb board. Modify the code to allow the user to move pacman around the versatilepb board screen without leaving a trail. The user can use keys such as s,d,e and w to move pacman. You need to use the arm cross compiler and the mk script.

<strong>Question 2</strong>

Give a brief overview of the clang generated Abstract Syntax Tree (AST) for the while loop of the attached t2.c file. The attached t2.ast file from line 25 to line 53 shows a dump of the WhileStmt node and its children which corresponds to the while loop.  The t2.ast file was generated using:

clang-check -ast-dump t2.c –extra-arg=”-fno-color-diagnostics” &gt;t2.ast

Clang/LLVM is a framework for the compilation and analysis of source code written is several different programming languages. Clang provides many tools for the manipulation of its ASTs. See the video linked in this tutorial for details <a href="https://jonasdevlieghere.com/understanding-the-clang-ast/">https://jonasdevlieghere.com/understanding-the-clang-ast/</a><a href="https://jonasdevlieghere.com/understanding-the-clang-ast/">.</a>

In this case we use clang to generate an AST for a given simple c function fred(). We use the -ast-dump command line argument to generate a textual representation of the AST, which is stored in the file t2.ast. Each node in the AST models a particular language construct. For example, the VarDecl class models a c declaration of a variable.

For instance, the c statement in the file t1.c:

int i,j=0; is modeled in the AST as two VarDecl nodes and one IntegerLiteral node which are in the t2.ast from line 15 to line 18:

-VarDecl 0x1c08820 &lt;col:1, col:5&gt; col:5 used i ‘int’

-VarDecl 0x1c08890 &lt;col:1, col:9&gt; col:7 used j ‘int’ cinit

-IntegerLiteral 0x1c088f0 &lt;col:9&gt; ‘int’ 0

If a c variable is used in an expression in t2.c, the AST will have a corresponding DeclRefExpr node to model that use.

For example, the c statement:

j = 0; will be modeled using the following AST nodes (dumped using the -ast-dump flag to the compiler):

BinaryOperator 0x1c089f8 &lt;line:4:1, col:3&gt; ‘int’ ‘=’

| |-DeclRefExpr 0x1c089b0 &lt;col:1&gt; ‘int’ lvalue Var 0x1c08890 ‘j’ ‘int’     | `-IntegerLiteral 0x1c089d8 &lt;col:3&gt; ‘int’ 0




<strong>Question 3</strong>

The attached code (testbench.c and peak.c) is a testbench and a state machine implementation of the peak constraint http://sofdem.github.io/gccat/gccat/Cpeak.html. You are to write a c function which implements the “valley” constraint and a second c function which implements the “increasing peak” constraint. You are to update the testbench to test these new constraints.

A constraint is just a form of if statement. The <em>valley</em> and <em>increasing peak</em> constraints are defined here: http://sofdem.github.io/gccat/gccat/Cvalley.html http://sofdem.github.io/gccat/gccat/Cincreasing_peak.html.

The <em>valley</em> constraint is a simple state machine, which is practically identical to the <em>peak</em> constraint. An implementation of the peak constraint state machine is given in peak.c. See figure 5.417.3 below for the valley constraint state machine.

The scope of this lab is the design of a hardware accelerator for detecting anomalies in time series data. These anomalies are defined by the user in terms of constraints which can be used to detect combinations of spikes and/or troughs with particular characteristics. Such accelerators could be deployed for example into a nuclear power facility to quickly detect fluctuations in the sensor readings from the instrumentation control systems of the plant. <a href="http://www.mcobject.com/radico">http://www.mcobject.com/ </a><a href="http://www.mcobject.com/radico">radico</a><a href="http://www.mcobject.com/radico">,</a> https://www.iaea.org/NuclearPower/IandC/index.html

The different constraints  can be combined to form more complex filters. See for example here <a href="https://www.doulos.com/knowhow/systemc/tutorial/modules_and_processes/">https://www.doulos.com/knowhow/systemc/tutorial/modules_and_processes/</a> where a systemc model of  an EXOR gate is implemented using four NAND gates.

The code (testbench.c and peak.c) is a high level data flow model/design that can be synthesised directly onto a FPGA using for example vivado HLS. <a href="https://www.xilinx.com/video/hardware/getting-started-vivado-high-level-synthesis.html">https://www.xilinx.com/video/hardware/getting-started-vivado-high-level</a><a href="https://www.xilinx.com/video/hardware/getting-started-vivado-high-level-synthesis.html">synthesis.html</a>