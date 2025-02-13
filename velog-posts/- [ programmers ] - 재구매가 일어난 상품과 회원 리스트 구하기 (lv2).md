<h3 id="문제-설명">문제 설명</h3>
<p>다음은 어느 의류 쇼핑몰의 온라인 상품 판매 정보를 담은 ONLINE_SALE 테이블 입니다. <code>ONLINE_SALE</code>테이블은 아래와 같은 구조로 되어있으며 <code>ONLINE_SALE_ID</code>, <code>USER_ID</code>, <code>PRODUCT_ID</code>, <code>SALES_AMOUNT</code>, <code>SALES_DATE</code>는 각각 온라인 상품 판매 ID, 회원 ID, 상품 ID, 판매량, 판매일을 나타냅니다.동일한 날짜, 회원 ID, 상품 ID 조합에 대해서는 하나의 판매 데이터만 존재합니다.</p>
<h3 id="문제">문제</h3>
<p><code>ONLINE_SALE</code>테이블에서 동일한 회원이 동일한 상품을 재구매한 데이터를 구하여, 재구매한 회원 ID와 재구매한 상품 ID를 출력하는 SQL문을 작성해주세요. 결과는 회원 ID를 기준으로 오름차순 정렬해주시고 회원 ID가 같다면 상품 ID를 기준으로 내림차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>ONLINE_SALE</p>
<table>
<thead>
<tr>
<th>ONLINE_SALE_ID</th>
<th>USER_ID</th>
<th>PRODUCT_ID</th>
<th>SALES_AMOUNT</th>
<th>SALES_DATE</th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>1</td>
<td>3</td>
<td>2</td>
<td>2022-02-25</td>
</tr>
<tr>
<td>2</td>
<td>1</td>
<td>4</td>
<td>1</td>
<td>2022-03-01</td>
</tr>
<tr>
<td>4</td>
<td>2</td>
<td>4</td>
<td>2</td>
<td>2022-03-12</td>
</tr>
<tr>
<td>3</td>
<td>1</td>
<td>3</td>
<td>3</td>
<td>2022-03-31</td>
</tr>
<tr>
<td>5</td>
<td>3</td>
<td>5</td>
<td>1</td>
<td>2022-04-03</td>
</tr>
<tr>
<td>6</td>
<td>2</td>
<td>4</td>
<td>1</td>
<td>2022-04-06</td>
</tr>
<tr>
<td>2</td>
<td>1</td>
<td>4</td>
<td>2</td>
<td>2022-05-11</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>일단 문제에서 재구매한 회원 ID를 찾아야 합니다. 문제 설명에서 회원 ID, 날짜, 상품 ID 조합에 대해 하나의 판매 데이터만 존재하기 때문에 이를 이용하여 데이터를 <code>GROUP BY</code>를 데이터를 그룹화하면 되겠다고 생각했습니다. 그리고 회원들 중 재구매한 정보를 필터링하는 방법은 그룹화 한 뒤 데이터의 개수를 비교하면 된다고 생각했습니다. 아니면 쿼리를 하나 더 만들어서 새로운 컬럼을 만들어서 구현도 할 수 있다고 생각했습니다. 그 후 데이터들을 정렬하기 위해 <code>order by</code>를 사용했습니다.</p>
<h3 id="정답">정답</h3>
<p>풀이 1</p>
<pre><code class="language-sql">with temp as (
    select
    USER_ID,
    PRODUCT_ID,
    count(*) OVER(PARTITION BY USER_ID, PRODUCT_ID) as count_sales 
from ONLINE_SALE
)
select
    USER_ID,
    PRODUCT_ID
from temp
where count_sales &gt;= 2
group by USER_ID, PRODUCT_ID
order by USER_ID, PRODUCT_ID DESC;</code></pre>
<p>풀이 2</p>
<pre><code class="language-sql">select 
    USER_ID, 
    PRODUCT_ID
from ONLINE_SALE
group by USER_ID, PRODUCT_ID
having count(*) &gt; 1
order by USER_ID ASC, PRODUCT_ID DESC;</code></pre>