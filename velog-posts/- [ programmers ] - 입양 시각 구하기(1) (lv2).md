<h3 id="문제-설명">문제 설명</h3>
<p><code>ANIMAL_OUTS</code> 테이블은 동물 보호소에서 입양 보낸 동물의 정보를 담은 테이블입니다. <code>ANIMAL_OUTS</code> 테이블 구조는 다음과 같으며, <code>ANIMAL_ID</code>, <code>ANIMAL_TYPE</code>, <code>DATETIME</code>, <code>NAME</code>, <code>SEX_UPON_OUTCOME</code>는 각각 동물의 아이디, 생물 종, 입양일, 이름, 성별 및 중성화 여부를 나타냅니다.</p>
<h4 id="문제">문제</h4>
<p>보호소에서는 몇 시에 입양이 가장 활발하게 일어나는지 알아보려 합니다. 09:00부터 19:59까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요. 이때 결과는 시간대 순으로 정렬해야 합니다.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>ANIMAL_OUTS</p>
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
<td>NAME</td>
<td>VARCHAR(N)</td>
<td>TRUE</td>
</tr>
<tr>
<td>SEX_UPON_OUTCOME</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>일단 몇 시에 가장 활발히 구하기 위해서는 시간별로 정보를 나눠서 봐야합니다. 따라서 <code>GROUP BY</code>를 사용하여 시간대별로 데이터를 조회합니다. 그리고 9시부터 19시 59분까지 조회를 하기 위해 <code>HAVING</code>을 사용하여 그룹을 필터링했습니다. 마지막으로 시간순으로 데이터를 정렬하기 위해 <code>ORDER BY</code>를 사용했습니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    HOUR(DATETIME) as HOUR,
    count(*) as COUNT
from ANIMAL_OUTS
group by HOUR(DATETIME)
having HOUR between 9 and 19
order by HOUR</code></pre>