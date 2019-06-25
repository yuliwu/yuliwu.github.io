 <!-- markdownlint-disable MD029 MD010 MD030 MD032-->
# DSP Design Methodologies and Tools

## §1 Introduction [1-8][1-59]

1. Characterise embedded systems and give examples of application areas.
   * Sophisticated functionality
   * Real-time operations: Hard/soft realtime
   * Low manufacturing cost: limited memory, uP power
   * Low power: dynamic voltage/frequency scaling, software design

2. What are the advantages of using microprocessors for embedded system implementation ?
   * Flexible: can use same logic to perform many different functions
   * Simplify the design of families of products
   * Much more logic than **Custom Logic** low power winner!
   * CPU: heavily pipelined, large design teams, latest VLSI tech, lower efficiency

3. What are the major challenges in embedded system design?
   * Hardware: CPU Memory
   * Deadlines: faster hardware or cleverer Software
   * Power: Turn off unnecessary logic, reduce memory accessed
   * Work?: correct specification, implementation, real-time, data test?
   * Work on system: observability, controllability, development platform

4. What is meant by a “design methodology”?
   A procedure for designing a system.
   Helpful: Compilers, Software engineering tools, EDA tools

5. Compare top-down vs. bottom-up design methodologies.
   * Top-Down: Start from most abstract description to most detailed
   * Bottom-Up: Work from small components to big system.

6. How can system requirements be captured?
   Functional / Non-functional Requirements.
   name, purpose, inputs, outputs, functions, performance,
   manufacturing cost, power, physical size/weight

7. What is contained in a specification?
   * A more precise description of the system: should not imply a particular architecture, provides input to the architecture design process
   * May include functional & non-functional elements
   * May be executable or may be in math form for proofs

8. Define “architecture design” and “system integration”.
   * **Architecture Design**: Components(H/S) to specification, incl. functional and non-functional specs.
   * **System Intergration**: Put together the components (many bugs), have a plan for integrating components to uncover bugs quickly, test as much functionality as early ap.

---

## §2 System Design [9-21][60-106]

9. What is a **design flow** and why is it important?
   * Sequence of steps in a design methodology.
   * Maybe partially or fully automated (tools to transform & verify design)

10. Describe the **waterfall** model and its pros and cons.
    * Requirements: determine basic characteristics
    * Architechture: decompose into basic modules
    * Coding: implement and integrate
    * Testing: exercise and uncover bugs
    * Mantenance: deploy, fix bugs, upgrade
    * **Local** feedback only: may need iterations between coding & requirements etc
    * Doesn't integrate top-down and bottom-up design
    * Assumes _HW is given_
  
11. Sketch the spiral model of system development.
    * System feasibility - spec - prototype - initial sys - enhanced sys
    * Successive refinement of system
    * Provides bottom-up feedback from previous stages
    * Working through stages may take too much time

12. What is the successive refinement model ?
    * Start with mockups, move through simple systems to full-scale systems
    * Initial -> refined system

13. Sketch a hardware/software co-design flow.
	* Must architect HW & SW together: provide sufficient resources, avoid SW bottlenecks
	* Can build pieces somewhat independently, but integration is major step
	* Also requires bottom-up feedback

14. Give an example of a hierarchical design flow.
	* Embedded systems must be designed across multiple levels of abstraction: System architecture, HW/SW systems, HW/SW components
	* Often need design flows within design flows
	* [P75-76]

15. Why do companies introduce “concurrent engineering” ?
	* Large projects use many people from multiple disciplines
	* Work on several tasks at once to reduce design time
	* Feedback between tasks helps improve quality reduce number of later design problems
	* Techniques: cross-functional teams, concurrent product realization, incremental infomation sharing, integrated project management, supplier involvement, customer focus

16. What makes up a good requirements list ?
	* Correct, unambiguous, complete, verifiable, consistent, modifiable, traceable

17. Why are there different specification styles?
	* Capture functional & non-functional properties: verify correctness of spec, compare spec to implementation
	* Styles: control-oriented vs. data-oriented, textual vs. graphical
	* UML: one specification/design language

18. What is the purpose of the SDL language ?
	* Specification & Description Language
	* Used in telecommunications protocol disign
	* Event-oriented state machine model

