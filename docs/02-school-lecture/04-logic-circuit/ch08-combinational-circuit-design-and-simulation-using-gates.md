---
layout: default
title: Ch8 Combinational Circuit Design and Simulation Using Gates
parent: Logic Circuit
grand_parent: School Lecture
nav_order: 8
mathjax: true
permalink: /docs/logic-circuit/ch8
---

<style>
.backslash {
  background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg"><line x1="0" y1="0" x2="100%" y2="100%" stroke="gray" /></svg>');
}
.slash, .backslash {
  text-align: left;
  padding: 0px 40px 0px 40px;
}
.slash div, .backslash div {
  text-align: right;
}
.map1 {
  background: #EEEEEE;
}
.map2 {
  background: #EEEEFF;
}
.map3 {
  background: #EEFFEE;
}
.map2_2 {
  background: #DDDDFF;
}
td {
  text-align: center;
}
</style>

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
![3-input-nor](/assets/logic-circuit/8-2-3-input-nor.png)
</center>

##### Expression

$$
\begin{align*}
f &= (a^{\prime}+b^{\prime}+c)(a+c^{\prime}+b^{\prime}d)(b+d^{\prime}+(a+c)(a^{\prime}+c^{\prime})) \\
  &= [(a^{\prime}+b^{\prime}+c)^{\prime}+(a+c^{\prime}+b^{\prime}d)^{\prime}+(b+d^{\prime}+(a+c)(a^{\prime}+c^{\prime}))^{\prime}]^{\prime} \\
  &= [(a^{\prime}+b^{\prime}+c)^{\prime}+(a+c^{\prime}+(b+d^{\prime})^{\prime})^{\prime}+(b+d^{\prime}+((a+c)^{\prime}+(a^{\prime}+c^{\prime})^{\prime})^{\prime}]^{\prime}
\end{align*}
$$

## 8.3 Gate Delays and Timing Digrams

- When the input to a logic gate is changed, the output will not change instantaneously

- The transistors or other switching elements within the the gate take a finite time to react to a change in input, so that the change in the gate output is delayed with respect to the input change

### Example

<center markdown="block">
![gate-delay](/assets/logic-circuit/8-3-gate-delay.png)
</center>

- $B=1, C=0$

<center markdown="block">
![gate-delay-timing-diagram](/assets/logic-circuit/8-3-gate-delay-timing-diagram.png)
</center>

- gate delay: 10 ns

## 8.4 Hazards in Combinational Logic

- when the input to a combinational circuit changes, unwanted switching transients may appear in the output

- These transients occur when different paths from input to output have different propagation delays


### Example

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

- 1-hazard

- $A=C=1;\,F=B^{\prime}+B=1$

<center markdown="block">
![hazard](/assets/logic-circuit/8-4-hazard.png)

Circuit

![hazard-timing-diagram](/assets/logic-circuit/8-4-hazard-timing-diagram.png)

Timing diagram
</center>

- gate delay: 10 ns

