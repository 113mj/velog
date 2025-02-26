<h3 id="문제-설명">문제 설명</h3>
<p>다음은 어느 한 서점에서 판매중인 도서들의 도서 정보(<code>BOOK</code>), 저자 정보(<code>AUTHOR</code>) 테이블입니다.</p>
<p><code>BOOK</code> 테이블은 각 도서의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.
<code>AUTHOR</code> 테이블은 도서의 저자의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.</p>
<h3 id="문제">문제</h3>
<p>'경제' 카테고리에 속하는 도서들의 도서 ID(<code>BOOK_ID</code>), 저자명(<code>AUTHOR_NAME</code>), 출판일(<code>PUBLISHED_DATE</code>) 리스트를 출력하는 SQL문을 작성해주세요.
결과는 출판일을 기준으로 오름차순 정렬해주세요.</p>
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
<td>AUTHOR</td>
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
<td>AUTHOR_ID</td>
<td>INTEGER</td>
<td>FALSE</td>
<td>저자 ID</td>
</tr>
<tr>
<td>AUTHOR_NAME</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
<td>저자명</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저 문제에서 필요한 데이터는 두 테이블에 있기 때문에 <code>JOIN</code>연산을 합니다. 그리고 '경제' 카테고리에 속하는 도서를 뽑기 위해 <code>WHERE</code>을 사용하여 정보들을 필터링합니다. 그 후 <code>DATE_FORMAT()</code>을 사용하여 날짜 데이터를 예시의 출력 결과와 일치하게 합니다. 마지막으로 출판일을 기준으로 정렬합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    b.BOOK_ID,
    a.AUTHOR_NAME,
    DATE_FORMAT(b.PUBLISHED_DATE, &quot;%Y-%m-%d&quot;) as PUBLISHED_DATE
from BOOK b
join AUTHOR a on b.AUTHOR_ID = a.AUTHOR_ID
where b.CATEGORY = &quot;경제&quot;
order by PUBLISHED_DATE</code></pre>