19. Why are finite state machines insufficient for system specification ?
	* Timing annotation
	* Composite states: `OR`, `AND`

20. What is the purpose of composite (AND/OR) states in Statecharts ?
	* Reduce the size of the state trasition graph
	* Example Figure: [P90]

21. Explain the _CRC_ card methodology.
	* __Classes__, __Responsibilities__ for each classes, __Collaborators__ are other classes that work with a class
	* Informal team-oriented methodology
	* Develop an initial list of classes: simple description is OK, team members should discuss their choices
	* Write initial responsibilities/collaborators: helps to define the classes
	* Create some usage scenarios: major uses of system and classes
	* Walk through scenarios: see what works and doesn't work
	* Refine the C R C
	* Add class relationships: superclass, subclass
	* Elevator example: [P100-106]

---

## §3 Instruction Sets [22-36][107-159]

22. What characterizes a von Neumann computer architecture ?
	* __CPU + Memory__
	* Memory holds data, instructions
	* CPU fetches instructions from memory. Seperate CPU and memory distinguiashes programmable computer
	* CPU registers: program counter(PC), instruction register(IR), general-purpose registers, etc.

23. What is a Harvard architecture and why is this architecture preferred in DSP processors ?
	* [P111]
	* Can't use self-modifying code
	* Allows two simulaneous memory fetches
	* For streaming data: greater memory bandwidth, more predictable bandwidth

24. What are major differences between CISC and RISC processors ?
	* Complex ISC: many addressing modes, many operations
	* Reduced ISC: load/store, pipelined instruction execution

25. Why do we need a __programming model__ of a CPU ?
	* ISA and registers visible to the programmer (some not: IR)

26. What is the purpose of pseudo assembly instructions or assembler directives ?
	* Some assembler directives don't correspond directly to instructions: difine current add, reserve storage, constants

27. What are the main characteristics of the SHARC DSP ?
	* 32/40-Bit IEEE __Floating-Point__ Math
	* 32-Bit __Fixed-Point__ MACs with 64-Bit Product & 80-Bit accumulation
	* __Circular Buffer__ Add supported in HW
	* 32 Add pointers support 32 curcular Buffers
	* Six nested levels of __Zero-Overhead Looping__ in HW
	* Rich, algebrac assembly language syntax
	* IS supports __Conditional Arithmetic__, Bit manipulation, divide & square root, bit field deposit and extract

28. What is a modified Harvard architecture ?
	* SHARC microarchitecture
	* Program memory can be used to store some data
	* Register file connects to: Multiplier; Shifter; ALU

29. How can a C programmer access multiple memories ?
	* DM and PM in paralell
	* `R2=DM(I1,M5), R1=PM(I8,M13);`

30. What is circular memory addressing ?
	* New data constantly arrives, each datum has a limited lifetime
	* Circular buffer to hold the data stream

31. What is the purpose of conditional instructions ?
	* Instructions may be executed conditionally
	* Conditions e.g. come from Arithmetic Status (ASTAT), Mode Control (MODE1), Loop Counter

32. Describe different variants of implementing C IF-statements by machine instructions.
	* Normal and fancy
	* [148_42]

33. Which types of branches are typically supported by a processor ?
	* CALL, JUMP, RTS, RTI
	* Can be conditional
	* Add can be direct, indirect, PC-relative
	* Can be delayed or non-delayed

34. What is a delayed jump/branch ?
	* NAN

35. Why do most DSPs support zero overhead loops and how do they work ?
	* DO UNTIL instruction provides efficient looping 
	* `LCNTR=30, DO label UNTIL LCE;` 
	* Loop counter, label, loop counter expired
	* Loop length, last instruction in loop, Termination condition

36. How many instruction cycles does a typical DSP processor need for FIR filter computations ?
	* [154_48]

---

## §4 Microprocessors [37-68][160-254]

37.  How can CPUs support I/O ?
	* Typical digital interface to CPU [Fig.161]
	* Two types of instructions can support I/O: special-purpose I/O instructions; memory-mapped load/store instructions
	* Intel x86 provides `in, out` instructions
	* Most other CPUs use memory-mapped I/O
	* ARM(`LDR, STR`), SHARC(`DM`), High-level(`peek, poke`) examples [164-166]

