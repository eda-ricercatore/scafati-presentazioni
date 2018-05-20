# The Hackin' Aggies

Repository for Hack@DAC 2018 contest.

It will become public at the end of phase 1 of the contest, which is tentatively May 1.





#	Notes

##	Comments on JTAG-based Security Bugs

+ buggy_soc/buggy_soc/tb/tb_jtag_pkg.sv
	- This is the closest match to the TAP controller in my presentation slides,
		which should indicate the security bug that allows us to switch from
		normal mode to test mode, without going through the reset mode.
	- \cite{Majeric2017} has references on how to exploit this security bug to
		dump or snoop data.
	- However, to inject faults for specific software (including operating systems),
		see \cite{Majeric2017} for more details.



+ \cite{Rosenfeld2010} shows some security bugs of JTAG and how to mitigate
	them.
+ The active-low input test reset, **TRST\***, to the advanced debugging unit
	(ADU) is optional \cite[\S10.2.2, pp. 562]{Wang2006b}.
	- Also, another input to the ADU, test mode select (**TMS**), is the only
		input to the test access port (TAP) controller that controls the TAP
		\cite[\S10.2.3, pp. 565]{Wang2006b}.
	- Apart from **TMS**, the only other required input for the TAP controller is
		the test clock input (**TCK**) \cite[\S10.2.3, pp. 564-565]{Wang2006b}.
	- Hence, the **TMS** input is used to determine the next state of the TAP
		controller \cite[\S10.2.5, pp. 567]{Wang2006b}. 
	- From the finite state machine (FSM) of the TAP controller
		\cite[\S10.2.5, pp. 567]{Wang2006b}, a low **TRST\*** input brings the
		TAP controller to the **Test–Logic–Reset** state, in which "the
		boundary-scan circuitry is disabled" \cite[\S10.2.5, pp. 568]{Wang2006b}.
	- In addition, from the FSM of the TAP controller
		\cite[\S10.2.5, pp. 567]{Wang2006b}, a low **TMS** input brings the
		TAP controller from the **Test–Logic–Reset** state to the
		**Run-Test/Idle** state, without having to reset the scan registers.

+ In \S4.1, Table 20, page 37 of the "Advanced Debug Interface" report by
	Mr.  Nathan Yawn shows some states of the TAP controller that can be
	mapped to the standard TAP controller (old JTAG standard).
	- However, I cannot map the following states in the standard TAP controller
		to comparable states in the FSM of the TAP controller in the RTL.
		* Select-DR-Scan
		* Exit1-DR
		* Exit2-DR
	- These are states related to the scan data registers of the ADU.
	- I cannot find FSM states in the RTL for the ADU that can be mapped to the
		states for the scan instruction registers in the standard TAP controller.
	- See buggy_soc/ips/adv_dbg_if/doc/AdvancedDebugInterface.pdf. 




##	Questions about the JTAG-based Debugging Unit

+ Are there any access hidden JTAG registers that can be accessed via
	side-channel or backdoor attacks?
	- Reference: https://www.cl.cam.ac.uk/~sps32/ECRYPT2011_1.pdf







#	References








@article{Rosenfeld2010,
	Address = {Los Alamitos, {CA}},
	Author = {Kurt Rosenfeld and Ramesh Karri},
	Doi = {https://dx.doi.org/10.1109/MDT.2010.9},
	Journal = {{IEEE} Design {\rm \&}\ Test of Computers},
	Month = {January--February},
	Number = {1},
	Pages = {36--47},
	Publisher = {{IEEE} Computer Society Press},
	Title = {Attacks and Defenses for {JTAG}},
	Volume = {27},
	Year = {2010}}

@article{Majeric2017,
	Address = {},
	Author = {F. Maj{\'{e}}ric and B. Gonzalvo and L. Bossuet},
	Doi = {https://dx.doi.org/10.1109/LES.2017.2771206},
	Journal = {{IEEE} Embedded Systems Letters},
	Month = {November 9},
	Number = {},
	Pages = {},
	Publisher = {{IEEE} Press},
	Title = {{JTAG} Fault Injection Attack},
	Volume = {},
	Year = {2017}}

@book{Wang2006b,
	Address = {San Francisco, {CA}},
	Author = {Wang, {Laung-Terng} and Wu, {Cheng-Wen} and Wen, Xiaoqing},
	Publisher = {Morgan Kaufmann},
	Series = {The Morgan Kaufmann Series in Systems on Silicon},
	Title = {{VLSI} Test Principles And Architectures: Design for Testability},
	Year = {2006}}





























#	Author Information

The MIT License (MIT)

Copyright (c) <2017> Zhiyang Ong

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Email address: echo "cukj -wb- 23wU4X5M589 TROJANS cqkH wiuz2y 0f Mw Stanford" | awk '{ sub("23wU4X5M589","F.d_c_b. ") sub("Stanford","d0mA1n"); print $5, $2, $8; for (i=1; i<=1; i++) print "6\b"; print $9, $7, $6 }' | sed y/kqcbuHwM62z/gnotrzadqmC/ | tr 'q' ' ' | tr -d [:cntrl:] | tr -d 'ir' | tr y "\n"		Don't compromise my computing accounts. You have been warned.



