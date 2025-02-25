<h3 id="문제-설명">문제 설명</h3>
<p>다음은 어느 의류 쇼핑몰에서 판매중인 상품들의 상품 정보를 담은 <code>PRODUCT</code> 테이블과 오프라인 상품 판매 정보를 담은 <code>OFFLINE_SALE</code> 테이블 입니다. <code>PRODUCT</code> 테이블은 아래와 같은 구조로 <code>PRODUCT_ID</code>, <code>PRODUCT_CODE</code>, <code>PRICE</code>는 각각 상품 ID, 상품코드, 판매가를 나타냅니다.</p>
<p>상품 별로 중복되지 않는 8자리 상품코드 값을 가지며, 앞 2자리는 카테고리 코드를 의미합니다.</p>
<p><code>OFFLINE_SALE</code> 테이블은 아래와 같은 구조로 되어있으며 <code>OFFLINE_SALE_ID</code>, <code>PRODUCT_ID</code>, <code>SALES_AMOUNT</code>, <code>SALES_DATE</code>는 각각 오프라인 상품 판매 ID, 상품 ID, 판매량, 판매일을 나타냅니다.</p>
<p>동일한 날짜, 상품 ID 조합에 대해서는 하나의 판매 데이터만 존재합니다.</p>
<h3 id="문제">문제</h3>
<p><code>PRODUCT</code> 테이블과 <code>OFFLINE_SALE</code> 테이블에서 상품코드 별 매출액(판매가 * 판매량) 합계를 출력하는 SQL문을 작성해주세요. 결과는 매출액을 기준으로 내림차순 정렬해주시고 매출액이 같다면 상품코드를 기준으로 오름차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>PRODUCT</p>
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
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>PRODUCT_CODE</td>
<td>VARCHAR(8)</td>
<td>FALSE</td>
</tr>
<tr>
<td>PRICE</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
</tbody></table>
<p>OFFLINE_SALE</p>
<table>
<thead>
<tr>
<th>Column Name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>OFFLINE_SALE_ID</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>PRODUCT_ID</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>SALES_AMOUNT</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>SALES_DATE</td>
<td>DATE</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>저희가 해야할 과정은 다음과 같습니다.</p>
<ol>
<li><code>OFFLINE_SALE</code>에서 판매량 추출</li>
<li>매출액 추출</li>
<li>데이터 정렬</li>
</ol>
<p>먼저, <code>PRODUCT</code> 테이블에는 <code>PRODUCT_ID</code>에 대한 <code>PRICE</code> 속성이 있으므로, <code>OFFLINE_SALE</code> 테이블에서 <code>PRODUCT_ID</code>별 판매량을 조회해야 합니다. 이를 위해 <code>GROUP BY</code>와 <code>SUM()</code>을 사용하여 총 판매량을 집계합니다.</p>
<p>다음으로, 판매량과 가격이 서로 다른 테이블에 존재하므로, 매출액을 계산하기 위해 두 테이블을 <code>JOIN</code>합니다. 매출액은 (판매가 * 판매량)으로 정의되므로, 두 컬럼을 곱한 값을 출력합니다.</p>
<p>마지막으로, 매출액을 기준으로 내림차순 정렬하고, 동일한 매출액일 경우 <code>PRODUCT_CODE</code>를 기준으로 오름차순 정렬합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">with temp1 as (
    SELECT
        PRODUCT_ID,
        sum(SALES_AMOUNT) as &quot;count&quot;
    From OFFLINE_SALE
    group by PRODUCT_ID
)
select 
    p.PRODUCT_CODE,
    t.count * p.price as &quot;SALES&quot;
from PRODUCT p
join temp1 t on p.PRODUCT_ID = t.PRODUCT_ID
order by SALES DESC, p.PRODUCT_CODE</code></pre>