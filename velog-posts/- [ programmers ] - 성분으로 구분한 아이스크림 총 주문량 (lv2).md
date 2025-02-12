<h3 id="문제">문제</h3>
<p>상반기 동안 각 아이스크림 성분 타입과 성분 타입에 대한 아이스크림의 총주문량을 총주문량이 작은 순서대로 조회하는 SQL 문을 작성해주세요. 이때 총주문량을 나타내는 컬럼명은 TOTAL_ORDER로 지정해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>FIRST_HALF</p>
<table>
<thead>
<tr>
<th>NAME</th>
<th>TYPE</th>
<th>NULLABLE</th>
</tr>
</thead>
<tbody><tr>
<td>SHIPMENT_ID</td>
<td>INT(N)</td>
<td>FALSE</td>
</tr>
<tr>
<td>FLAVOR</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
<tr>
<td>TOTAL_ORDER</td>
<td>INT(N)</td>
<td>FALSE</td>
</tr>
</tbody></table>
<p>ICECREAM_INFO</p>
<table>
<thead>
<tr>
<th>NAME</th>
<th>TYPE</th>
<th>NULLABLE</th>
</tr>
</thead>
<tbody><tr>
<td>FLAVOR</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
<tr>
<td>INGREDIENT_TYPE</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>문제에서 저희가 봐야할 값이 두 테이블에 있기 때문에 조인을 해야한다고 생각했습니다. 그리고 문제에서 두 성분타입에 대한 총 주문량을 검색해야 하기 때문에 <code>group by</code> 로 묶은 뒤 <code>TOTAL_ORDER</code> 의 합을 구하면 되겠다고 생각했습니다. 마지막으로 합계를 올림차순으로 출력해야하기 때문에 <code>ORDER_BY</code> 를 사용했습니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    i.INGREDIENT_TYPE,
    SUM(f.TOTAL_ORDER) as TOTAL_ORDER
from FIRST_HALF f
join ICECREAM_INFO i on f.FLAVOR = i.FLAVOR
group by i.INGREDIENT_TYPE
order by TOTAL_ORDER;</code></pre>