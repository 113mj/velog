<h3 id="문제-설명">문제 설명</h3>
<p>대장균들은 일정 주기로 분화하며, 분화를 시작한 개체를 부모 개체, 분화가 되어 나온 개체를 자식 개체라고 합니다.
다음은 실험실에서 배양한 대장균들의 정보를 담은 <code>ECOLI_DATA</code> 테이블입니다. <code>ECOLI_DATA</code> 테이블의 구조는 다음과 같으며, <code>ID</code>, <code>PARENT_ID</code>, <code>SIZE_OF_COLONY</code>, <code>DIFFERENTIATION_DATE</code>, <code>GENOTYPE</code> 은 각각 대장균 개체의 ID, 부모 개체의 ID, 개체의 크기, 분화되어 나온 날짜, 개체의 형질을 나타냅니다.</p>
<p>최초의 대장균 개체의 <code>PARENT_ID</code> 는 NULL 값입니다.</p>
<h3 id="문제">문제</h3>
<p>부모의 형질을 모두 보유한 대장균의 ID(<code>ID</code>), 대장균의 형질(<code>GENOTYPE</code>), 부모 대장균의 형질(<code>PARENT_GENOTYPE</code>)을 출력하는 SQL 문을 작성해주세요. 이때 결과는 ID에 대해 오름차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<table>
<thead>
<tr>
<th>Column name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>ID</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>PARENT_ID</td>
<td>INTEGER</td>
<td>TRUE</td>
</tr>
<tr>
<td>SIZE_OF_COLONY</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>DIFFERENTIATION_DATE</td>
<td>DATE</td>
<td>FALSE</td>
</tr>
<tr>
<td>GENOTYPE</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저 문제에서 준 예시를 보여주겠습니다. 예시는 다음과 같습니다.</p>
<table>
<thead>
<tr>
<th>ID</th>
<th>PARENT_ID</th>
<th>SIZE_OF_COLONY</th>
<th>DIFFERENTIATION_DATE</th>
<th>GENOTYPE</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>NULL</td>
<td>10</td>
<td>2019/01/01</td>
<td>1</td>
</tr>
<tr>
<td>2</td>
<td>1</td>
<td>2</td>
<td>2019/01/01</td>
<td>1</td>
</tr>
<tr>
<td>3</td>
<td>1</td>
<td>100</td>
<td>2020/01/01</td>
<td>3</td>
</tr>
<tr>
<td>4</td>
<td>2</td>
<td>16</td>
<td>2020/01/01</td>
<td>2</td>
</tr>
<tr>
<td>5</td>
<td>4</td>
<td>17</td>
<td>2020/01/01</td>
<td>8</td>
</tr>
<tr>
<td>6</td>
<td>3</td>
<td>101</td>
<td>2021/01/01</td>
<td>5</td>
</tr>
<tr>
<td>7</td>
<td>2</td>
<td>101</td>
<td>2022/01/01</td>
<td>5</td>
</tr>
<tr>
<td>8</td>
<td>6</td>
<td>1</td>
<td>2022/01/01</td>
<td>13</td>
</tr>
</tbody></table>
<p>각 대장균 별 형질을 2진수로 나타내면 다음과 같습니다.</p>
<p>ID 1 : 1₍₂₎
ID 2 : 1₍₂₎
ID 3 : 11₍₂₎
ID 4 : 10₍₂₎
ID 5 : 1000₍₂₎
ID 6 : 101₍₂₎
ID 7 : 101₍₂₎
ID 8 : 1101₍₂₎</p>
<p>각 대장균 별 보유한 형질을 다음과 같습니다.</p>
<p>ID 1 : 1
ID 2 : 1
ID 3 : 1, 2
ID 4 : 2
ID 5 : 4
ID 6 : 1, 3
ID 7 : 1, 3
ID 8 : 1, 3, 4</p>
<p>각 개체별로 살펴보면 다음과 같습니다.</p>
<p>ID 1 : 최초의 대장균 개체이므로 부모가 없습니다.
ID 2 : 부모는 ID 1 이며 부모의 형질인 1번 형질을 보유하고 있습니다.
ID 3 : 부모는 ID 1 이며 부모의 형질인 1번 형질을 보유하고 있습니다.
ID 4 : 부모는 ID 2 이며 부모의 형질인 1번 형질을 보유하고 있지 않습니다.
ID 5 : 부모는 ID 4 이며 부모의 형질인 2번 형질을 보유하고 있지 않습니다.
ID 6 : 부모는 ID 3 이며 부모의 형질 1, 2번 중 2 번 형질을 보유하고 있지 않습니다.
ID 7 : 부모는 ID 2 이며 부모의 형질인 1번 형질을 보유하고 있습니다.
ID 8 : 부모는 ID 6 이며 부모의 형질 1, 3번을 모두 보유하고 있습니다.</p>
<p>따라서 부모의 형질을 모두 보유한 개체는 ID 2, ID 3, ID 7, ID 8입니다.</p>
<p>부모의 형질을 모두 보유한 대장균을 찾기 위해 <code>&amp;</code> 연산을 활용해야 합니다. <code>&amp;</code> 연산을 사용하면 두 개의 숫자를 비트 단위로 비교할 수 있으며, 부모의 형질을 포함하고 있는지를 판별할 수 있습니다. 예를 들어, 어떤 개체의 <code>GENOTYPE</code>값과 부모의 <code>GENOTYPE</code> 값을 <code>&amp;</code> 연산했을 때 그 결과가 부모의 <code>GENOTYPE</code> 값과 동일하면, 부모의 형질을 모두 보유하고 있다고 볼 수 있습니다.</p>
<p>그러나 데이터에서 부모와 자식의 형질을 직접 비교할 수 있는 컬럼이 없기 때문에, 부모와 자식 데이터를 연결해야 합니다. 이를 위해 <code>JOIN</code>을 사용하여 부모 대장균의 데이터를 자식 개체와 결합합니다.</p>
<p>이후 <code>WHERE</code> 절에서 <code>&amp;</code> 연산을 수행하여 부모의 형질을 모두 보유한 개체만 필터링합니다. 마지막으로, <code>ID</code> 값을 기준으로 오름차순 정렬(<code>ORDER BY ID</code>)을 수행하여 결과를 출력합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">select 
    c.ID, 
    c.GENOTYPE, 
    p.GENOTYPE AS PARENT_GENOTYPE
from ECOLI_DATA c
JOIN ECOLI_DATA p ON c.PARENT_ID = p.ID
WHERE (c.GENOTYPE &amp; p.GENOTYPE) = p.GENOTYPE  
order by c.ID ;</code></pre>