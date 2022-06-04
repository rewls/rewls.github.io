---
layout: default
title: Ch6 Quine-McCluskey Method
parent: Logic Circuit
grand_parent: School Lecture
nav_order: 6
mathjax: true
permalink: /docs/logic-circuit/ch6
---

# Ch6 Quine-McCluskey Method
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

- k-map의 단점: 변수가 5개 이상이면 계산하기 힘들고 경험이나 노하우로 계산해야 한다.

- Quine-McCluskey Method, Petrick's Method를 이용하여 알고리즘적으로 계산할 수 있다.

	- 프로그래밍 가능

## 6.1 Determination of Prime Implicants

- $XY + XY^{\prime} = X$

- 알고리즘적으로 prime implicant를 찾을 수 있다.

### Step

1. $n$개의 variable이 있을 때, 각 minterm을 $n$-bit binary로 표현하고 1의 개수에 따라 group을 나눈다.

2. 이웃한 그룹 간에 1-bit 차이나는 term을 묶는다.

	- 사용한 term은 체크한다.

3. 이웃한 그룹 간에 1-bit 차이나는 term이 없어질 때까지 2.를 반복한다.

4. 체크되지 않은 term이 prime implicant이다.

### Example 1

- $f(a,b,c,d) = \sum m(0,1,2,5,6,7,8,9,10,14)$

<table>
	<thead>
		<tr>
			<th colspan='3'>Column 1</th>
			<th colspan='3'>Column 2</th>
			<th colspan='3'>Column 3</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>group 0</th>
			<td class="map1">0</td>
			<td class="map1">0000</td>
			<th rowspan='3'>group 0, 1</th>
			<td class="map1">0, 1</td>
			<td class="map1">000-</td>
			<th rowspan='4'>group<br>(0, 1), (1, 2)</th>
			<td>0, 1, 8, 9</td>
			<td>-00-</td>
		</tr>
		<tr>
			<th rowspan='3'>group 1</th>
			<td class="map1">1</td>
			<td class="map1">0001</td>
			<td class="map1">0, 2</td>
			<td class="map1">00-0</td>
			<td>0, 2, 8, 10</td>
			<td>-0-0</td>
		</tr>
		<tr>
			<td class="map1">2</td>
			<td class="map1">0010</td>
			<td class="map1">0, 8</td>
			<td class="map1">-000</td>
			<td><strike>0, 8, 1, 9</strike></td>
			<td><strike>-00-</strike></td>
		</tr>
		<tr>
			<td class="map1">8</td>
			<td class="map1">1000</td>
			<th rowspan='6'>group 1, 2</th>
			<td>1, 5</td>
			<td>0-01</td>
			<td><strike>0, 8, 2, 10</strike></td>
			<td><strike>-0-0</strike></td>
		</tr>
		<tr>
			<th rowspan='4'>group 2</th>
			<td class="map1">5</td>
			<td class="map1">0101</td>
			<td class="map1">1, 9</td>
			<td class="map1">-001</td>
			<th rowspan='2'>group<br>(1, 2), (2, 3)</th>
			<td>2, 6, 10, 14</td>
			<td>--10</td>
		</tr>
		<tr>
			<td class="map1">6</td>
			<td class="map1">0110</td>
			<td class="map1">2, 6</td>
			<td class="map1">0-10</td>
			<td><strike>2, 10, 6, 14</strike></td>
			<td><strike>--10</strike></td>
		</tr>
		<tr>
			<td class="map1">9</td>
			<td class="map1">1001</td>
			<td class="map1">2, 10</td>
			<td class="map1">-010</td>
		</tr>
		<tr>
			<td class="map1">10</td>
			<td class="map1">1010</td>
			<td class="map1">8, 9</td>
			<td class="map1">100-</td>
		</tr>
		<tr>
			<th rowspan='2'>group 3</th>
			<td class="map1">7</td>
			<td class="map1">0111</td>
			<td class="map1">8, 10</td>
			<td class="map1">10-0</td>
		</tr>
		<tr>
			<td class="map1">14</td>
			<td class="map1">1110</td>
			<th rowspan='4'>group 2, 3</th>
			<td>5, 7</td>
			<td>01-1</td>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
			<td>6, 7</td>
			<td>011-</td>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">6, 14</td>
			<td class="map1">-110</td>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">10, 14</td>
			<td class="map1">1-10</td>
		</tr>
	</tbody>
</table>

- 6개의 prime implicant가 있다.

