<h3 id="문제-설명">문제 설명</h3>
<p><code>ANIMAL_INS</code> 테이블은 동물 보호소에 들어온 동물의 정보를 담은 테이블입니다. <code>ANIMAL_INS</code> 테이블 구조는 다음과 같으며, <code>ANIMAL_ID</code>, <code>ANIMAL_TYPE</code>, <code>DATETIME</code>, <code>INTAKE_CONDITION</code>, <code>NAME</code>, <code>SEX_UPON_INTAKE</code>는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.</p>
<h3 id="문제">문제</h3>
<p>동물 보호소에 들어온 동물 중 고양이와 개가 각각 몇 마리인지 조회하는 SQL문을 작성해주세요. 이때 고양이를 개보다 먼저 조회해주세요.</p>
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
<p>먼저 생물 종으로 나누고 생물들의 수를 세야하기 때문에 <code>GROUP BY</code>로 생물 종을 나눕니다. 그리고 생물 종 중 고양이와 개의 수를 세야하기 때문에 <code>having</code>을 사용하여 생물 종이 고양이거나 개인 그룹만 조회합니다. 그 다음 고양이와 개의 수를 세야하기 때문에 <code>count</code>를 사용하여 집계합니다. 마지막으로 고양이가 개보다 이름이 먼저나와야 하기 때문에 <code>order by</code>를 사용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    ANIMAL_TYPE,
    count(*)
from ANIMAL_INS
group by ANIMAL_TYPE
having ANIMAL_TYPE in ('Cat', 'Dog')
order by ANIMAL_TYPE</code></pre>