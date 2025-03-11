<h3 id="문제-설명">문제 설명</h3>
<p><code>AIR_POLLUTION</code> 테이블은 전국의 월별 미세먼지 정보를 담은 테이블입니다. <code>AIR_POLLUTION</code> 테이블의 구조는 다음과 같으며 <code>LOCATION1</code>, <code>LOCATION2</code>, <code>YM</code>, <code>PM_VAL1</code>, <code>PM_VAL2</code>은 각각 지역구분1, 지역구분2, 측정일, 미세먼지 오염도, 초미세먼지 오염도를 의미합니다.</p>
<h3 id="문제">문제</h3>
<p><code>AIR_POLLUTION</code> 테이블에서 수원 지역의 연도 별 평균 미세먼지 오염도와 평균 초미세먼지 오염도를 조회하는 SQL문을 작성해주세요. 이때, 평균 미세먼지 오염도와 평균 초미세먼지 오염도의 컬럼명은 각각 PM10, PM2.5로 해 주시고, 값은 소수 셋째 자리에서 반올림해주세요.
결과는 연도를 기준으로 오름차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>AIR_POLLUTION</p>
<table>
<thead>
<tr>
<th>Column Name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>LOCATION1</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>LOCATION2</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>YM</td>
<td>DATE</td>
<td>FALSE</td>
</tr>
<tr>
<td>PM_VAL1</td>
<td>NUMBER</td>
<td>FALSE</td>
</tr>
<tr>
<td>PM_VAL2</td>
<td>NUMBER</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저 연도별 수원에 대한 데이터를 뽑기 위해 <code>GROUP BY</code>를 사용합니다. 그 다음 각 미세먼지 별로 평균을 낸 뒤 반올림을 하기 위해 <code>AVG()</code>와 <code>ROUND()</code>함수를 사용합니다. 마지막으로 데이터 정렬을 위해 <code>ORDER BY</code>를 사용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">select
    year(YM) as &quot;YEAR&quot;,
    ROUND(AVG(PM_VAL1), 2) as 'PM10',
    ROUND(AVG(PM_VAL2), 2) as 'PM2.5'
from AIR_POLLUTION
where LOCATION2 = &quot;수원&quot;
group by year(YM)
order by year(YM)</code></pre>