##### Karnaugh map

<table>
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
			<td class="map2_2_2">1</td>
			<td></td>
			<td></td>
			<td class="map2_2">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map2_2">1</td>
			<td class="map2_2">1</td>
			<td></td>
			<td class="map2_2">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td class="map2_2">1</td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map2_2_2">1</td>
			<td class="map2_2">1</td>
			<td class="map2_2">1</td>
			<td class="map2_2_2">1</td>
		</tr>
	</tbody>
</table>

- Column 2: 2개 묶음 implicant

<table>
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
			<td class="map3_3">1</td>
			<td></td>
			<td></td>
			<td class="map3_3">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map3">1</td>
			<td>1</td>
			<td></td>
			<td class="map3">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td>1</td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map3_3">1</td>
			<td class="map3">1</td>
			<td class="map3">1</td>
			<td class="map3_3">1</td>
		</tr>
	</tbody>
</table>

- Column 3: 4개 묶음 implicant

<table>
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
			<td class="map3_3">1</td>
			<td></td>
			<td></td>
			<td class="map3_3">1</td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map2_3">1</td>
			<td class="map2_2">1</td>
			<td></td>
			<td class="map3">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td class="map2_2">1</td>
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map3_3">1</td>
			<td class="map2_3">1</td>
			<td class="map3">1</td>
			<td class="map3_3">1</td>
		</tr>
	</tbody>
</table>

- prime implicant 6개

### Example 2

- $F(a,b,c) = \sum m(0,1,2,5,6,7)$

<table>
	<thead>
		<tr>
			<th colspan='3'>Column 1</th>
			<th colspan='3'>Column 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>group 0</th>
			<td class="map1">0</td>
			<td class="map1">000</td>
			<th rowspan='2'>group 0, 1</th>
			<td>0, 1</td>
			<td>00-</td>
		</tr>
		<tr>
			<th rowspan='2'>group 1</th>
			<td class="map1">1</td>
			<td class="map1">001</td>
			<td>0, 2</td>
			<td>0-0</td>
		</tr>
		<tr>
			<td class="map1">2</td>
			<td class="map1">010</td>
			<th rowspan='2'>group 1, 2</th>
			<td>1, 5</td>
			<td>-01</td>
		</tr>
		<tr>
			<th rowspan='2'>group 2</th>
			<td class="map1">5</td>
			<td class="map1">101</td>
			<td>2, 6</td>
			<td>-10</td>
		</tr>
		<tr>
			<td class="map1">6</td>
			<td class="map1">110</td>
			<th rowspan='2'>group 2, 3</th>
			<td>5, 7</td>
			<td>1-1</td>
		</tr>
		<tr>
			<th>group 3</th>
			<td class="map1">7</td>
			<td class="map1">111</td>
			<td>6, 7</td>
			<td>11-</td>
		</tr>
	</tbody>
</table>

- prime implicant 6개

##### Karnaugh map

<table>
	<thead>
		<tr>
			<th class='backslash'><div>$a$</div>$bc$</th>
			<th>0</th>
			<th>1</th>
		 </tr>
	</thead>
	<tbody>
		 <tr>
			<th>00</th>
			<td class="map2_2">1</td>
			<td></td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map2_2">1</td>
			<td class="map2_2">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td></td>
			<td class="map2_2">1</td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map2_2">1</td>
			<td class="map2_2">1</td>
		</tr>
	</tbody>
</table>

- Column 2: 2개 묶음 implicant 6개

---

## 6.2 The Prime Implicant Chart

### Step

1. 위에서 찾은 prime implicant의 expression과 minterm 조합을 row head에 적고 minterm을 coloumn head에 적는다.

2. 각 prime implicant이 cover하는 minterm에 $\times$ 표시한다.

3. column에 $\times$가 1개 있는 셀을 찾고 해당 implicant가 cover하는 $\times$를 표시한다.

	- column에 $\times$가 1개 있는 셀의 implicant가 essential prime implicant이다.

4. essential prime implicant가 cover하는 $\times$의 column에 위치한 $\times$를 지운다.

5. $\times$가 남았다면 적절한 prime implicant를 선택하여 $\times$를 표시하고 해당 $\times$의 column에 위치한 $\times$을 지워 남는 $\times$가 없도록 한다.

### Example 1

- $f(a,b,c,d) = \sum m(0,1,2,5,6,7,8,9,10,14)$