38.  What is “busy wait” I/O ?
	* Simplest way to program device: use instructions to test when device is ready
	* Simutaneous busy/wait I/O: `while(TRUE) { ... while(peek(IN_STATUS)==0)..}`
	* Very inefficient: CPU can't do other work while testing device; hard to do simultaneous I/O

39.  How are interrupts processed ?
	* Allow a device to change the flow of control in the CPU: causes subroutine cal to handle device request
	* __Physical Interface__: CPU & device are connected by CPU bus; CPU & device handshake, device asserts interrupt request, CPU asserts interrupt acknowledge when is can handle the interrupt [Fig.171]
	* Behavior: based on subroutine call mechanism; interrupt forces next instruction to be a subroutine call to a predetermined location
	* Examples: character I/O handlers, interrupt-driven, buffer-based [174]

40.  Why should interrupts be prioritised ?
	* Determine what interrupt gets CPU first
	* __Masking__: interrupt with priority lower than current prio. is not recognized until pending interrupt is complete

41.  What is an interrupt vector ?
	* Determin what code is called for each type of interrupt
	* Allow different devices to be handled by different code
	* Interrupt vector table

42.  What is an _NMI_ ?
	* Non-Marskable Interrupt: highest priority, never masked
	* Often used for _power-down_

43.  Do interrupts incur any overhead ?
	* Handler execution time
	* Interrupt mechanism overhead
	* Register save/store
	* Pipeline-related penalties
	* Cache-related penalties
	* __Interrupt sequence__ [185]
	* Example SHARC interrupt [188-190]

44.  What is an exception ?
	* Internally detected error: e.g. devide-by-0, illegal address
	* __Synchronous__ with instruction but __unpredictable__
	* Build exception mechanism on top of interrupt mechanism
	* Are usually _prioritized_ and _vectorized_

45.  Give examples for traps or software interrupts.
	* Trap (_software interrupt_): an exception generated by an instruction: Call OS service routine; Call supervisor mode
	* ARM used SWI instruction for traps
	* SHARC offers three levels of software interrupts: Called by setting bits in IRPTL register

46. What is the purpose of a co-processor ?
	* __Added function unit__ that is called by instruction
	* Floating-point units are often strctured as co-processors e.g. in earlier Intel x_86 machines
	* Use __trap__ if co-processor instruction received, but no co-processor attached
	* ARM allows up to 16 designer-selected co-processors

47. Describe a typical system memory hierarchy.
	* Expoitation of spatioal and temporal locality
	* The closer to CPU, the _faster, more expensive, smaller_
	* __Chip__[CPU(register file), L1 Cache], __Board or multi-chip module__[L2 Cache], Main memory, hard disk, tape, nettwork ...
	* [Fig.196]

48. What are pros and cons of caches in DSP systems ?
	* Many main memory locations are mapped onto one cache entry
	* May have caches for instructions, data, data+instructions (unified)
	* Memory access time is no longer deterministic
	* __Performance benefits__: keep _frequently-accessed_ locations in fast caches, cache retrieves _more than one word_ at a time, sequential accesses are faster _after first access_

49. What is a “working set” ?
	* Set of locations used by program in a given time interval

50. Which three types of cache misses exist ?
	* _Compulsory(cold)_: location has never been accessed 
	* _Capacity_: working set is too large
	* _Conflict_: multiple locations in working set map to same cache entry

51. Derive the average memory access time in a two-level cache system.
	* $t_{av} = h_1 t_{L1} + (h_2 - h_1) t_{L2} + (1-h_2) t_{main}$

52. Why do we need a replacement policy and what is LRU ?
	* Strategy for choosing which cache entry to overwrite to make room for a new memory location
	* Random or Least-Recently-Used (LRU)

53. Define possible cache organizations.
	* __Fully-associative__: any memory location can be stored anywhere in the cache (almost never implemented)
	* __Direct-mapped__: each memory location maps onto exactly one cache entry
	* __N-way set-associative__: each memory location can go into one of N sets

54. What is the advantage of set-associative versus direct mapped caches ?
	* In general significantly different contents than direct mapped cache () larger size)

