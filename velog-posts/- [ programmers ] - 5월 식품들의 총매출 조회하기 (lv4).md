<h3 id="문제-설명">문제 설명</h3>
<p>다음은 식품의 정보를 담은 <code>FOOD_PRODUCT</code> 테이블과 식품의 주문 정보를 담은 <code>FOOD_ORDER</code> 테이블입니다. <code>FOOD_PRODUCT</code> 테이블은 다음과 같으며 <code>PRODUCT_ID</code>, <code>PRODUCT_NAME</code>, <code>PRODUCT_CD</code>, <code>CATEGORY</code>, <code>PRICE</code>는 식품 ID, 식품 이름, 식품코드, 식품분류, 식품 가격을 의미합니다.</p>
<p><code>FOOD_ORDER</code> 테이블은 다음과 같으며 <code>ORDER_ID</code>, <code>PRODUCT_ID</code>, <code>AMOUNT</code>, <code>PRODUCE_DATE</code>, <code>IN_DATE</code>, <code>OUT_DATE</code>, <code>FACTORY_ID</code>, <code>WAREHOUSE_ID</code>는 각각 주문 ID, 제품 ID, 주문량, 생산일자, 입고일자, 출고일자, 공장 ID, 창고 ID를 의미합니다.</p>
<h3 id="문제">문제</h3>
<p><code>FOOD_PRODUCT</code>와 <code>FOOD_ORDER</code> 테이블에서 생산일자가 2022년 5월인 식품들의 식품 ID, 식품 이름, 총매출을 조회하는 SQL문을 작성해주세요. 이때 결과는 총매출을 기준으로 내림차순 정렬해주시고 총매출이 같다면 식품 ID를 기준으로 오름차순 정렬해주세요.</p>
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
<p>FOOD_ORDER</p>
<table>
<thead>
<tr>
<th>Column Name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>ORDER_ID</td>
<td>VARCHAR(10)</td>
<td>FALSE</td>
</tr>
<tr>
<td>PRODUCT_ID</td>
<td>VARCHAR(5)</td>
<td>FALSE</td>
</tr>
<tr>
<td>AMOUNT</td>
<td>NUMBER</td>
<td>FALSE</td>
</tr>
<tr>
<td>PRODUCE_DATE</td>
<td>DATE</td>
<td>TRUE</td>
</tr>
<tr>
<td>IN_DATE</td>
<td>DATE</td>
<td>TRUE</td>
</tr>
<tr>
<td>OUT_DATE</td>
<td>DATE</td>
<td>TRUE</td>
</tr>
<tr>
<td>FACTORY_ID</td>
<td>VARCHAR(10)</td>
<td>FALSE</td>
</tr>
<tr>
<td>WAREHOUSE_ID</td>
<td>VARCHAR(10)</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저 조건에 맞는 데이터를 찾기 위해선 두 테이블을 같이 봐야하기 때문에 <code>JOIN</code>연산을 합니다. 그 다음 2022년 5월에 생산한 제품을 찾기 위해 <code>MONTH</code> 와 <code>YEAR</code>함수를 사용합니다. 그리고 제품별 총 매출을 구하기 위하여 <code>GROUP BY</code>를 사용합니다. 그 다음<code>PRICE</code>와 <code>AMOUNT</code>를 곱한 값이 매출이며 각 매출을 다 합쳐야 총매출이 구해지기 때문에 집계함수 <code>SUM</code>을 사용합니다. 마지막으로 데이터 정렬을 위해 <code>ORDER BY</code>를 사용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    p.PRODUCT_ID,
    p.PRODUCT_NAME,
    sum(p.PRICE * o.AMOUNT) as TOTAL_SALES
From FOOD_PRODUCT p
join FOOD_ORDER o on p.PRODUCT_ID = o.PRODUCT_ID
where MONTH(o.PRODUCE_DATE) = 5 and YEAR(o.PRODUCE_DATE) = 2022
group by o.PRODUCT_ID
order by TOTAL_SALES DESC, p.PRODUCT_ID ASC</code></pre>