<table>
	<thead>
		<tr>
			<th></th>
			<th></th>
			<th></th>
			<th>0</th>
			<th>1</th>
			<th>2</th>
			<th>5</th>
			<th>6</th>
			<th>7</th>
			<th>8</th>
			<th>9</th>
			<th>10</th>
			<th>14</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th class="map4">0, 1, 8, 9</th>
			<th class="map4">$b^{\prime}c^{\prime}$</th>
			<td class="map2">$\times$</td>
			<td class="map2">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map2">$\times$</td>
			<td class="map4">$\times$</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>0, 2, 8, 10</th>
			<th>$b^{\prime}c^{\prime}$</th>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
		</tr>
		<tr>
			<th class="map4">2, 6, 10, 14</th>
			<th class="map4">$cd^{\prime}$</th>
			<td></td>
			<td></td>
			<td class="map2">$\times$</td>
			<td></td>
			<td class="map2">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map2">$\times$</td>
			<td class="map4">$\times$</td>
		</tr>
		<tr>
			<th>1, 5</th>
			<th>$a^{\prime}c^{\prime}d$</th>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th class="map3">5, 7</th>
			<th class="map3">$a^{\prime}bd$</th>
			<td></td>
			<td></td>
			<td></td>
			<td class="map3">$\times$</td>
			<td></td>
			<td class="map3">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>6, 7</th>
			<th>$a^{\prime}bc$</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">$\times$</td>
			<td class="map1">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>

- $f = b^{\prime}c^{\prime} + cd^{\prime} + a^{\prime}bd$

##### Karnaugh map

<table>
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
			<td></td>
			<td class="map3">1</td>
		</tr>
		<tr>
			<th>01</th>
			<td class="map3">1</td>
			<td class="map2">1</td>
			<td></td>
			<td class="map3">1</td>
		</tr>
		<tr>
			<th>11</th>
			<td></td>
			<td class="map2">1</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>10</th>
			<td class="map3">1</td>
			<td class="map3">1</td>
			<td class="map3">1</td>
			<td class="map3">1</td>
		</tr>
	</tbody>
</table>

---

## 6.3 Petrick's Method

### Perpose

- 남은 term을 cover하면서 선택된 term의 개수가 가장 적어지도록 implicant 선택

### Step

1. $P_i$에 대하여 $P$를 정의한다. 각 minterm을 커버하는 prime implicant를 product of sum 형태로 정의한다.

	- $P$ is a logic functions, which is true when all of the minterms in the chart have been covered

	- $P_i$ is a logic variable, which is true when the prime implicant in row $P_i$ is included in the solution

2. $P$를 Sum of product로 정리한다.

3. $P$에서 literal 개수가 가장 적은 term을 선택한다.

### Example 1

- $f(a,b,c,d) = \sum m(0,1,2,5,6,7,8,9,10,14)$

<table>
	<thead>
		<tr>
			<th></th>
			<th></th>
			<th></th>
			<th>0</th>
			<th>1</th>
			<th>2</th>
			<th>5</th>
			<th>6</th>
			<th>7</th>
			<th>8</th>
			<th>9</th>
			<th>10</th>
			<th>14</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>$P_1$</th>
			<th>0, 1, 8, 9</th>
			<th class="map4">$b^{\prime}c^{\prime}$</th>
			<td class="map2">$\times$</td>
			<td class="map2">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map2">$\times$</td>
			<td class="map4">$\times$</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_2$</th>
			<th>0, 2, 8, 10</th>
			<th>$b^{\prime}c^{\prime}$</th>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
		</tr>
		<tr>
			<th>$P_3$</th>
			<th class="map4">2, 6, 10, 14</th>
			<th class="map4">$cd^{\prime}$</th>
			<td></td>
			<td></td>
			<td class="map2">$\times$</td>
			<td></td>
			<td class="map2">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map2">$\times$</td>
			<td class="map4">$\times$</td>
		</tr>
		<tr>
			<th>$P_4$</th>
			<th>1, 5</th>
			<th>$a^{\prime}c^{\prime}d$</th>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td>$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_5$</th>
			<th>5, 7</th>
			<th>$a^{\prime}bd$</th>
			<td></td>
			<td></td>
			<td></td>
			<td>$\times$</td>
			<td></td>
			<td>$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_6$</th>
			<th>6, 7</th>
			<th>$a^{\prime}bc$</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">$\times$</td>
			<td>$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>

$$
\begin{align*}
P &= (P_4+P_5)(P_5+P_6) \\
  &= P_5+P_4P_6
