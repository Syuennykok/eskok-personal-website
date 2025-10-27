---
created: 2025-10-27T15:42
updated: 2025-10-27T15:44
title: "Reading Notes: Building ASIPs - The MESCAL Methodology"
tags:
  - ReadingNotes
---
This book can be find [here](https://link.springer.com/book/10.1007/b136892).
# Contents

1. [Introduction and Motivation](#Introduction%20and%20Motivation)
	1. [Design Discontinuity](#Design%20Discontinuity)
	2. [Makimoto's Wave](#Makimoto's%20Wave)
	3. [A Methodology for ASIP Design](#A%20Methodology%20for%20ASIP%20Design)
2. Judiciously Using Benchmarking
3. [Inclusively Identifying the Architectural Space](#Inclusively%20Identifying%20the%20Architectural%20Space)
4. [Efficiently Describing and Evaluating the ASIPs](#Efficiently%20Describing%20and%20Evaluating%20the%20ASIPs)
5. [Comprehensively Exploring the Design Space](#Comprehensively%20Exploring%20the%20Design%20Space)
6. Successfully Deploying the ASIP
7. Designing and Modeling MPSoC Processors and Communication Architectures
8. Commercial Configurable Processors and the MESCAL Approach
---
# Introduction and Motivation

## Design Discontinuity

- Characteristics
	- commercial push to achieve higher levels of productivity due to Moore's Law
	- Foundation of Design Discontinuity is the creation of a base level, or platform whose functional and physical properties are well understood.
	- a higher-level abstraction allows details of the foundation to be abstracted away
	- a supportive methodology with below elements
		- a *design-entry* approach that offers 10x productivity improvement
		- a *functional verification* approach that offers 10-100x speed-up in verification
		- an *implementation* approach that is predictable and reliable

## Makimoto's Wave

![](attachments/Pasted%20image%2020250619105147.png)

- There is a continuous battle between the drive for customization and standardization (period about 10 years)
	- forces for standardization
		- new device structures
		- new architectures
		- software development innovation
	- forces for customization
		- improved design automation
		- improved computer-aided manufacturing
		- improved computer-aided testing
- Takeaways
	- When innovations in devices, architectures, and software development are greater that innovations in design automation, design for manufacturing, and technology-CAD, then standard solution will predominate.
- new version from internet
	- ![](attachments/Pasted%20image%2020250619105725.png)

## A Methodology for ASIP Design

- MESCAL research project
	- focus on developing a coherent methodology and set of supporting tools for the development and deployment of programmable platforms
- Five element methodology (not sequential)
	- **judiciously using benchmarking**
		- guideline for benchmarks
			- selected with careful application domain analysis
			- indicative of real-world performance
			- representative of both the environment and the functionality
			- communicated with a precise specification
		- noted that kernel level benchmarks might potentially hide performance bottlenecks
	- **inclusively identify the architectural space**
		- restricted design space may abandon many promising architecture
	- **efficiently describe and evaluate the ASIPs**
		- requires a software mapping and evaluation environment for the design metrics
		- what we have now: OpenASIP or ASIP Designer
	- **comprehensively explore the design space**
		- design space exploration is a feedback driven process
		- tool driven the ability to exploration
	- **successfully deploy the ASIP**

---

# Inclusively Identifying the Architectural Space

- design axes, in aspect of two classes of ASIPs
	- ISA based :luc_alert_octagon:control flow
		- parallel processing
			- hardware is inherently parallel
			- PE level
				- pipelined
				- symmetric: perform similar functionality
			- Instruction level
				- at compile time: VLIW
				- at run time: superscalar
			- word/bit level
		- special purpose hardware
			- co-processors
				- triggered by a PE 💡TTA
				- does not have an instruction decode unit ❓
				- :luc_alert_octagon:operations cumbersome to execute within ISA
			- special function units
				- computational block that computes result within the pipeline stage of PE
				- :luc_alert_octagon:operations which it would take a large number of cycles for the computation with standard ISA
		- Memory architectures
			- multi-threading
				- allow hardware to be used for processing other streams
				- require dedicated hardware support
			- memory management
				- eliminate the overhead of operating system calls
			- task-specific memories
		- On-chip communication mechanisms
			- topology
			- connectivity
			- link type
			- programmability
		- support for peripherals
			- network interfaces
			- memory interfaces
			- system extension interfaces
			- test and debug interfaces
			- common standard interfaces
			- specialized auxiliary interfaces
		- Programmable hardware based :luc_alert_octagon:data flow
			- Granularity of programmability
				- fine grain
				- coarse grain
			- Time of programming
				- static reconfiguration
				- dynamic reconfiguration
- closer look into subspaces
	- memory design space
		- Dominant Memory Access Patterns
		- Memory Design Space Selection
			- classifies the memory access patterns of an application into several compatible groups
				- profiling
				- compiler analysis
			- selects the types of memory hardware units that efficiently support
			- indicates a selection of mapping strategies
			- mapping strategies combined with the memory hardware choice form the overall memory design space
		- Memory Design Space Complexity
			- ![](attachments/Pasted%20image%2020250707075011.png)
	- Peripheral Design Space
		- Impact of Peripherals on programmable platforms
		- Implementation Techniques for peripherals
			- Individual IP
			- Multiple Macros/pin sharing
			- Parameterizable Peripherals
			- Programmable Interfaces
			- Multiple Channels
			- Generic interfaces

---
# Efficiently Describing and Evaluating the ASIPs

- Some fundamental
	- Architecture Description Languages (ADLs)
		- Behavioral ADLs - instruction semantics
			- nML
			- ISDL
			- CSDL
		- Mixed ADL - instruction semantic + micro-architectural structure
			- FlexWare
			- Maril
			- LISA
		- Stylized HDLs - extract instruction, generate compiler and simulator, synthesize design
			- MIMOLA 
	- Hardware Description Languages (HDLs)
		- Verilog
		- VHDL
		- SystemC
- Recipe for Developing ASIPs
	- Design Principles
		- Strict Models: Formally defined models ease verification and correctness of the design
		- Separation of Concerns: Different aspects of the design should be handled independently
		- Correct by Construction: Different aspects of a design are kept consistent in underlying formal models
	- Example: Tipi's Implementation
		- Correct by Construction Design
		- Multi-view Design
		- Operation-level Design
- Tipi's Design Flow
	- ![](attachments/Pasted%20image%2020250707105343.png)
	- Multi-view Operation-level Design
		- Architecture View: provides the ability to describe datapath
		- Operation View: provides the ability to extract configurations of datapath
		- Simulation View: provides capability to generate a simulator
		- Assembly View: Generate assemble of operation set
		- Hardware View: Generate hardware and provide combinational timing feedback
- Memory System Design
	- Goal: allow designers to comprehensively explore memory space at architecture level by giving facilities for rapid construction and rapid feedback
---
# Comprehensively Exploring the Design Space

- Design space exploration
	- an iterative procedure
	- How can a single design point be evaluated?
	- How can the design space be covered during the exploration process?
- Problem Space
- Solution/Objective Space
- Pareto Criterion for Dominance