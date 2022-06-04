---
layout: default
title: Ch8 Combinational Circuit Design and Simulation Using Gates
parent: Logic Circuit
grand_parent: School Lecture
nav_order: 8
mathjax: true
permalink: /docs/logic-circuit/ch8
---

# Ch8 Combinational Circuit Design and Simulation Using Gates
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

## 8.2 Design of Circuits with Limited Gate Fan-In

### Example

- $f = \sum m(0,3,4,5,8,9,10,14,15)$

- only 3-input NOR

<table>
	<thead>
		<tr>
			<th class='backslash'><div>$ab$</div>$cd$</th>
			<th>00</th>
			<th>01</th>
			<th>11</th>
			<th>10</th>
		</tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td></td>
			<td></td>
			<td class="map2">0</td>
			<td></td>
		</tr>
		<tr>
			<th>01</th>
			<td class="map1">0</td>
			<td></td>
			<td class="map2">0</td>
			<td></td>
		</tr>
		<tr>
			<th>11</th>
			<td></td>
			<td class="map2">0</td>
			<td></td>
			<td class="map1">0</td>
		</tr>
		<tr>
			<th>10</th>
			<td class="map2">0</td>
			<td class="map2_2">0</td>
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
f &= (a^{\prime}+b^{\prime}+c)(a+c^{\prime}+d)(a+b^{\prime}+c^{\prime})(a+b+c+d^{\prime})(a^{\prime}+b+c^{\prime}+d^{\prime}) \\
  &= (a^{\prime}+b^{\prime}+c)(a+c^{\prime}+b^{\prime}d)(b+d^{\prime}+(a+c)(a^{\prime}+c^{\prime}))
\end{align*}
$$

<center markdown="block">
![3-input-nor](/assets/logic-circuit/img/8-2-3-input-nor.png)
</center>

##### Expression