\end{align*}
$$

- 최소 1개의 prime implicant를 선택할 수 있다.

<table>
	<thead>
		<tr>
			<th></th>
			<th></th>
			<th></th>
			<th>0</th>
			<th>1</th>
			<th>2</th>
			<th>5</th>
			<th>6</th>
			<th>7</th>
			<th>8</th>
			<th>9</th>
			<th>10</th>
			<th>14</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>$P_1$</th>
			<th>0, 1, 8, 9</th>
			<th class="map4">$b^{\prime}c^{\prime}$</th>
			<td class="map2">$\times$</td>
			<td class="map2">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map2">$\times$</td>
			<td class="map4">$\times$</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_2$</th>
			<th>0, 2, 8, 10</th>
			<th>$b^{\prime}c^{\prime}$</th>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
		</tr>
		<tr>
			<th>$P_3$</th>
			<th class="map4">2, 6, 10, 14</th>
			<th class="map4">$cd^{\prime}$</th>
			<td></td>
			<td></td>
			<td class="map2">$\times$</td>
			<td></td>
			<td class="map2">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map2">$\times$</td>
			<td class="map4">$\times$</td>
		</tr>
		<tr>
			<th>$P_4$</th>
			<th>1, 5</th>
			<th>$a^{\prime}c^{\prime}d$</th>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_5$</th>
			<th>5, 7</th>
			<th>$a^{\prime}bd$</th>
			<td></td>
			<td></td>
			<td></td>
			<td class="map3">$\times$</td>
			<td></td>
			<td class="map3">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_6$</th>
			<th>6, 7</th>
			<th>$a^{\prime}bc$</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">$\times$</td>
			<td class="map1">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
	</tbody>
</table>

- $P_5$

### Example 2

$F = \sum m(0,1,2,5,6,7)$

<table>
	<thead>
		<tr>
			<th></th>
			<th></th>
			<th></th>
			<th>0</th>
			<th>1</th>
			<th>2</th>
			<th>5</th>
			<th>6</th>
			<th>7</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>$P_1$</th>
			<th>0, 1</th>
			<th>$a^{\prime}b^{\prime}$</th>
			<td>$\times$</td>
			<td>$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_2$</th>
			<th>0, 2</th>
			<th>$a^{\prime}c^{\prime}$</th>
			<td>$\times$</td>
			<td></td>
			<td>$\times$</td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_3$</th>
			<th>1, 5</th>
			<th>$b^{\prime}c$</th>
			<td></td>
			<td>$\times$</td>
			<td></td>
			<td>$\times$</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_4$</th>
			<th>2, 6</th>
			<th>$bc^{\prime}$</th>
			<td></td>
			<td></td>
			<td>$\times$</td>
			<td></td>
			<td>$\times$</td>
			<td></td>
		</tr>
		<tr>
			<th>$P_5$</th>
			<th>5, 7</th>
			<th>$ac$</th>
			<td></td>
			<td></td>
			<td></td>
			<td>$\times$</td>
			<td></td>
			<td>$\times$</td>
		</tr>
		<tr>
			<th>$P_6$</th>
			<th>6, 7</th>
			<th>$ab$</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td>$\times$</td>
			<td>$\times$</td>
		</tr>
	</tbody>
</table>

- essential prime implicant가 없다.

$$
\begin{align*}
P &= (P_1+P_2)(P_1+P_3)(P_2+P_4)(P_3+P_5)(P_4+P_6)(P_5+P_6) \\
  &= (P_1 + P_2P_3)(P_4+P_2P_6)(P_5+P_3P_6) \\
  &= (P_1P_4+P_1P_2P_6+P_2P_3P_4+P_2P_3P_6)(P_5+P_3P_6) \\
  &= P_1P_4P_5+P_1P_3P_4P_6+P_1P_2P_5P_6+P_1P_2P_3P_6+P_2P_3P_4P_5+P_2P_3P_4P_6+P_2P_3P_5P_6+P_2P_3P_6
\end{align*}
$$

- 최소 3개의 prime implicant를 선택할 수 있다.

