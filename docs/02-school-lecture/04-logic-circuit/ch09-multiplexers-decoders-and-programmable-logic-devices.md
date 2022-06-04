---
layout: default
title: Ch9 Multiplexers, Decoders, and Programmable Logic Devices
parent: Logic Circuit
grand_parent: School Lecture
nav_order: 9
mathjax: true
permalink: /docs/logic-circuit/ch9
---

# Ch9 Multiplexer, Decoders, and Programmable Logic Devices
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

## 9.1 Introduction

- ICs: integrated circuits

	- Depending on the number of gates in each integrated circuit package and the type of function performed.

	- SSI: small-scale integration

		- NAND, NOR, AND and OR gates, inverters, and flip-flops

		- four gates, six inverters, or one or two flip-flops

	- MSI: medium-scale integration

		- adders, multiplexers, decoders, registers, and counters

		- equivalent of 12 to 100 gates

	- LSI: large-scale integration

		- memories and microprocessors

		- 100 to a few thousand gates

	- VLSI: very-large-scale integration

		- memories and microprocessors

		- several thousandgate or more

-  By using LSI and VLSI functions, the required number of integrated circuit packages is greatly reduced

- This unit introduces the use of multiplexers, decoders, encoders, and three-state buffers in logic design. Then read-only memories (ROMs) are described and used to implement multiple-output combinational logic circuits. Finally, other types of programmable logic devices (PLDs), including programmable logic arrays (PLAs), programmable array logic devices (PALs), complex programmable logic devices (CPLDs), and field- programmable gate arrays (FPGAs) are introduced and used in combinational logic design.

---

## 9.2 Multiplexers

- Data Selector, MUX

- Multiplexer has a group of data inputs and a group of control inputs

- The control inputs are used to select one of the data inputs and connect it to the output terminal

### 2-to-1 MUX

<center markdown="block">
![2-to-1-mux](/assets/logic-circuit/img/9-2-to-1-mux.png)
</center>

$$
\begin{cases}
A=0, Z=I_0 \\
A=1, Z=I_1
\end{cases}
$$

- data input 2개, control input 1-bit

$$
A = A^{\prime}I_0 + AI_1
$$

<table>
	<thead>
		<tr>
			<th>$A$</th>
			<th class="left-none">$I_0$</th>
			<th class="left-none">$I_1$</th>
			<th>$Z$</th>
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
			<td>0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>0</td>
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
			<td>0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>1</td>
		</tr>
	</tbody>
</table>

<table>
	<caption>$Z$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$A$</div>$I_0I_1$</th>
			<th>0</th>
			<th>1</th>
		 </tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>01</th>
			<td></td>
			<td class="map2">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td class="map2">1</td>
			<td class="map2">1</td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map2">1</td>
			<td></td>
		</tr>
	</tbody>
</table>

$$
Z = AI_1+A^{\prime}I_0
$$

### 4-to-1 MUX

<center markdown="block">
![4-to-1-mux](/assets/logic-circuit/img/9-4-to-1-mux.png)
</center>

- data input 2개, control input 1-bit

$$
\begin{cases}
AB = 00, Z=I_0 \\
AB=01, Z=I_1 \\
AB=10, Z=I_2 \\
AB = 11, Z=I_3
\end{cases}
$$

- input 6개. K-map으로 구현하기 어려움

- 논리 설계