55. Describe the access procedure for a two-way set-associative cache.
	* [Link wiki](https://en.wikipedia.org/wiki/Cache_placement_policies#Set_Associative_Cache)

56. Explain different cache write strategies.
	* Write-through: immediately copy write to main memory
	* Write-back: write to main memory only when location is removed from cache

57. How does instruction pipelining work ?
	* Several instructions are executed simultaneously at different stages of completion

58. Sketch a typical pipeline architecture.
    * [27] Several instructions are executed simultaneously at different stages of completion: instruction *fetch* / instruction *decode* / *execute* / memory access / write back. *ARM, SHARC*
    * [28] Five-stage pipeline architecture

59. Define the terms “latency” and “throughput” for pipelined processors.
    * [31]
    * ***Latency**: Time it takes for an instruction to get through the pipeline;
    * **throughput**: #instructions executed per time period

60. What is a pipeline bubble and why can it occur ?
    * [32] If every step cannot be completed in the same amount of time, pipeline stalls. Branches, memory system delays etc. -> reduce utilization(throughput), increase latency
    * [33] Figure.

61. What is a branch penalty and how can it be avoided ?
	* To increase pipeline efficiency, __delayed branch mechanism__ requires `n` instructions after branch __always executed__ whether branch is executd or not.
	* SHARC supports delayed and non-delayed branches: specified by bit in branch instruction, 2 instruction branch delay slot

62. What is a __superscalar processor__ ?
	* Can execute several instructions per cycle: uses multiple pipelined data paths
	* Programs execute faster but itis harder to determine how much faster
	* Hard to use for real-time DSP applications

63. Why are power and energy concerns important for embedded systems ?
	* Heat depends on power consumption
	* Battery life depends on energy consumption
	* Power wall

64. What are sources for power consumption in a __CMOS__ circuit ?
	* __Voltage__: power consumption proportionla to V^2
	* __Toggling__: more activity means more power
	* __Leakage__: basic circuit characteristics, can be eliminatted by disconnecting power

65. What are the main methods for __CPU power saving__ ?
	* Reduce power supply voltage
	* Run at lower clock frequency
	* Disable function units with control signals when not in use
	* Disconnect parts from power supply when not in use

66. What is meant by _“static”_ and _“dynamic”_ __power management__ ?
	* Static: does not depend on CPU activity: user-activated power-down mode
	* Dynamic: based on CPU activity: disabling of function units

67. What is visualized in a power state machine ?
	* Power modes, Wakeup time, Power consumption [Fig.252]

68. Why should low-power modes in CPUs be used carefully ?
	* Going into a power-down mode costs time & energy
	* Must determine if going in to mode is worthwhile
	* Can model CPU power states with power state machine

## §5 Designing with Microprocessors [69-87][255-307]

69. What is an evaluation board ?
    Designed by CPU manufacturer or others,
    Includes CPU, Memory, some IO devices,
    Permits execution on target hardware,
    CPU manufacturer often gives out evaluation board netlist,
    Can be used as starting point for your custom board design.
    [22]

70. What are possible components of an evaluation board ?
    includes CPU, Memory, some IO devices

71. What is a bus protocol ?
    Bus connects CPU to memory & devices.
    Protocol controls communication between entities.
    Determines who gets to use the bus at any particular time.
    Govern length, style of communication.
    [28]

72. Describe a simple handshake protocol.
    * Four-cycle: two wires enq & ack (enquiry-acknowledge)
    [29,30]

73. Mention examples for popular bus protocols.
    * Timing
    [33]

74. What problems are associated with debugging embedded systems ?
    * Target system may be hard to observe,
    * Target may be hard to control,
    * May be hard to generate realistic inputs,
    * Setup sequence may be complex.
    [35]

75. How does a software debugger work ?
    A monitor program residing on the target provides basic debugger functions,
    Debugger should have a minimal footprint in memory,
    User program must be careful not to destroy debugger program,
    But debugger should be able to recover from some damage caused by user code.
    [36]

76. What is a breakpoint ?
    Allows the user to stop execution, examine system state and change state.
    Replace the breakpointed instruction with a subroutine call to the monitor program.
    [37]

77. What is an in-circuit emulator ?
    (ICE): a specially-instrumented microprocessor.
    Allows to stop execution, examine CPU state, modify registers.
    Disadvantage: microprocessor-specific
    [40]

78. Sketch the basic architecture of a logic analyser.
    A LA is an array of low-grade oscilloscopes, logic(0/1/x) display of samples signals.
    [41] Figure.

79. What is the general procedure to validate software for embedded processors ?
    Run on host system.
    Run on target system.
    Run in instruction-set simulator.
    Run on cycle-accurate simulator.
    Run in hardware/software co-simulation environment or virtual platform.
    [43]

80. What is manufacturing testing ?
    Goal: ensure that manufacturing produces defect-free copies of the design.
    Can test by comparing unit being tested to the expected behaviour. But running tests is expensive.
    Maximise confidence while minimising testing cost.
    [44]

81. Define the terms “yield”, “fault model”, and “fault coverage”.
    *Yield:* proportion of manufactured systems that work.
            Proper manufacturing maximises Yield,
            Proper testing accurately estimates Yield.
    *Field return:* defective unit that leaves the factory.
    *Fault Model:* model that predicts effects of a particular type of fault.
    *Fault Coverage:* proportion of possible faults found by a set of tests.
            Having a fault model allows us to determine fault coverage.
    [46]

82. What are major differences between software and hardware testing ?
    *Software:* no fault model. Verify implementation, not manufacturing. Simple tests work well to verify software manufacturing.
    *Hardware:* requires manufacturing tests in addition to implementation verification.
    [47]

83. Explain the stuck-at fault model. Is it realistic ?
    Stuck-at-0: output of gate is always 0.
    Stuck-at-1: output of gate is always 1.
    [48]

84. How is the stuck-at fault model used for testing combinational logic ?
    Every gate can be stuck-at-0, stuck-at-1.
    Usually test for *single stuck-at-faults*: one fault at a time, multiple faults can mask each other.
    Generate a test for a gate by controlling the gate's input & observing the gate's output through other gates.
    [49]

85. What architectural support can be provided for sequential testing ?
    A state machine is combinational logic + registers.
    Sequential testing is considerably harder:
      A single stuck-at fault affects the machine on every cycle.
      Fault behaviour on one cycle can be masked by same fault on other cycles.
    *Scan Chains:* A special register operates in two modes: normal & scan (forms an element in a shift register)
    Reduces Sequential testing to combinational testing: Loading/unloading scan chain is slow, may use partial scan.
    [50, 51]

86. What is meant by ATPG ?
    *Automatic Test Pattern Generation:* produces a set of tests given the logic structure. (exponential problem)
    Some faults may be from redundant logic.
    Timeout on a fault may mean hard-to-test or un-testable
    [52]

87. What is the purpose of boundary scan ?
    Simplifies testing of multiple chips on a board.
    Standard interface: JTAG (Joint Test Action Group), registers on pins can be configured as a scan chain.
    [53]

## §6 Program Design & Analysis  [88-142][308-407]

__P260__
88. What is a __design pattern__ ?
	* A generic description of a component tthat can be customized and used in different circumstances
	* Examples: data structures: linear lists, hash tables, etc.

89. Describe the __state machine model__ of computation and sketch an example.
	* Keeps internal state as a variable, changes state based on inputs
	* [Fig.262]

90. For which type of applications are state machine models most suitable ?
	* Uses: control-dominated code; reactive systems

91. How are state machines implemented in the C language ?
	* Current state is kept in a variable
	* State table is implemented as a switch statement: cases define states, states can test inputs
	* Switch is repeatedly evaluated in a while loop
	* `while(TTRUE){ switch(state){ case state1: ... }}`
	* `switch(state){ case A: if(in1 == 1) {x=a; state=B;} else {s=b, state=D}}`

92. Give an example for a data stream oriented design pattern.
	* Commonly used in signal processing: new data constantly arrive, each datum has a limited lifetime
	* Use a circular buffer to hold the data stream

__P308__
93. Why do compilers generally use intermediate representations (IRs) for program representation instead of source language code ?
	* Source code is not a good representation for programs: clumsy, language dependent, leaves much information implicit
	* Compilers derive IR to manipulate and optimize the program
	* [Fig.311]

94. What is __three address code__ ?
	* _Assembly-like_, yet _machine-independent_
	* At most three operands per statement
	* Split complex expressions by inserting __temporary variables__

95. What is a __basic block__ ?
	* Code with one entry and one exit

96. What is captured in a data flow graph ?
	* Describes the minimal ordering requirements on operations

97. Why is a __single assignment__ form useful ?
	* Three-address-code <-> DFG

98. What is a CDFG ?
	* __Control-Data Flow Graph__: represents control and data
	* Uses DFG as components
	* Two types of nodes: decision; data flow

99. Give examples for capturing control flow in a CDFG.
	* if-then-else, switch/case, for loop

100. Give an overview of the code generation tool chain.
	* HLL --(compile)--> assembly --(asseble)--> object codes --(link)--> executable --(load)--> Prosessors

101. What is the purpose of an assembler ?
	* Generate binary for symbolic instructions
	* Translate labels into addresses
	* Handle pseudo-ops (data, etc.)
	* Generally one-to-one translation

102. How does the assembler build symbol tables ?
	* Use program location counter (PLC) to determine address of each location
	* Scan program, keeping count of PLC
	* Addresses are generated at assembly time, not execution time
	* Efficient implementation: linear list too slow -> hash table
	* Hash function: map identifiers to table entries, which contain list of items with common hash key

103. Why does an assembler generally comprise two passes ?
	* Pass 1: collect symbolic addresses, generate symbol table
	* Pass 2: translate symbolic to real address, generate binary instructions
	* __Relative address generation__: Some label values may not be known at assembly time. Labels within the module may be kept in _relative form_. Must keep track of _external labels_ - can't generate full binary for instructions that use external labels

104. What are pseudo-operations in assembly languages ?
	* Do not generate instructions:
	* __ORG__ sets program location
	* __EQU__ generates symbol table entry without advancing PLC
	* __Data statements__ define data blocks

105. What are the tasks of a linker ?
	* Combines several object modules into a single executable module
	* Jobs: put modules in order; resolve labels across modules

106. Describe the major phases of a compiler.
	* Compilation = translation + optimization
	* HLL -(_parsing, symbol table_)-(_machine-independent optimizations_)-(_machine-dependent optimizations_)-> assembly

107. Describe a simple __CDFG-based code generation__ procedure.
	* Source code is translated into intermediate form such as CDFG
	* CDFG is transformed / optimized
	* CDFG is translated into instructions with optimization decisions
	* Instructions are further optimized

108. How does a compiler generate code for procedure calls ?
	* Need code to: call and return; pass parameters and results
	* Parameters and returns are passed on __stack__
	* Procedures with few parameters may use registers
	* Frame pointer `FP`, Stack pointer `SP`
	* ARM procedure linkage example [350]

109. Describe the addressing of composite data structure elements (arrays,structures) in compiled code.
	* 1D arrays: C array name points to 0th element
	* 2D arrays: Row-major layout
	* Structures: fields within structures are static offsets [354]

110. What are the most important objectives in DSP code optimisation ?
	* LOOP :)