<table>
	<thead>
		<tr>
			<th></th>
			<th></th>
			<th></th>
			<th>0</th>
			<th>1</th>
			<th>2</th>
			<th>5</th>
			<th>6</th>
			<th>7</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th class="map3">$P_1$</th>
			<th class="map3">0, 1</th>
			<th class="map3">$a^{\prime}b^{\prime}$</th>
			<td class="map3">$\times$</td>
			<td class="map3">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_2$</th>
			<th>0, 2</th>
			<th>$a^{\prime}c^{\prime}$</th>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_3$</th>
			<th>1, 5</th>
			<th>$b^{\prime}c$</th>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th class="map3">$P_4$</th>
			<th class="map3">2, 6</th>
			<th class="map3">$bc^{\prime}$</th>
			<td></td>
			<td></td>
			<td class="map3">$\times$</td>
			<td></td>
			<td class="map3">$\times$</td>
			<td></td>
		</tr>
		<tr>
			<th class="map3">$P_5$</th>
			<th class="map3">5, 7</th>
			<th class="map3">$ac$</th>
			<td></td>
			<td></td>
			<td></td>
			<td class="map3">$\times$</td>
			<td></td>
			<td class="map3">$\times$</td>
		</tr>
		<tr>
			<th>$P_6$</th>
			<th>6, 7</th>
			<th>$ab$</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">$\times$</td>
			<td class="map1">$\times$</td>
		</tr>
	</tbody>
</table>

- $P_1P_4P_5$

<table>
	<thead>
		<tr>
			<th></th>
			<th></th>
			<th></th>
			<th>0</th>
			<th>1</th>
			<th>2</th>
			<th>5</th>
			<th>6</th>
			<th>7</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>$P_1$</th>
			<th>0, 1</th>
			<th>$a^{\prime}b^{\prime}$</th>
			<td class="map1">$\times$</td>
			<td class="map1">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th class="map3">$P_2$</th>
			<th class="map3">0, 2</th>
			<th class="map3">$a^{\prime}c^{\prime}$</th>
			<td class="map3">$\times$</td>
			<td></td>
			<td class="map3">$\times$</td>
			<td></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th class="map3">$P_3$</th>
			<th class="map3">1, 5</th>
			<th class="map3">$b^{\prime}c$</th>
			<td></td>
			<td class="map3">$\times$</td>
			<td></td>
			<td class="map3">$\times$</td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<th>$P_4$</th>
			<th>2, 6</th>
			<th>$bc^{\prime}$</th>
			<td></td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
		</tr>
		<tr>
			<th>$P_5$</th>
			<th>5, 7</th>
			<th>$ac$</th>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
		</tr>
		<tr>
			<th class="map3">$P_6$</th>
			<th class="map3">6, 7</th>
			<th class="map3">$ab$</th>
			<td></td>
			<td></td>
			<td></td>
			<td></td>
			<td class="map3">$\times$</td>
			<td class="map3">$\times$</td>
		</tr>
	</tbody>
</table>

- $P_2P_3P_6$

---

## 6.4 Simplification of Incompletely Specified Functions

### Example

- $F(a,b,c,d) = \sum m(2,3,7,9,11,13) G \sum d(1, 10, 15)$

##### Karnaugh map

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
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>01</th>
			<td>x</td>
			<td></td>
			<td class="map3">1</td>
			<td class="map3">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td class="map3_3">1</td>
			<td class="map3">1</td>
			<td class="map3_3">x</td>
			<td class="map3_3_3">1</td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map3">1</td>
			<td></td>
			<td></td>
			<td class="map3">x</td>
		</tr>
	</tbody>
</table>

- prime implicant 4개, essential prime implicant 3개

##### Quine-mcCluskey method

- don't care term도 포함해서 적용한다.

