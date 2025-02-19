<h3 id="문제-설명">문제 설명</h3>
<p>다음은 식품공장의 주문정보를 담은 <code>FOOD_ORDER</code> 테이블입니다. <code>FOOD_ORDER</code> 테이블은 다음과 같으며 <code>ORDER_ID</code>, <code>PRODUCT_ID</code>, <code>AMOUNT</code>, <code>PRODUCE_DATE</code>, <code>IN_DATE</code>,<code>OUT_DATE</code>,<code>FACTORY_ID</code>, <code>WAREHOUSE_ID</code>는 각각 주문 ID, 제품 ID, 주문양, 생산일자, 입고일자, 출고일자, 공장 ID, 창고 ID를 의미합니다.</p>
<h3 id="문제">문제</h3>
<p><code>FOOD_ORDER</code> 테이블에서 2022년 5월 1일을 기준으로 주문 ID, 제품 ID, 출고일자, 출고여부를 조회하는 SQL문을 작성해주세요. 출고여부는 2022년 5월 1일까지 출고완료로 이 후 날짜는 출고 대기로 미정이면 출고미정으로 출력해주시고, 결과는 주문 ID를 기준으로 오름차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>FOOD_ORDER</p>
<table>
<thead>
<tr>
<th>Column name</th>
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
<p>먼저, 문제에서 2022년 5월 1일을 기준으로 출고 여부를 판단해야 하므로 <code>CASE</code>문을 사용해야 합니다. <code>OUT_DATE</code>가 2022년 5월 1일 이후라면 &quot;출고대기&quot;, <code>OUT_DATE</code>가 NULL이면 &quot;출고미정&quot;, <code>OUT_DATE</code>가 2022년 5월 1일 이전이라면 &quot;출고완료&quot;로 분류해야 하므로, 각각의 조건을 별도로 설정했습니다. 이후, 데이터를 정렬하기 위해 <code>ORDER BY</code>를 사용했습니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT 
    ORDER_ID,
    PRODUCT_ID,
    DATE_FORMAT(OUT_DATE, &quot;%Y-%m-%d&quot;) as OUTDATE,
    CASE
        when OUT_DATE is NULL then '출고미정'
        when OUT_DATE &gt; '2022-05-01' then '출고대기'
        else '출고완료'
    end as '출고여부'
from FOOD_ORDER
order by ORDER_ID</code></pre>