111. Exemplify some simplification rules a compiler might use for code optimisation.
	* Constant folding: `8+1=9`
	* Algebraic: `a*b+a*c=a*(b*c)`
	* Strength reduction: `a*2=a<<1`

112. What is _dead code_ ?
	* `#define DEBUG 0; if(DEBUG) dbg(p1)`
	* Can be eliminated by analysis of control flow, constant folding

113. What is _procedure inlining_ ?
	* Eliminates procedure linkage overhead: parameter passing; context saving; call/return instructions (pipeline hazards)
	* Example [357]

114. Why are loop transformations highly important for code quality ?
	* 90/10 rule: 90% of execution time spent in 10% of the code (loops)
	* Goals: reduce loop overhead; increase opportunuties for pipelining; improve memory system performance

115. What are the pros and cons of _loop unrolling_ ?
	* Reduces loop overhead, enables some other optimizations

116. What is the effect of _loop fusion_ and _loop distribution_ ?
	* Fusion combines two loops into one
	* Distribution breaks one loop into two
	* Changes optimizations within loop body

117. How does _loop tiling_ work ?
	* Breaks one loop into a nest of loops
	* Changes order of accesses within array
	* Changes cache behavior 
	* Example [363]

118. What is meant by array padding ?
	* Add array elements to change mapping into cache

