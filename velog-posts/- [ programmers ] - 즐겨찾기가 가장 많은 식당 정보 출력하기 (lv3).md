<h3 id="문제-설명">문제 설명</h3>
<p>다음은 식당의 정보를 담은 <code>REST_INFO</code> 테이블입니다. <code>REST_INFO</code> 테이블은 다음과 같으며 <code>REST_ID</code>, <code>REST_NAME</code>, <code>FOOD_TYPE</code>, <code>VIEWS</code>, <code>FAVORITES</code>, <code>PARKING_LOT</code>, <code>ADDRESS</code>, <code>TEL</code>은 식당 ID, 식당 이름, 음식 종류, 조회수, 즐겨찾기수, 주차장 유무, 주소, 전화번호를 의미합니다.</p>
<h3 id="문제">문제</h3>
<p><code>REST_INFO</code> 테이블에서 음식종류별로 즐겨찾기수가 가장 많은 식당의 음식 종류, ID, 식당 이름, 즐겨찾기수를 조회하는 SQL문을 작성해주세요. 이때 결과는 음식 종류를 기준으로 내림차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>REST_INFO</p>
<table>
<thead>
<tr>
<th>Column Name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>REST_ID</td>
<td>VARCHAR(5)</td>
<td>FALSE</td>
</tr>
<tr>
<td>REST_NAME</td>
<td>VARCHAR(50)</td>
<td>FALSE</td>
</tr>
<tr>
<td>FOOD_TYPE</td>
<td>VARCHAR(20)</td>
<td>TRUE</td>
</tr>
<tr>
<td>VIEWS</td>
<td>NUMBER</td>
<td>TRUE</td>
</tr>
<tr>
<td>FAVORITES</td>
<td>NUMBER</td>
<td>TRUE</td>
</tr>
<tr>
<td>PARKING_LOT</td>
<td>VARCHAR(1)</td>
<td>TRUE</td>
</tr>
<tr>
<td>ADDRESS</td>
<td>VARCHAR(100)</td>
<td>TRUE</td>
</tr>
<tr>
<td>TEL</td>
<td>VARCHAR(100)</td>
<td>TRUE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저 테이블에서 음식종류별 즐겨찾기가 가장 많은 수를 <code>OVER()</code>와 <code>MAX()</code>함수를 통해 뽑습니다. 그 다음 가장 높은 즐겨찾기를 가진 행을 <code>WHERE</code>를 통해 뽑은 뒤 <code>FOOD_TYPE</code>, <code>REST_ID</code>, <code>REST_NAME</code>, <code>FAVORITES</code>를 뽑습니다. 마지막으로 데이터 정렬을 위해 <code>ORDER BY</code>를 사용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">with temp1 as (
    SELECT
    *,
    MAX(FAVORITES) OVER(PARTITION BY FOOD_TYPE) as &quot;MAX&quot;
from REST_INFO
)
select
    FOOD_TYPE,
    REST_ID,
    REST_NAME,
    FAVORITES
from temp1
where FAVORITES = MAX
group by FOOD_TYPE
order by FOOD_TYPE DESC</code></pre>