# 1-bit full adder using CMOS mirror logic
  * [Introduction](#introduction)
  * [Working](#working)
  * [Reference Circuit](#referenceCircuit)
  * [Implementation in synopsis](# implementation in synopsis)
  * [Netlist](#netlist)
  * [Simulation result](#simulation result)
  * [Conclusion](#conclusion)
  * [References](#references)
  * [Acknowledgement](#acknowledgement)
  * [Author](#author)


## Introduction
Full Adder is the adder which adds three inputs and produces two outputs. The first two inputs are A and B and the third input is an input carry as Cin The output carry is designated as Cout and the normal output is designated as SUM
## Working
we can design full adder using static cmos logic but it takes nearly 40 transistors to build it. By using the simple current mirror logic, we can reduce the total number of transistors and power consumption. Indeed, compared to static CMOS logic, it exhibits a very low switching noise, a very high speed and a better power efficiency at high operating frequencies other than a significantly lower sensitivity to process variability. These features are exploited in current high resolution mixed signal Integrated Circuits (ICs), high speed arithmetic cores, multiplexing/demultiplexing ICs for optical fibre communication systems and RF circuits [2]. To implement mirror logic the pull up and pull-down network of carry circuit and sum circuit should be same, with this we can reduce the number of transistors used to build the circuit to 28 and the total power consumption in the circuit. As the full adder equations obeys duality and inversion, we can convert equations of 1-bit full adder  to the following to implement mirror logic easily.
Cout = AB + Cin (A+B)  (A+B) (Cin+AB)
Sum=ABCin+Cout(A+B+Cin)  (A+B+Cin) (Cout+ABCin)

## Reference Circuit Diagram
<img width="1371" alt="Reference_Ckt" src="https://user-images.githubusercontent.com/59500283/155388072-53c63be1-69c2-4d84-90e7-4cb95889fb67.png">
![alt text](https://github.com/[username]/[reponame]/blob/[branch]/image.jpg?raw=true)

## Implementation in synopsis

## Netlist
*  Generated for: PrimeSim
*  Design library name: cmos_mirror
*  Design cell name: cmos_mirror_logic_tb
*  Design view name: schematic
.lib '/PDK/SAED_PDK32nm/hspice/saed32nm.lib' TT
*Custom Compiler Version S-2021.09
*Thu Feb 24 04:48:36 2022
.global gnd!
********************************************************************************
* Library          : cmos_mirror
* Cell             : cmos_mirror_logic
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
.subckt cmos_mirror_logic cin cout va vb vd gn sum
xm25 sum net78 vd vd p105 w=0.1u l=0.03u nf=1 m=1
xm24 cout net125 vd vd p105 w=0.1u l=0.03u nf=1 m=1
xm23 vd va net103 vd p105 w=0.1u l=0.03u nf=1 m=1
xm22 net103 vb net99 vd p105 w=0.1u l=0.03u nf=1 m=1
xm21 net99 cin net78 vd p105 w=0.1u l=0.03u nf=1 m=1
xm20 net156 cin vd vd p105 w=0.1u l=0.03u nf=1 m=1
xm19 net156 va vd vd p105 w=0.1u l=0.03u nf=1 m=1
xm18 net156 vb vd vd p105 w=0.1u l=0.03u nf=1 m=1
xm17 net78 net125 net156 vd p105 w=0.1u l=0.03u nf=1 m=1
xm4 net125 cin net41 vd p105 w=0.1u l=0.03u nf=1 m=1
xm3 net14 vb net125 vd p105 w=0.1u l=0.03u nf=1 m=1
xm2 vd va net14 vd p105 w=0.1u l=0.03u nf=1 m=1
xm1 vd vb net41 vd p105 w=0.1u l=0.03u nf=1 m=1
xm0 net41 va vd vd p105 w=0.1u l=0.03u nf=1 m=1
xm27 sum net78 gn gn n105 w=0.1u l=0.03u nf=1 m=1
xm26 cout net125 gn gn n105 w=0.1u l=0.03u nf=1 m=1
xm16 gn cin net70 gn n105 w=0.1u l=0.03u nf=1 m=1
xm15 net70 vb net66 gn n105 w=0.1u l=0.03u nf=1 m=1
xm14 net66 va net78 gn n105 w=0.1u l=0.03u nf=1 m=1
xm13 net78 net125 net158 gn n105 w=0.1u l=0.03u nf=1 m=1
xm12 net158 cin gn gn n105 w=0.1u l=0.03u nf=1 m=1
xm11 net158 vb gn gn n105 w=0.1u l=0.03u nf=1 m=1
xm10 net158 va gn gn n105 w=0.1u l=0.03u nf=1 m=1
xm9 gn vb net38 gn n105 w=0.1u l=0.03u nf=1 m=1
xm8 net38 va net125 gn n105 w=0.1u l=0.03u nf=1 m=1
xm7 gn vb net30 gn n105 w=0.1u l=0.03u nf=1 m=1
xm6 net30 va gn gn n105 w=0.1u l=0.03u nf=1 m=1
xm5 net125 cin net30 gn n105 w=0.1u l=0.03u nf=1 m=1
.ends cmos_mirror_logic

********************************************************************************
* Library          : cmos_mirror
* Cell             : cmos_mirror_logic_tb
* View             : schematic
* View Search List : hspice hspiceD schematic spice veriloga
* View Stop List   : hspice hspiceD
********************************************************************************
xi0 cin cout va vb net8 gnd! sum cmos_mirror_logic
v1 net8 gnd! dc=1.05
v9 vb gnd! dc=0 pulse ( 0 1.05 2u 0.1u 0.1u 5u 10u )
v8 va gnd! dc=0 pulse ( 0 1.05 1u 0.1u 0.1u 5u 10u )
v7 cin gnd! dc=0 pulse ( 0 1.05 0 0.1u 0.1u 5u 10u )
c11 cout gnd! c=1p
c10 sum gnd! c=1p
.tran '1u' '20u' name=tran
.option primesim_remove_probe_prefix = 0
.probe v(*) i(*) level=1
.probe tran v(cin) v(cout) v(va) v(vb) v(sum)

.temp 25
.option primesim_output=wdf
.option parhier = LOCAL
.end


## Conclusion
Thus, the implementation of 1-bit full adder is done using CMOS mirror logic, the output is verified using the synopsis custom compiler.

## References 
1. [1] https://youtu.be/BflzLRjsECM 
2. [2] H. Lee and G. E. Sobelman, 1997, “A New Low Voltage Full Adder Circuit,” in IEEE proc. 7th great lakes symosium vlsi, pp. 88–92.
3. [3]http://www.ijarse.com/images/fullpdf/1444293364_4_Re search_Paper.pdf
## Acknowledgement
1. Kunal Ghosh, Co-founder, VSD Corp. Pvt. Ltd. - kunalpghosh@gmail.com
2. Chinmay panda, IIT Hyderabad
3. Indian Institute Of Technology (IIT), Hyderabad
4. Synopsys

