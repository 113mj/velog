<h3 id="문제-설명">문제 설명</h3>
<p>다음은 어느 한 서점에서 판매중인 도서들의 도서 정보(<code>BOOK</code>), 판매 정보(<code>BOOK_SALES</code>) 테이블입니다.</p>
<p><code>BOOK</code> 테이블은 각 도서의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.
<code>BOOK_SALES</code> 테이블은 각 도서의 날짜 별 판매량 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.</p>
<h3 id="문제">문제</h3>
<p>2022년 1월의 카테고리 별 도서 판매량을 합산하고, 카테고리(<code>CATEGORY</code>), 총 판매량(<code>TOTAL_SALES</code>) 리스트를 출력하는 SQL문을 작성해주세요.
결과는 카테고리명을 기준으로 오름차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>BOOK</p>
<table>
<thead>
<tr>
<th>Column Name</th>
<th>Type</th>
<th>Nullable</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>BOOK_ID</td>
<td>INTEGER</td>
<td>FALSE</td>
<td>도서 ID</td>
</tr>
<tr>
<td>CATEGORY</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
<td>카테고리 (경제, 인문, 소설, 생활, 기술)</td>
</tr>
<tr>
<td>AUTHOR_ID</td>
<td>INTEGER</td>
<td>FALSE</td>
<td>저자 ID</td>
</tr>
<tr>
<td>PRICE</td>
<td>INTEGER</td>
<td>FALSE</td>
<td>판매가 (원)</td>
</tr>
<tr>
<td>PUBLISHED_DATE</td>
<td>DATE</td>
<td>FALSE</td>
<td>출판일</td>
</tr>
<tr>
<td>BOOK_SALES</td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody></table>
<table>
<thead>
<tr>
<th>Column Name</th>
<th>Type</th>
<th>Nullable</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>BOOK_ID</td>
<td>INTEGER</td>
<td>FALSE</td>
<td>도서 ID</td>
</tr>
<tr>
<td>SALES_DATE</td>
<td>DATE</td>
<td>FALSE</td>
<td>판매일</td>
</tr>
<tr>
<td>SALES</td>
<td>INTEGER</td>
<td>FALSE</td>
<td>판매량</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저 문제에서 조회해야할 정보들이 두 테이블에 있기 때문에 <code>JOIN</code>을 합니다. 2022년 1월 판매 정보를 조회하기 위해 <code>WHERE</code>과 <code>BETWEEN AND</code>를 사용하여 판매일에 대해 필터링을 합니다. 그 후 카테고리별로 판매량을 봐야하기 때문에 <code>GROUP BY</code>을 사용합니다. 필터링 및 그룹화된 정보들에 대해 판매량을 확인하기 위해여 집계함수 <code>SUM()</code>을 사용하여 카테고리별 책들의 판매량을 합니다. 마지막으로 카테고리별로 정렬하기 위해 <code>ORDER BY</code>를 사용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT 
    b.CATEGORY,
    sum(s.SALES) as &quot;TOTAL_SALES&quot;
from BOOK_SALES s
join BOOK b on s.BOOK_ID = b.BOOK_ID
where s.SALES_DATE between '2022-01-01' and '2022-01-31'
group by b.CATEGORY
order by b.CATEGORY</code></pre>