$$
\begin{align*}
Z &= A^{\prime}B^{\prime}I_0+A^{\prime}BI_1+AB^{\prime}I_2+ABI_3 \\
  &= A^{\prime}(B^{\prime}I_0 +BI_1)+A(B^{\prime}I_2+BI_3) \\
  &= ((A^{\prime}((B^{\prime}I_0)^{\prime}(BI_1)^{\prime})^{\prime})^{\prime}(A((B^{\prime}I_2)^{\prime}(BI_3)^{\prime})^{\prime})^{\prime}
\end{align*}
$$

##### Using NAND

<center markdown="block">
![4-to-1-mux-using-nand](/assets/logic-circuit/img/9-4-to-1-mux-using-nand.png)
</center>

##### Using MUX

<center markdown="block">
![4-to-1-mux-using-mux](/assets/logic-circuit/img/9-4-to-1-mux-using-mux.png)
</center>

### 8-to-1 MUX

<center markdown="block">
![8-to-1-mux](/assets/logic-circuit/img/9-8-to-1-mux.png)
</center>

- data input 2개, control input 1-bit

$$
\begin{cases}
ABC=000, I_0 \\
ABC=001, I_1 \\
ABC=010, I_2 \\
\quad\vdots \\
ABC=111, I_7
\end{cases}
$$

##### Using MUX

<center markdown="block">
![8-to-1-mux-using-mux1](/assets/logic-circuit/img/9-8-to-1-mux-using-mux1.png)

2-to-1 MUX 4-to-1 MUX

![8-to-1-mux-using-mux2](/assets/logic-circuit/img/9-8-to-1-mux-using-mux2.png)

4-to-1 MUX 2-to-1 MUX
</center>

### Bus

<center markdown="block">
![quad-multiplexer](/assets/logic-circuit/img/9-quad-multiplexer.png)

- Several logic signals that perform a common function may be grouped together to form a bus.

![quad-multiplexer-with-bus](/assets/logic-circuit/img/9-quad-multiplexer-with-bus.png)
</center>

### Active-High, Active-Low

- The multiplexers without the inversion have active high outputs, and the multiplexers with the inversion have active low outputs

- The enable signal $E$ is connected to the input of each of the AND gates

	- $E=0, Z=0$

- The enable is active high; $E$ must be 1 for the MUX to function as a multiplexer.

- If an inverter is inserted between $E$ and the AND gates, $E$ must be 0 for the MUX to function as a multiplexer; the enable is active low

<center markdown="block">
![active-high-low](/assets/logic-circuit/img/9-active-high-low.png)
</center>

### Example

- $F = A^{\prime}C^{\prime}+A^{\prime}BD^{\prime}+AB^{\prime}D^{\prime}$

<table>
	<caption>$F$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$AB$</div>$CD$</th>
			<th>00</th>
			<th>01</th>
			<th>11</th>
			<th>10</th>
		 </tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td class="map3">1</td>
			<td class="map2_3">1</td>
			<td></td>
			<td class="map2">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map3">1</td>
			<td class="map3">1</td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td class="map2">1</td>
			<td></td>
			<td class="map2">1</td>
		</tr>
	</tbody>
</table>

##### control input이 $A, B$일 때

<table>
	<caption>$F$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$AB$</div>$CD$</th>
			<th>00</th>
			<th>01</th>
			<th>11</th>
			<th>10</th>
		 </tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td class="map2">1</td>
			<td class="map2_2">1</td>
			<td></td>
			<td class="map2">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map2">1</td>
			<td class="map2">1</td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td class="map2">1</td>
			<td></td>
			<td class="map2">1</td>
		</tr>
	</tbody>
</table>

$$
\begin{cases}
AB=00, C^{\prime} \\
AB=01, C^{\prime}+D^{\prime} \\
AB=10, D^{\prime} \\
AB=11, 0
\end{cases}
$$

<center markdown="block">
![mux-ex1-1](/assets/logic-circuit/img/9-mux-ex1-1.png)
</center>

- $F = A^{\prime}B^{\prime}C^{\prime}+A^{\prime}B(C^{\prime}+D^{\prime})+AB^{\prime}D^{\prime}$

##### control input이 $C, D$일 때

<table>
	<caption>$F$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$AB$</div>$CD$</th>
			<th>00</th>
			<th>01</th>
			<th>11</th>
			<th>10</th>
		 </tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td class="map2_2">1</td>
			<td class="map2">1</td>
			<td></td>
			<td class="map2">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map2">1</td>
			<td class="map2">1</td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td class="map1">1</td>
			<td></td>
			<td class="map1">1</td>
		</tr>
	</tbody>
</table>

$$
\begin{cases}
CD=00, A^{\prime}+B^{\prime} \\
CD=01, A^{\prime} \\
CD=10, A \oplus B \\
CD=11, 0
\end{cases}
$$

<center markdown="block">
![mux-ex1-2](/assets/logic-circuit/img/9-mux-ex1-2.png)
</center>

- $F = C^{\prime}D^{\prime}(A^{\prime}+B^{\prime})+C^{\prime}DA^{\prime}+CD^{\prime}(A \oplus B)$

---

## 9.3 Three-State Buffers

### Buffer

<center markdown="block">
![buffer](/assets/logic-circuit/img/9-buffer.png)

Buffer
</center>

- $F = A$

### Three-state buffer

<center markdown="block">
![three-state-buffer](/assets/logic-circuit/img/9-three-state-buffer.png)

Three-state buffer

![three-state-buffer-switch](/assets/logic-circuit/img/9-three-state-buffer-switch.png)

Three-state buffer switch
</center>

$$
\begin{cases}
B=1, C=A \\
B=0, C=Z\text{(High Inpedence)}
\end{cases}
$$

<center markdown="block">
![three-state-buffer-four-types](/assets/logic-circuit/img/9-three-state-buffer-four-types.png)
</center>

- $Z,0,1$ 3가지 값이 나오기 때문에 three-state

### MUX

<center markdown="block">
![mux-buffer](/assets/logic-circuit/img/9-mux-buffer.png)

$\equiv$

![mux](/assets/logic-circuit/img/9-mux.png)
</center>

- when $A=0$, the top buffer is enabled, so that $F=I_0;$ when $A=1$, the lower buffer is enalbed, so that $F=I_1$.

$$
\begin{cases}
A=0, F=I_0 \\
A=1, F=I_1 \\
\end{cases}
$$

$$
F = A^{\prime}I_0+AI_1
$$

### connected two three-state buffer outputs

<table>
	<thead>
		<tr>
			<th class='backslash'><div>$S_2$</div>$S_1$</th>
			<th>X</th>
			<th>0</th>
			<th>1</th>
			<th>Z</th>
		</tr>
	</thead>
	<tbody>
		 <tr>
			<th>X</th>
			<td>X</td>
			<td>X</td>
			<td>X</td>
			<td>X</td>
		</tr>
		<tr>
			<th>0</th>
			<td>X</td>
			<td>0</td>
			<td>X</td>
			<td>0</td>
		</tr>
		<tr>
			<th>1</th>
			<td>X</td>
			<td>X</td>
			<td>1</td>
			<td>1</td>
		</tr>
		<tr>
			<th>Z</th>
			<td>X</td>
			<td>0</td>
			<td>1</td>
			<td>Z</td>
		</tr>
	</tbody>
</table>

- If one of the buffers is disabled (output=Z), the combined output $F$ is the same as the other buffer output.

- If both buffers are disabled, the output is Z.

- If both buffers are enabled, a conflict can occur.

- If $A=0$ and $C=1$, we do not know what the hardware will do, so the $F$ output is unknown (X)

- If one of the buffer inputs is unknown, the $F$ output will also be unknown.

### Bus

<center markdown="block">
![bus](/assets/logic-circuit/img/9-bus.jpg)
</center>

- Bus: 컴퓨터 안의 부품들 간에 또는 컴퓨터 간에 데이터와 정보를 전송하는 통신 시스템

	- 각 부품에 대해 공통된 선을 두어 연결한다.

	- 양방향 통신

- bus 사용 장점

	- 여러 개의 부품에 대해 따로 연결할 필요 없이 모든 부품이 연결된 공통 선에 연결하면 된다.

- bus 사용 단점

	- 한번에 하나씩 쓸 수 있도록 bus controller가 있어야 한다.

	- 연결된 부품의 내부 회로에 영향을 받을 수 있다.

- 통신하려는 부품 외의 연결을 끊기 위해 three-state buffer를 사용한다. 전류의 역류도 방지한다.

	- 모든 부품의 output에 three-state buffer를 단다.

---

## 9.4 Decoders and Encoders

### Decoders

- An $n$-to-$2^n$ line decoder generates all $2^n$ minterms of the $n$ input variables

- if the decoder outputs are inverted, generates maxterms

$$
\begin{matrix}
& y_i = m_i = M_i^{\prime}, & i=0\, \text{to}\, 2^n-1 & (\text{noninverted outputs}) \\
\text{or} & \\
&  y_i = m_i^{\prime} = M_i, & i = 0\, \text{to}\, 2^n-1 & (\text{inverted outputs})
\end{matrix}
$$

- $n$-variable functions can be reailzed by ORing together selected minterm outputs from a decoder

- If the decoder outputs are inverted, then NAND gates can be used to generate the functions

##### 용도

- 여러개의 three-state-buffer 중 control bit로 하나만 enable하게 하도록 제어한다.

- control하고 싶은 unit의 enable bit에 연결하여 control bit로 한 번에 하나씩 정상동작하도록 제어한다.

##### 3-to-8 decoder

<center markdown="block">
![3-to-8-decoder](/assets/logic-circuit/img/9-3-to-8-decoder.png)
</center>

- $F = \sum m(0,1,3,4)$

<center markdown="block">
![3-to-8-decoder-ex](/assets/logic-circuit/img/9-3-to-8-decoder-ex.png)
</center>

##### 4-to-10 decoder

<center markdown="block">
![4-to-10-decoder](/assets/logic-circuit/img/9-4-to-10-decoder.png)
</center>

- when a binary-coded-decimal digit is used as an input to this decode one of the output lines will go low to indicate which of the 10 decimal digits is present

### Encoders

- encoder performs the inverse function of a decoder

<center markdown="block">
![8-to-3-priority-encoder]((/assets/logic-circuit/img/9-8-to-3-priority-encoder.png)
</center>

---

## 9.5 Read-Only Memories

- memory는 주소에 있는 데이터를 읽고 주소에 데이터를 쓰는 두 가지 operation으로 작동한다.

- Read-Only Memory(ROM)

- 한 번 기록된 정보를 읽을 수만 있고 수정할 수는 없다.

- 전원이 공급되지 않아도 기록된 정보가 지워지지 않는 비휘발성 메모리이다.

- 펌웨어를 저장하는 데 주로 사용된다.

### ROM

- A ROM which has $n$ input lines and $m$ output lines contains an array of $2^n$ words, and each word is $m$ bits long

- The input lines serve as an address to select one of the $2^n$ words

- When an input combination is applied to the ROM, the pattern of 0's and 1's which is stored in the corresponding word in the memory appears at the output lines

- A $2^n \times m$ ROM can realize $m$ functions of $n$ variables because it can store a truth table with $2^n$ rows and $m$ columns.

<center markdown="block">
![rom](/assets/logic-circuit/img/9-rom.png)

ROM with $n$ inputs and $m$ outputs
</center>

### Basic ROM structure

- A ROM basically consists of a decoder and a memory array

<center markdown="block">
![rom-structure](/assets/logic-circuit/img/9-rom-structure.png)

basic ROM structure
</center>

- When a pattern of $n$ 0's and 1's is applied to the decoder inputs exactly one of the $2^n$ decoder outputs is 1

- This decoder output line selects one of the words in the memory array, and the bit pattern stored in this word is transferred to the memory output lines.

### Internal structure

- The minterms which are connected to output line $F$ by switching elements are ORed together to form the output $F_i$.

- A switching element is placed at the intersection of a $word\,line$ nad an $output\,line$ if the corresponding minterm is to be included in the output function; otherwise, the switching element is omitted (or not connected)

	- If a switching element connects an output line to a word line which is 1, the output line will be 1

	- Otherwise, the pull-down resistors cause the output line to be 0.

- So the switching elements which are connected in this way in the memory array

<center markdown="block">
![8-word-4-bit-rom](/assets/logic-circuit/img/9-8-word-4-bit-rom.png)

8-word $\times$ 4-bit ROM

![rom-internal-structure](/assets/logic-circuit/img/9-rom-internal-structure.png)

8-word $\times$ 4-bit ROM internal structure
</center>

---

## HW4

### 1

- 4-bit Add ALU(Arithmetic Logic Unit)

- Operation: Add, Subract, AND, OR

- overflow는 생각하지 않는다.

<center markdown="block">
![1](/assets/logic-circuit/img/9-hw-1.png)
</center>

##### Circuit

<center markdown="block">
![circuit](/assets/logic-circuit/img/9-hw-1-circuit.png)

Circuit

![circuit-ex1](/assets/logic-circuit/img/9-hw-1-circuit-ex1.png)

$110 + 101 = 1011$

![circuit-ex2](/assets/logic-circuit/img/9-hw-1-circuit-ex2.png)

$110 - 101 = 0001$

![circuit-ex3](/assets/logic-circuit/img/9-hw-1-circuit-ex3.png)

$110 AND 101 = 0100$

![circuit-ex4](/assets/logic-circuit/img/9-hw-1-circuit-ex4.png)
</center>

$110 OR 101 = 0111$

##### 4-bit ALU

<center markdown="block">
![4-bit-alu](/assets/logic-circuit/img/9-hw-4-bit-alu.png)

Circuit

![4-bit-alu-block](/assets/logic-circuit/img/9-hw-4-bit-alu-block.png)

Block
</center>

##### 4-to-1 MUX

<center markdown="block">
![4-to-1-mux](/assets/logic-circuit/img/9-hw-4-to-1-mux.png)

Circuit

![4-to-1-mux-block](/assets/logic-circuit/img/9-hw-4-to-1-mux-block.png)

Block
</center>

##### 1-bit full adder

<table>
	<thead>
		<tr>
			<th>$C_{in}$</th>
			<th class="left-none">$A$</th>
			<th class="left-none">$B$</th>
			<th>$C_{out}$</th>
			<th class="left-none">$F$</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>0</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>1</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>1</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>1</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>1</td>
			<td class="left-none">1</td>
		</tr>
	</tbody>
</table>

<table>
	<caption>$C_{out}$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$C_{in}$</div>$AB$</th>
			<th>0</th>
			<th>1</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>00</th>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>01</th>
			<td></td>
			<td class="map2">1</td>
		</tr>
		<tr>
			<th>11</th>
			<td class="map2">1</td>
			<td class="map2_2_2">1</td>
		</tr>
		<tr>
			<th>10</th>
			<td></td>
			<td class="map2">1</td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
C_{out} &= C_{in}B+AB+C_{in}A \\
        &= B(C_{in}+A)+C_{in}A \\
		&= ((B(C_{in}^{\prime}A^{\prime})^{\prime})^{\prime}(C_{in}A)^{\prime})^{\prime}
\end{align*}
$$

<table>
	<caption>$F$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$C_{in}$</div>$AB$</th>
			<th>0</th>
			<th>1</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>00</th>
			<td></td>
			<td class="map1">1</td>
		</tr>
		<tr>
			<th>01</th>
			<td class="map1">1</td>
			<td></td>
		</tr>
		<tr>
			<th>11</th>
			<td></td>
			<td class="map1">1</td>
		</tr>
		<tr>
			<th>10</th>
			<td class="map1">1</td>
			<td></td>
		</tr>
	</tbody>
</table>

$$
F = C_{in} \oplus A \oplus B
$$

<center markdown="block">
![1-bit-full-adder](/assets/logic-circuit/img/9-hw-1-bit-full-adder.png)

Circuit

![1-bit-full-adder-block](/assets/logic-circuit/img/9-hw-1-bit-full-adder-block.png)

Block
</center>

##### 4-bit full adder

<center markdown="block">
![4-bit-full-adder](/assets/logic-circuit/img/9-hw-4-bit-full-adder.png)

Circuit

![4-bit-full-adder-block](/assets/logic-circuit/img/9-hw-4-bit-full-adder-block.png)

Block
</center>

##### 1-bit subtractor

<table>
	<thead>
		<tr>
			<th>$B_{in}$</th>
			<th class="left-none">$A$</th>
			<th class="left-none">$B$</th>
			<th>$B_{out}$</th>
			<th class="left-none">$F$</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>1</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>1</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>1</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>1</td>
			<td class="left-none">1</td>
		</tr>
	</tbody>
</table>

<table>
	<caption>$B_{out}$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$B_{in}$</div>$AB$</th>
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
			<td class="map2_2_2">1</td>
		</tr>
		<tr>
			<th>11</th>
			<td></td>
			<td class="map2">1</td>
		</tr>
		<tr>
			<th>10</th>
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
B_{out} &= B_{in}A^{\prime}+A^{\prime}B+B_{in}B \\
        &= A^{\prime}(B_{in}+B) +B_{in}B \\
		&= ((A^{\prime}(B_{in}^{\prime}B^{\prime})^{\prime})^{\prime}(B_{in}B)^{\prime})^{\prime}
\end{align*}
$$

<table>
	<caption>$F$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$B_{in}$</div>$AB$</th>
			<th>0</th>
			<th>1</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>00</th>
			<td></td>
			<td class="map1">1</td>
		</tr>
		<tr>
			<th>01</th>
			<td class="map1">1</td>
			<td></td>
		</tr>
		<tr>
			<th>11</th>
			<td></td>
			<td class="map1">1</td>
		</tr>
		<tr>
			<th>10</th>
			<td class="map1">1</td>
			<td></td>
		</tr>
	</tbody>
</table>

$$
F = B_{in} \oplus A \oplus B
$$

<center markdown="block">
![1-bit-full-subtractor](/assets/logic-circuit/img/9-hw-1-bit-full-subtractor.png)

Circuit

![1-bit-full-subtractor-block](/assets/logic-circuit/img/9-hw-1-bit-full-subtractor-block.png)

Block
</center>

##### 4-bit full subtractor

<center markdown="block">
![4-bit-full-subtractor](/assets/logic-circuit/img/9-hw-4-bit-full-subtractor.png)

Circuit

![4-bit-full-subtractor-block](/assets/logic-circuit/img/9-hw-4-bit-full-subtractor-block.png)

Block
</center>

##### 4-bit AND

<center markdown="block">
![4-bit-and](/assets/logic-circuit/img/9-hw-4-bit-and.png)

Circuit

![4-bit-and-block](/assets/logic-circuit/img/9-hw-4-bit-and-block.png)

Block
</center>

##### 4-bit OR

<center markdown="block">
![4-bit-or](/assets/logic-circuit/img/9-hw-4-bit-or.png)

Circuit

![4-bit-or-block](/assets/logic-circuit/img/9-hw-4-bit-or-block.png)

Block
</center>

