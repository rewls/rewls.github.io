---
layout: default
title: Ch11 Latches and Flip-Flops
parent: Logic Circuit
grand_parent: School Lecture
nav_order: 9
mathjax: true
permalink: /docs/logic-circuit/ch9
---

# Ch11 Latches and Flip-Flops
{: .no_toc }

<details markdown="block">
  <summary>
	Table of contents
  </summary>
{: .fs-3 .text-delta }

- TOC
{:toc}
</details>

---

## 11.1 Introduction

- Sequential switching circuits have the property that the output depends not only on the present input but also on the past sequence of inpus.

- These circuits must be ableto "remember" something about the past history of the inputs in order to produce the present output

- Latches and flip-flops are commonly used memory devices in sequential circuits

- Basically, latches and flip-flops are memory devices which can assumme one of two stable output states and which have one or more inputs that can cause the output state to change

- Each of the flip-flops has a clock input, and the flip-flops can only change state in response to a clock pulse

- latch: A memory element that has no clock input

- flip-flop: A memory device that changes its output in response to a clock input and not in response to a data input

- In order to construct a switching circuit that has memory, we must introduce feedback into the circuit.

- By feedback we mean that the output of one of the gates is connected back into the input of another gate in the circuit so as to form a closed loop

- In simple cases, we can analyze circuits with feedback by tracing signals through the circuit.

### Example 1

<center markdown="block">
![feedback-ex1](/assets/logic-circuit/img/11-feedback-ex1.png)
</center>

- If at some instant of time the inverter input is 0, this will propagate through the inverter and cause the output to become 1 after the inverter delay.

- This 1 is fed back into the input, so after the propagation delay, the inverter output will become 0.

- When this 0 feeds back into the input, the output will again switch to 1, and so forth

- An oscillator can be created using any odd number of inverters.

- The oscillator waveform has a high and a low time that is the sum of the propagation times of the inverters.

### Example 2

<center markdown="block">
![feedback-ex2](/assets/logic-circuit/img/11-feedback-ex2.png)
</center>

- The circuit has two stable conditions, often referred to as stable states

- If the input to the first inverter is 0, its output will be 1

- Then, the input to the second inverter will be 1, and its outputwill be 0

- This 0 will feed back into the first inverter, but because this input is already 0, no changes will occur

- When the input to the first inverter is 1 and the input to the second inverter is 0.

- The simple loop of two inverters lacks any external means of initializingthe state to one of the stable states.

---

## 11.2 Set-Reset Latch

- We can construct a simple latch by introducing feedback into a NOR-gate circuit.

<center markdown="block">
![nor-latch](/assets/logic-circuit/img/11-nor-latch.png)
</center>

### 변화 관찰

<center markdown="block">
![nor-latch-11](/assets/logic-circuit/img/11-nor-latch-11.png)

$1.\,S=1, R=1: P=0, Q=0$

![nor-latch-10](/assets/logic-circuit/img/11-nor-latch-10.png)

$2.\,S=1, R=0: P=0, Q=1$

![nor-latch-11](/assets/logic-circuit/img/11-nor-latch-11.png)

$3.\,S=1, R=1: P=0, Q=0$

![nor-latch-01](/assets/logic-circuit/img/11-nor-latch-01.png)

$4.\,S=0, R=1: P=1, Q=0$

![nor-latch-00-1](/assets/logic-circuit/img/11-nor-latch-00-1.png)

$5.\,\color{red}S=0, R=0: P=1, Q=0$

![nor-latch-10](/assets/logic-circuit/img/11-nor-latch-10.png)

$6.\,S=1, R=0: P=0, Q=1$

![nor-latch-00](/assets/logic-circuit/img/11-nor-latch-00-2.png)

$7.\,\color{red}S=0, R=0: P=0, Q=1$
</center>

- $7.$에서 input은 다시 $S=R=0$이 되지만 output은 $5.$와 다르다.

- This circuit is said to have memory because its output depends not only on the present inputs, but also on the past sequence of inputs.

### S-R latch

<center markdown="block">
![s-r-latch](/assets/logic-circuit/img/11-s-r-latch.png)

S-R latch $cross$-$coupled$ form

![s-r-latch-block](/assets/logic-circuit/img/11-s-r-latch-block.png)

Block

![s-r-latch-timing-diagram](/assets/logic-circuit/img/11-s-r-latch-timing-diagram.png)

Timing diagram
</center>

