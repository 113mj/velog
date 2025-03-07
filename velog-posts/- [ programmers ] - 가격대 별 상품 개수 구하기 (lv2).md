<h3 id="문제-설명">문제 설명</h3>
<p>다음은 어느 의류 쇼핑몰에서 판매중인 상품들의 정보를 담은 <code>PRODUCT</code> 테이블입니다. <code>PRODUCT</code> 테이블은 아래와 같은 구조로 되어있으며, <code>PRODUCT_ID</code>, <code>PRODUCT_CODE</code>, <code>PRICE</code>는 각각 상품 ID, 상품코드, 판매가를 나타냅니다.</p>
<p>상품 별로 중복되지 않는 8자리 상품코드 값을 가지며 앞 2자리는 카테고리 코드를 나타냅니다.</p>
<h3 id="문제">문제</h3>
<p><code>PRODUCT</code> 테이블에서 만원 단위의 가격대 별로 상품 개수를 출력하는 SQL 문을 작성해주세요. 이때 컬럼명은 각각 컬럼명은 <code>PRICE_GROUP</code>, <code>PRODUCTS</code>로 지정해주시고 가격대 정보는 각 구간의 최소금액(10,000원 이상 ~ 20,000 미만인 구간인 경우 10,000)으로 표시해주세요. 결과는 가격대를 기준으로 오름차순 정렬해주세요.</p>
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
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저, 가격을 만 원 단위로 표현하기 위해 <code>PRICE</code>를 10,000으로 나누어야 합니다. 이를 위해 <code>DIV</code> 연산자를 사용하여 <code>PRICE</code> 값을 10,000으로 나눈 몫을 구합니다. 그다음, 이렇게 구한 <code>PRICE_GROUP</code> 값은 0, 1, 2처럼 몫으로 표현되므로, 실제 가격 범위를 반영하기 위해 10,000을 다시 곱하여 원래의 범위값(0, 10000, 20000 등)으로 변환합니다. 이후, <code>GROUP BY</code>를 사용하여 <code>PRICE_GROUP</code>을 기준으로 그룹화하고, <code>COUNT()</code> 함수를 활용하여 각 그룹별 행의 개수를 계산합니다. 마지막으로, 그룹별로 오름차순 정렬하기 위해 <code>ORDER BY</code>를 적용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    (PRICE div 10000) * 10000 as &quot;PRICE_GROUP&quot;,
    count(PRODUCT_ID) as &quot;PRODUCTS&quot;
from PRODUCT
group by PRICE_GROUP
order by PRICE_GROUP</code></pre>