119. What is the task of a _register allocator_ ?
	* Choose register to hold each varuable
	* Determine lifespan of variable in the register
	* Basic case: within basic block
	* Global: within procedure

120. Describe a technique for register allocation in a basic block.
	* [366]

121. What is the relation between register allocation and graph coloring ?


122. For which types of processors is instruction scheduling important ?


123. What is represented in a reservation table ?


124. Which types of inter-instruction dependencies have to be taken into account during scheduling ?


125. What is the idea of _software pipelining_ ?
	* Schedules instructions across loop iterations
	* Reduces instruction latency in iteration i by inserting instructions from other iterations

126. Give an example for software pipelining on a DSP processor.
	* Software pipelining in SHARC [376-377]

127. Why is _instruction selection_ important in _code generation_ ?
	* May be several ways to implement an operation or sequence of operations
	* Represent operations as graphs, match possible instruction sequences onto graph

128. Outline the _template matching_ approach to instruction selection.
	* [Fig.380]

129. Compare _compilers_ to _interpreters_ and _JIT compilers_.
	* __Interpreter__: translates and executes program statements on-the-fly
	* __Just-in-Time compiler__: compiles small sections of code into instructions during program execution. E.g. Java Virtual Machine. 
	* Add performance / memory overhead

130. What makes _static prediction_ of program _execution time_ hard ?
	* Depend on: input data values; instruction/operand types; cache effects; pipelining effects