- When used with the restriction that $R$ and $S$ cannot be 1 simultaneouly, the circuit is commonly referred to as a set-reset ($S$-$R$) latch

- $S=R=1$

	- If $S=R=1$, the latch will not operate properly

	- $P$ is not equal to $Q^{\prime}$, and this viloates a basic rule of latch operation that requires the latch outputs to be complements.

	- if $S$ and $R$ are simulataneously changed back to 0, $P$ and $Q$ may both change to 1.

	- If $S=R=0$ and $P=Q=1$, then after the 1's propagate through the gates, $P$ and $Q$ will become 0 again, and the latch may continue to oscillate if the gate delays are equal.

- If we restrict the inputs so that $R=S=1$ is not allowed, the stable states of the outputs $P$ and $Q$ are alaways complements, $P=Q^{\prime}$

- $Q$: present state, $Q^+$: next state

<table>
	<caption>Truth table</caption>
	<thead>
		<tr>
			<th>$S$</th>
			<th class="left-none">$R$</th>
			<th class="left-none">$Q$</th>
			<th>$Q^+$</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>-</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>-</td>
		</tr>
	</tbody>
</table>

- `-`: Inputs not allowed

$$
\begin{cases}
S=0, R=1 &: Q^+=0 \\
S=1, R=0 &: Q^+=1 \\
S=0, R=0 &: Q^+=Q \\
S=1, R=1 &: \text{Don't care}
\end{cases}
$$

- An input $S=1$ $sets$ the output to $Q=1$, and an input $R=1$ $resets$ the output to $Q=0$

- $Q$가 memory 역할을 한다.

<table>
	<caption>$Q^+$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$S$</div>$RQ$</th>
			<th>0</th>
			<th>1</th>
		 </tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td></td>
			<td class="map3">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map2">1</td>
			<td class="map2_3">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td class="map3">x</td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td class="map3">x</td>
		</tr>
	</tbody>
</table>

$$
Q^+ = S+R^{\prime}Q
$$

### S-R latch using NAND

<center markdown="block">
![s-r-latch-nand-inverter](/assets/logic-circuit/img/11-s-r-latch-nand-inverter.png)

Circuit

![s-r-latch-nand-inverter-block](/assets/logic-circuit/img/11-s-r-latch-nand-inverter-block.png)

Block
</center>

$$
\begin{align*}
Q^+ &= (S^{\prime}(R^{\prime}Q)^{\prime})^{\prime} \\
    &= S + R^{\prime}Q
\end{align*}
$$

<center markdown="block">
![s-r-latch-nand](/assets/logic-circuit/img/11-s-r-latch-nand.png)

Circuit

![s-r-latch-nand-block](/assets/logic-circuit/img/11-s-r-latch-nand-block.png)

Block
</center>

---

## 11.3 Gated Latches

### Gated S-R Latch

<center markdown="block">
![gated-s-r-latch](/assets/logic-circuit/img/11-gated-s-r-latch.png)

Circuit
</center>

$$
\begin{cases}
G=1 &: Q^+=S+R^{\prime}Q \\
G=0 &: Q^+=Q
\end{cases}
$$

### Gated D Latch

<center markdown="block">
![gated-d-latch-s-r-latch](/assets/logic-circuit/img/11-gated-d-latch-s-r-latch.png)

Circuit

![gated-d-latch-block](/assets/logic-circuit/img/11-gated-d-latch-block.png)

Block
</center>

$$
\begin{cases}
G=0 &: Q^+=Q \\
G=1, D=0 &: Q^+=0 \\
G=1, D=1 &: Q^+=1
\end{cases}
$$

$$
\begin{cases}
G=0 &: Q^+=Q \\
G=1 &: Q^+=D
\end{cases}
$$

- 1 bit memory

### Example

- Most digital systems use a clock signal to synchronize the change in outputs of the system's flip-flops to an edge of the clock signal

- it is tempting to think that gated latches could be used as flip-flops where the clock signal is connected to the gate inputs of the latches.

- However, this is not a practical approach

- The following example illustrates the difficulty

<center markdown="block">
![unreliable-gated-d-latch](/assets/logic-circuit/img/11-unreliable-gated-d-latch.png)
</center>

- $\text{Clk}=1, x=1 : Q=0\rightarrow1\rightarrow0\rightarrow1$

- It seems that when the $\text{Clk}$ is 1 the next value of $Q$ should be $Q^{\prime}$ when the input $x=1$ and should be $Q$ when $x=0$

- If $\text{Clk}$ remains at 1, $Q$ will oscillate.

- The circuit will only operate as intended if $\text{Clk}$ remains at 1 for a short time; it has to 1 just long enough to allow $Q$ to change but short enough to prevent the change from feeding back and causing a second change

- In a system with several latches, the variation in gate delays would make it impossible to provide the correct clock width to all latches.

<center markdown="block">
![gated-d-latch-s-r-latch-timing-diagram](/assets/logic-circuit/img/11-gated-d-latch-s-r-latch-timing-diagram.png)

Timing diagram
</center>

##### edge-triggered

- To avoid this iming problem, more complicated flip-flops restrict the flip-flop output to only change on an edge of the clock, and the outputs cannot change at other times even if the inputs change

- edge-triggered: If the inputs to the flip-flop only need to be stable for a short period of time around the clock edge

- master-slave flip-flop: a particular implementation that uses two gated latches in such a way that the flip-flop outputs only change on a clock edge

- However, master-slave flipflops are not neccessarily edge-triggered flip-flops because they may require the flip-flop inputs to be stabe at times during the clock period other than just around the clock edge.

	-  The S-R, J-K, and T master-slave flip-flops in later sections are examples. The master-slave D flip-flop of the next section is an exception; it uses the master-slave implementation and it is also edge triggered.

---

## 11.4 Edge-Triggered D Flip-Flop

- A D flip-flop has two inputs, $D$ (data) and $\text{Ck}$ (clock)

- The small arrowhead on the flip-flop symbol identifies the clock input.

- Unlike the D latch, the flip-flop output changes only in response to the clock, not to a change in $D$

- rising edge (or positive edge): if the output can change in response to a 0 to 1 trasition on the clock input

- falling edge (or negative edge): if the output can change in response to a 1 to 0 transition on the clock input

- falling-edge trigger: an inversion bubble on the clock input

- rising-edge trigger: no bubble on the clock input

- active edge: the clock edge (rising or falling) that triggers the flip-flop state change

### Clock

- 0과 1을 일정한 주기로 진동하는 신호

- 클럭 속도(Hz): 초당 사이클 수

	- 주기가 1sec이면 1Hz, 주기가 2sec이면 0.5Hz

	- 속도 = 1 / 주기

- 클럭 주기마다 하나의 명령어가 실행이 되기 때문에 클럭 속도가 빠른 CPU는 한 명령어를 실행하는 시간이 짧다.

### Rising-edge triggered D flip-flop

<center markdown="block">
![rising-edge-triggered-d-flip-flop-timing-diagram](/assets/logic-circuit/img/11-rising-edge-triggered-d-flip-flop-timing-diagram.png)

Timing Diagram
</center>

<center markdown="block">
![rising-edge-triggered-d-flip-flop-gated-d-latch](/assets/logic-circuit/img/11-rising-edge-triggered-d-flip-flop-gated-d-latch.png)

Implementation using d latchs

![rising-edge-triggered-d-flip-flop-gated-d-latch-timing-diagram](/assets/logic-circuit/img/11-rising-edge-triggered-d-flip-flop-gated-d-latch-timing-diagram.png)

d flip-flop using d latchs timing diagram
</center>

---

## 11.5 S-R Flip-Flop

<center markdown="block">
![s-r-flip-flop](/assets/logic-circuit/img/11-s-r-flip-flop.png)

S-R flip-flop
</center>

$$
\begin{cases}
S=R=0 & \text{No state change} \\
S=1,R=0 & \text{Set }Q\text{ to 1 (after active Ck edge)} \\
S=0,R=1 & \text{Reset }Q\text{ to 0 (after active Ck edge)} \\
S=R=1 & \text{Not allowed}
\end{cases}
$$

### Rising-edge triggered master-slave S-R flip-flop

<center markdown="block">
![s-r-flip-flop-s-r-latch](/assets/logic-circuit/img/11-s-r-flip-flop-s-r-latch.png)

Implementation of master-slave

![s-r-flip-flop-s-r-latch-timing-diagram](/assets/logic-circuit/img/11-s-r-flip-flop-s-r-latch-timing-diagram.png)

Timing diagram
</center>

---

## 11.6 J-K Flip-Flop

<center markdown="block">
![j-k-flip-flop](/assets/logic-circuit/img/11-j-k-flip-flop.png)

J-K flip-flop
</center>

$$
\begin{cases}
J=1, K=0 &: Q^+=1 \\
J=0, K=1 &: Q^+=0 \\
J=0, K=0 &: Q^+=Q \\
J=1, K=1 &: Q^+=Q^{\prime}
\end{cases}
$$

<table>
	<caption>Truth table</caption>
	<thead>
		<tr>
			<th>$J$</th>
			<th class="left-none">$K$</th>
			<th class="left-none">$Q$</th>
			<th>$Q^+$</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>0</td>
		</tr>
	</tbody>
</table>

<table>
	<caption>$Q^+$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$J$</div>$KQ$</th>
			<th>0</th>
			<th>1</th>
		 </tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td></td>
			<td class="map2">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map2">1</td>
			<td class="map2">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td class="map2">1</td>
		</tr>
	</tbody>
</table>

$$
Q^+ = JQ^{\prime}+R^{\prime}Q
$$

### Rising-edge triggered J-K flip-flop

<center markdown="block">
![j-k-flip-flop-timing-diagram](/assets/logic-circuit/img/11-j-k-flip-flop-timing-diagram.png)

Timing diagram
</center>

<center markdown="block">
![j-k-flip-flop-s-r-latch](/assets/logic-circuit/img/11-j-k-flip-flop-s-r-latch.png)

Implementation of master-slave
</center>

- $Q^+=S+R^{\prime}Q$에서 $S$ 대신 $JQ^{\prime}$, $R$ 대신 $KQ$를 넣으면 $Q^+=JQ^{\prime}+K^{\prime}Q$

---

## 11.7 T Flip-Flop

- T: Toggle

<center markdown="block">
![t-flip-flop](/assets/logic-circuit/img/11-t-flip-flop.png)

T flip-flop
</center>

$$
\begin{cases}
T=0 &: Q^+=Q \\
T=1 &: Q^+=Q^{\prime}
\end{cases}
$$

<table>
	<caption>Truth table</caption>
	<thead>
		<tr>
			<th>$T$</th>
			<th class="left-none">$Q$</th>
			<th>$Q^+$</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td>0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td>1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td>1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td>0</td>
		</tr>
	</tbody>
</table>

$$
Q^+ = T \oplus Q
$$

### Rising-edge triggered T flip-flop

<center markdown="block">
![t-flip-flop-timing-diagram](/assets/logic-circuit/img/11-t-flip-flop-timing-diagram.png)

Timing diagram
</center>

##### Implementation

<center markdown="block">
![t-flip-flop-d-flip-flop](/assets/logic-circuit/img/11-t-flip-flop-d-flip-flop.png)

Conversion of D to T
</center>

<center markdown="block">
![t-flip-flop-j-k-flip-flop](/assets/logic-circuit/img/11-t-flip-flop-j-k-flip-flop.png)

Conversion of J-K to T
</center>

---

## 11.8 Flip-Flops with Additional Inputs

- Flip-flops often have additional inputs which can be used to set the flip-flops to an initial state independent of the clock

<center markdown="block">
![d-flip-flop-clear-preset](/assets/logic-circuit/img/11-d-flip-flop-clear-preset.png)

D flip-flop with clear and preset inputs
</center>

- active-low: a logic 0 is required to clear or set the flip-flop.

- ClrN, PreN: active-low clear and preset inputs

<table>
	<thead>
		<tr>
			<th>$\text{Ck}$</th>
			<th class="left-none">$D$</th>
			<th class="left-none">$PreN$</th>
			<th class="left-none">$ClrN$</th>
			<th>$Q^+$</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>x</td>
			<td class="left-none">x</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>(not allowed)</td>
		</tr>
		<tr>
			<td>x</td>
			<td class="left-none">x</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>1</td>
		</tr>
		<tr>
			<td>x</td>
			<td class="left-none">x</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>0</td>
		</tr>
		<tr>
			<td>$\uparrow$</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>0</td>
		</tr>
		<tr>
			<td>$\uparrow$</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>1</td>
		</tr>
		<tr>
			<td>0, 1, $\downarrow$</td>
			<td class="left-none">x</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>$Q$ (no change)</td>
		</tr>
	</tbody>
</table>

- ClrN and PreN are often referred to as $asynchronous$ clearand preset inputs because their operation does not depend on the clock

- The clear and preset inputs can also be synchronous, i.e., the clear and set operations occur on the active edge of the clock
