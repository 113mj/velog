<h3 id="문제-설명">문제 설명</h3>
<p>다음은 식품의 정보를 담은 <code>FOOD_PRODUCT</code> 테이블입니다. <code>FOOD_PRODUCT</code> 테이블은 다음과 같으며 <code>PRODUCT_ID</code>, <code>PRODUCT_NAME</code>, <code>PRODUCT_CD</code>, <code>CATEGORY</code>, <code>PRICE</code>는 식품 ID, 식품 이름, 식품코드, 식품분류, 식품 가격을 의미합니다.</p>
<h3 id="문제">문제</h3>
<p><code>FOOD_PRODUCT</code> 테이블에서 식품분류별로 가격이 제일 비싼 식품의 분류, 가격, 이름을 조회하는 SQL문을 작성해주세요. 이때 식품분류가 '과자', '국', '김치', '식용유'인 경우만 출력시켜 주시고 결과는 식품 가격을 기준으로 내림차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>FOOD_PRODUCT</p>
<table>
<thead>
<tr>
<th>Column Name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>PRODUCT_ID</td>
<td>VARCHAR(10)</td>
<td>FALSE</td>
</tr>
<tr>
<td>PRODUCT_NAME</td>
<td>VARCHAR(50)</td>
<td>FALSE</td>
</tr>
<tr>
<td>PRODUCT_CD</td>
<td>VARCHAR(10)</td>
<td>TRUE</td>
</tr>
<tr>
<td>CATEGORY</td>
<td>VARCHAR(10)</td>
<td>TRUE</td>
</tr>
<tr>
<td>PRICE</td>
<td>NUMBER</td>
<td>TRUE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저 식품분류별 가장 비싼 식품의 가격을 알기 위해 집계함수 <code>MAX()</code>와 <code>OVER()</code>를 사용합니다. 왜냐하면 <code>MAX()</code>만을 사용해선 가장 높은 가격이 얼마인지 알 수 있지만 어떤 제품이 가장 비싼지 알 수 없기 때문입니다. 그래서 <code>OVER(PARTITION BY)</code>를 사용하여 식품분류별 가장 비싼 가격을 임시 테이블 <code>temp1</code>에 추가하였습니다.</p>
<p>그 다음 임시 테이블 <code>temp1</code>에서 특정 조건에 대해 필터링을 합니다. 문제에서는 식품분류 중 특정한 품목에 대해서 검색을 해야하기 때문에 <code>WHERE</code>에 특정 품목 및 식품분류별 가장 비싼 가격을 갖고잇는 품목을 찾는 조건을 추가합니다.</p>
<p>마지막으로 내림차순 정렬을 위해 <code>ORDER BY</code>를 사용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">with temp1 as (
    SELECT
    *,
    max(PRICE) OVER(PARTITION BY CATEGORY) as MAX_PRICE
from FOOD_PRODUCT
)
SELECT
    CATEGORY,
    MAX_PRICE,
    PRODUCT_NAME
from temp1
where MAX_PRICE = PRICE and CATEGORY in ('과자', '국', '김치', '식용유')
order by MAX_PRICE DESC</code></pre>