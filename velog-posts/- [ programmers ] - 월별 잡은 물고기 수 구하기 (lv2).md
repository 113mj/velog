<h3 id="문제-설명">문제 설명</h3>
<p>낚시앱에서 사용하는 <code>FISH_INFO</code> 테이블은 잡은 물고기들의 정보를 담고 있습니다. <code>FISH_INFO</code> 테이블의 구조는 다음과 같으며 <code>ID</code>, <code>FISH_TYPE</code>, <code>LENGTH</code>, <code>TIME</code>은 각각 잡은 물고기의 ID, 물고기의 종류(숫자), 잡은 물고기의 길이(cm), 물고기를 잡은 날짜를 나타냅니다.</p>
<h3 id="문제">문제</h3>
<p>월별 잡은 물고기의 수와 월을 출력하는 SQL문을 작성해주세요.</p>
<p>잡은 물고기 수 컬럼명은 <code>FISH_COUNT</code>, 월 컬럼명은 <code>MONTH</code>로 해주세요.
결과는 월을 기준으로 오름차순 정렬해주세요.
단, 월은 숫자형태 (1~12) 로 출력하며 9 이하의 숫자는 두 자리로 출력하지 않습니다. 잡은 물고기가 없는 월은 출력하지 않습니다.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>FISH_INFO</p>
<table>
<thead>
<tr>
<th>Column Name</th>
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
<td>FISH_TYPE</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>LENGTH</td>
<td>FLOAT</td>
<td>TRUE</td>
</tr>
<tr>
<td>TIME</td>
<td>DATE</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저 월별로 묶기 위해 <code>MONTH()</code> 과 <code>GROUP BY</code>를 사용합니다. 그 뒤 묶인 데이터별로 집계함수 <code>COUNT()</code>를 사용하여 물고기의 수를 셉니다. 마지막으로 정렬을 위해 <code>ORDER BY</code>를 사용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">select
    count(ID) as FISH_COUNT,
    month(TIME) as MONTH
from FISH_INFO
group by month(TIME)
order by MONTH</code></pre>