131. How can program _execution time_ be measured ?
	* __CPU simulator__: I/O may be hard; may not be totally accurate
	* __Hardware timer__: Requires board, intrumented program
	* __Logic analyzer__: Limited logic analyzer memory depth

132. Why should best, worst, and average execution times be analysed ?
	* __Average-case__: for typical data values, whatever they are
	* __Worst-case__: for any possible input set
	* __Best-case__: for any possible input set
	* Too-fast programs may cause critical races at system level

133. What is a program path ?
	* [389]

134. Which data structure helps to determine the execution times of program paths ?
	* LOOP :)

135. Describe _“code motion”_ as a _loop optimisation_.
	* [392]
	* `for(i=0; i<N*M; i++)` -> `i=0, X=N*M; if(i<X)...`

136. How does _induction variable elimination_ work ?
	* [393]
	* Rather than recompute i*M+j for each array in each iteration, share induction variable between arrays, increment at end of loop body

137. Why are both power and energy optimisation important for DSP systems ?
	* __Energy__: ability to do work: most important in battery-powered systems
	* __Power__: energy per unit time: important even in wall-plug systems: power becomes heat

138. How can the energy consumption of a program be measured ?
	* Execute a small loop, measure current

139. What types of CPU instructions tend to consume most energy ?
	* Memory

140. Mention some general recipes for minimizing _program energy consumption_.
	* __Cache behavior__: cache too small: program burns too much energy on external memory accesses; cach too large: cache itself burns too much energy
	* First-order optimization: high performance = low energy
	* Most instructions do not show significant variances in power consumption
	* Use registers efficiently
	* Identify and eliminate cache conflicts
	* Moderate loop unrolling eliminates some loop overhead instructions
	* Eliminate pipeline stalls
	* Inlining procedures may help: reduces linkage overhead, but may increase cache conflicts

141. What are techniques for _program size optimisation_ ?
	* Reduce HW cost of memory and power consumption of memory units
	* __Reduce data size__: reuse constants, variables, data buffers in different parts of code: requires careful verification of correctness
	* Generate data using instructions
	* __Reduce code size__: Avoid function inlining, choose CPU with compact instructions, use specialized instructions where possible

142. What are pros and cons of code compression ?
	* Use statistical compression after linking to reduce code size
	* Decompress on-the-fly

## §7 VLSIK Implementation [143-153][408-441]

1.   What are advantages of DSP system implementation in VLSI technology ?


2.   What is described by Moore ́s Law ?


3.   How many transistors can be integrated on today ́s VLSI systems ?


4.   What are the major cost factors for integrated circuits ?


5.   Sketch the Y-chart of the VLSI design process.


6.   Describe the concept of hierarchical VLSI design.


7.   Exemplify the different abstraction levels in VLSI design.


8.   What is meant by “digital abstraction” of a circuit ?


9.   Compare top-down vs. bottom-up design methodologies.


10.  What is “back annotation” ?


11.  What is the difference between design validation and manufacturing test ?


## §8 RTL Components [154-159][442-460]

1.   What is the functionality of a barrel shifter ?


2.   Sketch the architecture of a barrel shifter.


