<h3 id="문제-설명">문제 설명</h3>
<p>다음은 어느 의류 쇼핑몰에서 판매중인 상품들의 정보를 담은 <code>PRODUCT</code> 테이블입니다. <code>PRODUCT</code> 테이블은 아래와 같은 구조로 되어있으며, <code>PRODUCT_ID</code>, <code>PRODUCT_CODE</code>, <code>PRICE</code>는 각각 상품 ID, 상품코드, 판매가를 나타냅니다.
상품 별로 중복되지 않는 8자리 상품코드 값을 가지며, 앞 2자리는 카테고리 코드를 의미합니다.</p>
<h3 id="문제">문제</h3>
<p>PRODUCT 테이블에서 상품 카테고리 코드(PRODUCT_CODE 앞 2자리) 별 상품 개수를 출력하는 SQL문을 작성해주세요. 결과는 상품 카테고리 코드를 기준으로 오름차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>PRODUCT</p>
<table>
<thead>
<tr>
<th>Column name</th>
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
<p>먼저 카테고리별로 묶기 위해서 <code>PRODUCT_CODE</code>의 앞 두 자리를 기준으로 그룹화를 합니다. 이를 위해 문자열 함수 <code>SUBSTRING</code>을 사용하여 앞 두 글자를 뽑아 정렬 및 그룹화를 합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT SUBSTRING(PRODUCT_CODE, 1, 2) AS CATEGORY,
       COUNT(*) AS PRODUCTS
from PRODUCT
group by CATEGORY
order by CATEGORY</code></pre>