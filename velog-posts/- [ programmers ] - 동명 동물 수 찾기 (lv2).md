<h3 id="문제-설명">문제 설명</h3>
<p><code>ANIMAL_INS</code> 테이블은 동물 보호소에 들어온 동물의 정보를 담은 테이블입니다. <code>ANIMAL_INS</code> 테이블 구조는 다음과 같으며, <code>ANIMAL_ID</code>, <code>ANIMAL_TYPE</code>, <code>DATETIME</code>, <code>INTAKE_CONDITION</code>, <code>NAME</code>, <code>SEX_UPON_INTAKE</code>는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.</p>
<h3 id="문제">문제</h3>
<p>동물 보호소에 들어온 동물 이름 중 두 번 이상 쓰인 이름과 해당 이름이 쓰인 횟수를 조회하는 SQL문을 작성해주세요. 이때 결과는 이름이 없는 동물은 집계에서 제외하며, 결과는 이름 순으로 조회해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<table>
<thead>
<tr>
<th>NAME</th>
<th>TYPE</th>
<th>NULLABLE</th>
</tr>
</thead>
<tbody><tr>
<td>ANIMAL_ID</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
<tr>
<td>ANIMAL_TYPE</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
<tr>
<td>DATETIME</td>
<td>DATETIME</td>
<td>FALSE</td>
</tr>
<tr>
<td>INTAKE_CONDITION</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
<tr>
<td>NAME</td>
<td>VARCHAR(N)</td>
<td>TRUE</td>
</tr>
<tr>
<td>SEX_UPON_INTAKE</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저 문제에서 동물 이름이 두 번 이상 쓰인 이름을 찾기 위해 집계 함수를 사용해야겠다고 생각했습니다. 따라서 <code>NAME</code>으로 <code>GROUP BY</code>를 하여 데이터의 수를 <code>COUNT()</code>로 계산했습니다. 그리고 동물 이름이 두 번 이상 쓰인 이름을 찾기 위해선 <code>COUNT(*) &gt;= 2</code> 를 <code>HAVING</code>에 넣어 필터링을 했습니다. 그리고 이름에 NULL값이 없어야 하기 때문에 <code>WHERE</code>에서 <code>is NOT NULL</code>을 사용했습니다. 마지막으로 이름을 기준으로 정렬하기 위해 <code>ORDER BY</code>를 사용했습니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT 
    NAME,
    count(ANIMAL_ID) as COUNT
from ANIMAL_INS
where name is NOT NULL
group by NAME
having count(*) &gt;= 2
order by NAME</code></pre>