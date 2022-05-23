---
layout: default
title: Ch6 Quine-McCluskey Method
parent: Logic Circuit
grand_parent: School Lecture
nav_order: 6
mathjax: true
permalink: /docs/logic-circuit/ch6
---

<style>
.slash {
  background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg"><line x1="0" y1="100%" x2="100%" y2="0" stroke="gray" /></svg>');
}
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
.slash-left {
background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg"><polygon points="0 100 100 0 0 0"/></svg>');
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
.map4 {
  background: #FFEEEE;
}
.map1_1 {
  background: #DDDDDD;
}
.map2_2 {
  background: #DDDDFF;
}
.map3_3 {
  background: #DDFFDD;
}
.map4_4 {
  background: #FFDDDD;
}
.map2_2_2 {
  background: #CCCCFF;
}
.map2_3 {
  background: #EEFFFF;
}
.map3_4 {
  background: #FFFFEE;
}
.map2_4 {
  background: #FFEEFF;
}
td {
  text-align: center;
}
th {
  text-align: center;
}
</style>

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

## 6.1 Determination of Prime Implicants

$f(a,b,c,d) = \sum m(0,1,2,5,6,7,8,9,10,14)$

four variable일 때, 각 minterm을 4-bit binary로 group별로 표현한다.

group 0 0000

groutp n: 1의 개수가 n개인 항

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
			<td>0</td>
			<td>0000</td>
			<th rowspan='3'>group 0, 1</th>
			<td>0,1</td>
			<td>000-</td>
			<th rowspan='4'>group 0, 1, 2</th>
			<td>0, 1, 8, 9</td>
			<td>-00-</td>
		</tr>
		<tr>
			<th rowspan='3'>group 1</th>
			<td>1</td>
			<td>0001</td>
			<td>0,2</td>
			<td>00-0</td>
			<td>0, 2, 8, 10</td>
			<td>-0-0</td>
		</tr>
		<tr>
			<td>2</td>
			<td>0010</td>
			<td>0,8</td>
			<td>-000</td>
			<td class="map1">0, 8, 1, 9</td>
			<td class="map1">-00-</td>
		</tr>
		<tr>
			<td>8</td>
			<td>1000</td>
			<th rowspan='6'>group 1, 2</th>
			<td>1,5</td>
			<td>0-01</td>
			<td class="map1">0, 8, 2, 10</td>
			<td class="map1">-0-0</td>
		</tr>
		<tr>
			<th rowspan='4'>group 2</th>
			<td>5</td>
			<td>0101</td>
			<td>1,9</td>
			<td>-001</td>
			<th rowspan='2'>group 1,2,3</th>
			<td>2, 6, 10, 14</td>
			<td>--10</td>
		</tr>
		<tr>
			<td>6</td>
			<td>0110</td>
			<td>2,6</td>
			<td>0-10</td>
			<td class="map1">2, 10, 6, 14</td>
			<td class="map1">--10</td>
		</tr>
		<tr>
			<td>9</td>
			<td>1001</td>
			<td>2,10</td>
			<td>-010</td>
		</tr>
		<tr>
			<td>10</td>
			<td>1010</td>
			<td>8,9</td>
			<td>100-</td>
		</tr>
		<tr>
			<th rowspan='2'>group 3</th>
			<td>7</td>
			<td>0111</td>
			<td>8,10</td>
			<td>10-0</td>
		</tr>
		<tr>
			<td>14</td>
			<td>1110</td>
			<th rowspan='4'>group 2, 3</th>
			<td>5,7</td>
			<td>01-1</td>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
			<td>6,7</td>
			<td>011-</td>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
			<td>6,14</td>
			<td>-110</td>
		</tr>
		<tr>
			<td></td>
			<td></td>
			<td></td>
			<td>10,14</td>
			<td>1-10</td>
		</tr>
	</tbody>
</table>

- 1-bit 차이나는 조합을 묶는다.

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