3.   What is the functionality of a full adder ?


4.   What is the critical path in a ripple-carry adder ?


5.   Describe a carry-lookahead adder.


6.   Sketch a bit-serial adder.


## §9.1 Architecture and Chip Design [160-][461-517]

1.   What is a register-transfer (RT) system ?


2.   Why is it useful to separate a system into data path and controller ?


3.   How are conditionals modelled by RT components ?


4.   What is an ASM chart ?


5.   What is meant by “function unit sharing” ?


6.   What is the relation between ASMs and Moore/Mealy automata ?


7.   How do ASMs help in data path and controller partitioning ?


8.   What is the purpose of hardware description languages (HDLs) ?


9.   Define “compiled code simulation” and “event-driven simulation”.


10.  Describe the use of the timewheel data structure in simulation.


11.  Give examples for structural and behavioural hardware models.


12.  What is a testbench ?


13.  What is meant by a “synthesis subset” of an HDL ?


14.  What is RT synthesis ?


15.  Define the term high-level synthesis (or behavioral synthesis).


16.  What is ASAP/ALAP scheduling ?


17.  What is the relation between ASAP/ALAP and critical paths in data flow graphs ?


18.  What is the impact of operation chaining on the cycle time of a design ?


19.  Give an example of non-additive delay in operation chaining.


20.  Describe the major steps of high-level synthesis.


21.  What are the advantages of hardware description languages (HDLs) ?


22.  What is the simulation semantics of VHDL processes ?


23.  What is an entity in VHDL ?


24.  Why can a VHDL entity have multiple architectures ?


25.  Are there differences in the use of HDLs like VHDL or Verilog for synthesis and simulation purposes ?


26.  How does a VHDL testbench work ?


27.  Sketch a sample VLSI design flow.


28.  What are methods to estimate speed or area of designs at early stages ?


29.  What is the purpose of floorplanning ?


30.  What is meant by state assignment in logic synthesis ?


31.  What are the main application areas for full custom layout ?


32.  What is covered by design validation ?


33.  What is meant by tapeout ?


34.  Sketch a basic CPU data path.


35.  What influences design decisions about the number of register file ports ?


36.  What is a wiring plan ?


37.  What is a bricks-and-mortar floorplan ?


38.  What is the difference between channel and switchbox routing ?


39.  Is the definition of routing channels unique ?


40.  What is a channel graph and what is it used for ?


41.  What is a “windmill” floorplan ?


42.  When is a floorplan called “sliceable” ?


43.  What is global routing ?


44.  How does line probe routing work ?


45.  Why is switchbox routing more difficult than channel routing ?


46.  What is the purpose of interchange languages in CAD systems ?


47.  What is the difference between a data base and a translator based approach to design interchange ?


48.  What is back annotation ?


49.  What are the major phases of layout synthesis ?


50.  How can you estimate the placement quality before actual wiring ?


51.  What are the Euclidian and Manhattan wire length measures ?


52.  What is meant by “placement by partitioning” ?


53.  Describe the idea of min-cut bisecting partitioning.


54.  What is the main advantage of the Kernighan-Lin partitioning algorithm ?


55.  What is the difference between global and detailed routing ?


56.  Why is net ordering important ?


57.  Why are Steiner trees of interest in routing ?


58.  Describe Lee ́s maze routing algorithm.


59.  Where does the channel routing problem occur ?


60.  Describe the left-edge channel routing algorithm and its limitations.


61.  What is a “dogleg” in channel routing ?


62.  What are the main ideas of the Rivest-Fiduccia channel router ?


63.  Describe the scan line algorithm for Boolean mask operations. What is it used for ?


64.  What is a Boolean function and how can it be represented ?


65.  What is a “complete” set of functions ?


66.  What tasks are involved in logic synthesis ?


67.  Why is library binding required ?


68.  What are methods for technology-independent logic optimisation ?


69.  Define the terms “cover” and “cube”.


70.  How can covers be minimized ?


71.  How can don ́t cares be exploited during logic optimisation ?


72.  Describe a technology mapping procedure.


73.  What is a fault model used for ?


74.  Describe the stuck-at fault model.


75.  What is the general procedure for combinational logic testing ?


76.  Describe the main ideas of the PODEM algorithm for fault propagation.