$$
\begin{align*}
f &= (a^{\prime}+b^{\prime}+c)(a+c^{\prime}+b^{\prime}d)(b+d^{\prime}+(a+c)(a^{\prime}+c^{\prime})) \\
  &= [(a^{\prime}+b^{\prime}+c)^{\prime}+(a+c^{\prime}+b^{\prime}d)^{\prime}+(b+d^{\prime}+(a+c)(a^{\prime}+c^{\prime}))^{\prime}]^{\prime} \\
  &= [(a^{\prime}+b^{\prime}+c)^{\prime}+(a+c^{\prime}+(b+d^{\prime})^{\prime})^{\prime}+(b+d^{\prime}+((a+c)^{\prime}+(a^{\prime}+c^{\prime})^{\prime})^{\prime}]^{\prime}
\end{align*}
$$

---

## 8.3 Gate Delays and Timing Digrams

- When the input to a logic gate is changed, the output will not change instantaneously

- The transistors or other switching elements within the the gate take a finite time to react to a change in input, so that the change in the gate output is delayed with respect to the input change

### Example

<center markdown="block">
![gate-delay](/assets/logic-circuit/img/8-3-gate-delay.png)
</center>

- $B=1, C=0$

<center markdown="block">
![gate-delay-timing-diagram](/assets/logic-circuit/img/8-3-gate-delay-timing-diagram.png)
</center>

- gate delay: 10 ns

---

## 8.4 Hazards in Combinational Logic

- when the input to a combinational circuit changes, unwanted switching transients may appear in the output

- These transients occur when different paths from input to output have different propagation delays

<center markdown="block">
![hazard](/assets/logic-circuit/img/8-4-hazard.png)
</center>

- static 1-hazard: in response to any single input change and for some combinations of propagation delays, a circuit output may momentarily go to 0 when it whould remain a constant 1, then it is static-0 hazard

- static 0-hazard: the output may momentarily go to 1 when it should remain a 0, then it is a static-0 hazard

- dynamic hazard: when the output is supposed to change from 0 to 1 (or 1 to 0), the output may change three or more times, then it is a dynamic hazard

- We can detect hazards in a two-level AND-OR circuit, using the following procedure:

1. Write down the sum-of-products expressiong for the circuit

2. Plot each term on the map nad loop it

3. If any two adjacent 1's are not covered by the same loop, a 1-hazard exists for the transition between the two 1's. For an $n$-variable map, this transition occurs when one variable changes and the other $n-1$ variables are heldconstant

### Example 1

- $F=AB^{\prime}+BC$

<table>
	<thead>
		<tr>
			<th class='backslash'><div>$A$</div>$BC$</th>
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
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>

- $A=C=1;\,F=B^{\prime}+B=1$

<center markdown="block">
![hazard1-1](/assets/logic-circuit/img/8-4-hazard1-1.png)

Circuit

![hazard-timing-diagram1-1](/assets/logic-circuit/img/8-4-hazard-timing-diagram1-1.png)

Timing diagram

gate delay: 200 ns
</center>

- static 1-hazard

<table>
	<thead>
		<tr>
			<th class='backslash'><div>$A$</div>$BC$</th>
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
			<td></td>
			<td class="map2_2">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td class="map2">1</td>
			<td class="map2_2">1</td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>

- $F = AB^{\prime} + BC + AC$

<center markdown="block">
![hazard1-2](/assets/logic-circuit/img/8-4-hazard1-2.png)

Circuit

![hazard-timing-diagram1-2](/assets/logic-circuit/img/8-4-hazard-timing-diagram1-2.png)

Timing diagram

gate delay: 200 ns
</center>

- The term $AC$ remains 1 while $B$ is changing, so no glitch can appear in the output.

### Example 2

- $F = AA^{\prime} = 0$

<table>
	<thead>
		<tr>
			<th>$B$</th>
			<td>0</td>
			<td>1</td>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td></td>
			<td class="map1">0</td>
			<td class="map1">0</td>
		</tr>
	</tbody>
</table>

<center markdown="block">
![hazard2](/assets/logic-circuit/img/8-4-hazard2.png)

Circuit

![hazard-timing-diagram2](/assets/logic-circuit/img/8-4-hazard-timing-diagram2.png)

Timing diagram

gate delay: 200 ns
</center>

- static 0-hazard

---

## HW4

### 2

- 2-bit multiplier

- 7-segment

<center markdown="block">
![2](/assets/logic-circuit/img/8-hw-2.png)
</center>

##### Circuit

<center markdown="block">
![circuit](/assets/logic-circuit/img/8-hw-2-circuit.png)

Circuit

![ex1](/assets/logic-circuit/img/8-hw-2-circuit-ex1.png)

$2 \times 2 = 4$

![ex2](/assets/logic-circuit/img/8-hw-2-circuit-ex2.png)

$3 \times 3 = 9$
</center>

##### BCD(Binary Coded Decimal) to 7 Segment Decoder

<center markdown="block">
![7seg](/assets/logic-circuit/img/8-hw-7seg.png)

7 Segment
</center>

<table>
	<caption>Truth table</caption>
	<thead>
		<tr>
			<th>$A$</th>
			<th class="left-none">$B$</th>
			<th class="left-none">$C$</th>
			<th class="left-none">$D$</th>
			<th>$F_1$</th>
			<th class="left-none">$F_2$</th>
			<th class="left-none">$F_3$</th>
			<th class="left-none">$F_4$</th>
			<th class="left-none">$F_5$</th>
			<th class="left-none">$F_6$</th>
			<th class="left-none">$F_7$</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
			<td class="left-none">x</td>
		</tr>
	</tbody>
</table>

<table>
	<caption>$F_1$</caption>
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
			<td></td>
			<td class="map3">1</td>
			<td class="map3_4">x</td>
			<td class="map4">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td></td>
			<td class="map3">1</td>
			<td class="map3_4">x</td>
			<td class="map4">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td class="map3">1</td>
			<td></td>
			<td class="map4">x</td>
			<td class="map3_4">x</td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map3_3">1</td>
			<td class="map3">1</td>
			<td class="map3_4">x</td>
			<td class="map3_3_4">x</td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
F_1 &= A+BC^{\prime}+B^{\prime}C+CD^{\prime} \\
    &= A+BC^{\prime}+C(B^{\prime}+D^{\prime}) \\
	&= (A^{\prime}(BC^{\prime})^{\prime}(C(BD)^{\prime})^{\prime})^{\prime} \\
\end{align*}
$$

<table>
	<caption>$F_2$</caption>
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
			<td class="map3_4">1</td>
			<td class="map3_4_4">x</td>
			<td class="map3_4">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td></td>
			<td class="map4">1</td>
			<td class="map4_4">x</td>
			<td class="map4">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td class="map4">1</td>
			<td class="map4_4">x</td>
			<td class="map4">x</td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td class="map4">1</td>
			<td class="map4_4">x</td>
			<td class="map4">x</td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
F_2 &= B+A+C^{\prime}D^{\prime} \\
    &= (B^{\prime}A^{\prime}(C^{\prime}D^{\prime})^{\prime})^{\prime}
\end{align*}
$$

<table>
	<caption>$F_3$</caption>
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
			<td></td>
			<td class="map4">x</td>
			<td class="map3_4">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td></td>
			<td class="map3">1</td>
			<td class="map3_4">x</td>
			<td class="map4">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td class="map4">1</td>
			<td class="map3_4">1</td>
			<td class="map3_4_4">x</td>
			<td class="map4_4">x</td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map3_4">1</td>
			<td class="map4">1</td>
			<td class="map4_4">x</td>
			<td class="map3_4_4">x</td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
F_3 &= A+C+(B \oplus D)^{\prime} \\
    &= (A^{\prime}C^{\prime}(B \oplus D))^{\prime}
\end{align*}
$$

<table>
	<caption>$F_4$</caption>
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
			<td class="map3_4">1</td>
			<td class="map3">1</td>
			<td class="map3">x</td>
			<td class="map3_4">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map4">1</td>
			<td></td>
			<td>x</td>
			<td class="map4">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td class="map3_4">1</td>
			<td class="map3">1</td>
			<td class="map3">x</td>
			<td class="map3_4">x</td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map4">1</td>
			<td></td>
			<td>x</td>
			<td class="map4">x</td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
F_4 &= A+B^{\prime}+(C \oplus D)^{\prime} \\
    &= (A^{\prime}B(C \oplus D))^{\prime}
\end{align*}
$$

<table>
	<caption>$F_4$</caption>
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
			<td></td>
			<td>x</td>
			<td class="map3">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td></td>
			<td></td>
			<td>x</td>
			<td></td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td></td>
			<td>x</td>
			<td>x</td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map3_3">1</td>
			<td class="map3">1</td>
			<td class="map3">x</td>
			<td class="map3_3">x</td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
F_5 &= B^{\prime}D^{\prime}+CD^{\prime} \\
    &= D^{\prime}(B^{\prime}+C) \\
	&= (D+(B^{\prime}+C)^{\prime})^{\prime}
\end{align*}
$$

<table>
	<caption>$F_6$</caption>
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
			<td></td>
			<td>x</td>
			<td class="map3_3">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td></td>
			<td class="map2">1</td>
			<td class="map2">x</td>
			<td class="map3">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td class="map3">1</td>
			<td></td>
			<td>x</td>
			<td class="map3_3">x</td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map3_3_3">1</td>
			<td class="map3">1</td>
			<td class="map3">x</td>
			<td class="map3_3_3">x</td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
F_6 &= B^{\prime}D^{\prime}+B^{\prime}C+CD^{\prime}+BC^{\prime}D \\
    &= B^{\prime}(D^{\prime}+C)+CD^{\prime}+BC^{\prime}D \\
	&= ((B^{\prime}(DC^{\prime})^{\prime})^{\prime}(CD^{\prime})^{\prime}(BC^{\prime}D)^{\prime})^{\prime}
\end{align*}
$$

<table>
	<caption>$F_7$</caption>
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
			<td class="map4">1</td>
			<td class="map4_4">1</td>
			<td class="map4_4">x</td>
			<td class="map4">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map4_4">1</td>
			<td class="map4_4_4">1</td>
			<td class="map4_4_4">x</td>
			<td class="map4_4">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td class="map4">1</td>
			<td class="map4_4">1</td>
			<td class="map4_4">x</td>
			<td class="map4">x</td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td class="map4">1</td>
			<td class="map4">x</td>
			<td>x</td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
F_7 &= C^{\prime}+D+B \\
    &= (CD^{\prime}B^{\prime})^{\prime}
\end{align*}
$$

<center markdown="block">
![bcd-to-7seg](/assets/logic-circuit/img/8-hw-bcd-to-7seg.png)

Circuit

![bcd-to-7seg-block](/assets/logic-circuit/img/8-hw-bcd-to-7seg-block.png)

Block
</center>

##### 2-bit Multiplier

<table>
	<caption>Truth table</caption>
	<thead>
		<tr>
			<th>$A_1$</th>
			<th class="left-none">$A_0$</th>
			<th class="left-none">$B_1$</th>
			<th class="left-none">$B_0$</th>
			<th>$C_3$</th>
			<th class="left-none">$C_2$</th>
			<th class="left-none">$C_1$</th>
			<th class="left-none">$C_0$</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td>0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
			<td>0</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">0</td>
		</tr>
		<tr>
			<td>1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td class="left-none">1</td>
			<td>1</td>
			<td class="left-none">0</td>
			<td class="left-none">0</td>
			<td class="left-none">1</td>
		</tr>
	</tbody>
</table>

<table>
	<caption>$C_3$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$A_1A_0$</div>$B_1B_0$</th>
			<th>00</th>
			<th>01</th>
			<th>11</th>
			<th>10</th>
		 </tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>01</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td></td>
			<td class="map1">1</td>
			<td></td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
C_3 &= A_1A_0B_1B_0 \\
    &= (A_1^{\prime}+A_0^{\prime}+B_1^{\prime}+B_0^{\prime})^{\prime}
\end{align*}
$$

<table>
	<caption>$C_2$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$A_1A_0$</div>$B_1B_0$</th>
			<th>00</th>
			<th>01</th>
			<th>11</th>
			<th>10</th>
		 </tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>01</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td></td>
			<td></td>
			<td class="map2">1</td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td></td>
			<td class="map2">1</td>
			<td class="map2_2">1</td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
C_2 &= A_1B_1B_0^{\prime} + A_1A_0^{\prime}B_1 \\
    &= A_1B_1(B_0^{\prime}+A_0^{\prime}) \\
	&= (A_1^{\prime}+B_1^{\prime}+(B_0^{\prime}+A_0^{\prime})^{\prime})^{\prime}
\end{align*}
$$

<table>
	<caption>$C_1$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$A_1A_0$</div>$B_1B_0$</th>
			<th>00</th>
			<th>01</th>
			<th>11</th>
			<th>10</th>
		 </tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>01</th>
			<td></td>
			<td></td>
			<td class="map2">1</td>
			<td class="map2_2">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td class="map2">1</td>
			<td></td>
			<td class="map2">1</td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td class="map2_2">1</td>
			<td class="map2">1</td>
			<td></td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
C_1 &= A_1B_1^{\prime}B_0+A_1A_0^{\prime}B_0+A_1^{\prime}A_0B_1+A_0B_1B_0^{\prime} \\
	&= A_1B_0(B_1^{\prime}+A_0^{\prime})+A_0B_1(A_1^{\prime}+B_0^{\prime}) \\
	&= ((A_1B_0(B_1A_0)^{\prime})^{\prime}(A_0B_1(A_1B_0)^{\prime})^{\prime})^{\prime}
\end{align*}
$$

<table>
	<caption>$C_0$</caption>
	<thead>
		<tr>
			<th class='backslash'><div>$A_1A_0$</div>$B_1B_0$</th>
			<th>00</th>
			<th>01</th>
			<th>11</th>
			<th>10</th>
		 </tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>01</th>
			<td></td>
			<td class="map3">1</td>
			<td class="map3">1</td>
			<td></td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td class="map3">1</td>
			<td class="map3">1</td>
			<td></td>
		</tr>
		 <tr>
			<th>10</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
C_0 &= A_0B_0 \\
    &= (A_0^{\prime}+B_0^{\prime})^{\prime}
\end{align*}
$$

<center markdown="block">
![2-bit-multiplier](/assets/logic-circuit/img/8-hw-2-bit-multiplier.png)

Circuit

![2-bit-multiplier-block](/assets/logic-circuit/img/8-hw-2-bit-multiplier-block.png)

Block
</center>