<table>
	<thead>
		<tr>
			<th colspan='3'>Column 1</th>
			<th colspan='3'>Column 2</th>
			<th colspan='3'>Column 3</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th rowspan='2'>group 1</th>
			<td class="map1">1</td>
			<td class="map1">0001</td>
			<th rowspan='4'>group 1, 2</th>
			<td class="map1">1, 3</td>
			<td class="map1">00-1</td>
			<th rowspan='4'>group<br>(1, 2), (2, 3)</th>
			<td>1, 3, 9, 11</td>
			<td>-0-1</td>
		</tr>
		<tr>
			<td class="map1">2</td>
			<td class="map1">0010</td>
			<td class="map1">1, 9</td>
			<td class="map1">-001</td>
			<td><strike>1, 9, 3, 11</strike></td>
			<td><strike>-0-1</strike></td>
		</tr>
		<tr>
			<th rowspan='3'>group 2</th>
			<td class="map1">3</td>
			<td class="map1">0011</td>
			<td class="map1">2, 3</td>
			<td class="map1">001-</td>
			<td>2, 3, 10, 11</td>
			<td>-01-</td>
		</tr>
		<tr>
			<td class="map1">9</td>
			<td class="map1">1001</td>
			<td class="map1">2, 10</td>
			<td class="map1">-010</td>
			<td><strike>2, 10, 3, 11</strike></td>
			<td><strike>-01-</strike></td>
		</tr>
		<tr>
			<td class="map1">10</td>
			<td class="map1">1010</td>
			<th rowspan='5'>group 2, 3</th>
			<td class="map1">3, 7</td>
			<td class="map1">0-11</td>
			<th rowspan='4'>group<br>(2, 3), (3, 4)</th>
			<td>3, 7, 11, 15</td>
			<td>--11</td>
		</tr>
		<tr>
			<th rowspan='3'>group 3</th>
			<td class="map1">7</td>
			<td class="map1">0111</td>
			<td class="map1">3, 11</td>
			<td class="map1">-011</td>
			<td><strike>3, 11, 7, 15</strike></td>
			<td><strike>--11</strike></td>
		</tr>
		<tr>
			<td class="map1">11</td>
			<td class="map1">1011</td>
			<td class="map1">9, 11</td>
			<td class="map1">10-1</td>
			<td>9, 11, 13, 15</td>
			<td>1--1</td>
		</tr>
		<tr>
			<td class="map1">13</td>
			<td class="map1">1101</td>
			<td class="map1">9, 13</td>
			<td class="map1">1-01</td>
			<td><strike>9, 13, 11, 15</strike></td>
			<td><strike>1--1</strike></td>
		</tr>
		<tr>
			<th>group 4</th>
			<td class="map1">15</td>
			<td class="map1">1111</td>
			<td class="map1">10, 11</td>
			<td class="map1">101-</td>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
			<th rowspan='3'>group 3, 4</th>
			<td class="map1">7, 15</td>
			<td class="map1">-111</td>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">11, 15</td>
			<td class="map1">1-11</td>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
			<td class="map1">13, 15</td>
			<td class="map1">11-1</td>
		</tr>
	</tbody>
</table>

- prime implicant 4개

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
			<td></td>
			<td></td>
		</tr>
		 <tr>
			<th>01</th>
			<td class="map3">x</td>
			<td></td>
			<td class="map3">1</td>
			<td class="map3_3">1</td>
		</tr>
		 <tr>
			<th>11</th>
			<td class="map3_3_3">1</td>
			<td class="map3">1</td>
			<td class="map3_3">x</td>
			<td class="map3_3_3_3">1</td>
		</tr>
		 <tr>
			<th>10</th>
			<td class="map3">1</td>
			<td></td>
			<td></td>
			<td class="map3">x</td>
		</tr>
	</tbody>
</table>

##### Petrick's method

- column head에 don't care term을 빼고 적는다.

<table>
	<thead>
		<tr>
			<th></th>
			<th></th>
			<th></th>
			<th>2</th>
			<th>3</th>
			<th>7</th>
			<th>9</th>
			<th>11</th>
			<th>13</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<th>$P_1$</th>
			<th>1, 3, 9, 11</th>
			<th>$b^{\prime}d$</th>
			<td></td>
			<td class="map1">$\times$</td>
			<td></td>
			<td class="map1">$\times$</td>
			<td class="map1">$\times$</td>
			<td></td>
		</tr>
		<tr>
			<th class="map4">$P_2$</th>
			<th class="map4">2, 3, 10, 11</th>
			<th class="map4">$b^{\prime}c$</th>
			<td class="map4">$\times$</td>
			<td class="map2">$\times$</td>
			<td></td>
			<td></td>
			<td class="map2">$\times$</td>
			<td></td>
		</tr>
		<tr>
			<th class="map4">$P_3$</th>
			<th class="map4">3, 7, 11, 15</th>
			<th class="map4">$cd$</th>
			<td></td>
			<td class="map2">$\times$</td>
			<td class="map4">$\times$</td>
			<td></td>
			<td class="map2">$\times$</td>
			<td></td>
		</tr>
		<tr>
			<th class="map4">$P_4$</th>
			<th class="map4">9, 11, 13, 15</th>
			<th class="map4">$ad$</th>
			<td></td>
			<td></td>
			<td></td>
			<td class="map2">$\times$</td>
			<td class="map2">$\times$</td>
			<td class="map4">$\times$</td>
		</tr>
	</tbody>
</table>

- essential implicant 3개
