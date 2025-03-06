<h3 id="문제-설명">문제 설명</h3>
<p>다음은 중고 거래 게시판 정보를 담은 <code>USED_GOODS_BOARD</code> 테이블과 중고 거래 게시판 사용자 정보를 담은 <code>USED_GOODS_USER</code> 테이블입니다. <code>USED_GOODS_BOARD</code> 테이블은 다음과 같으며 <code>BOARD_ID</code>, <code>WRITER_ID</code>, <code>TITLE</code>, <code>CONTENTS</code>, <code>PRICE</code>, <code>CREATED_DATE</code>, <code>STATUS</code>, <code>VIEWS</code>는 게시글 ID, 작성자 ID, 게시글 제목, 게시글 내용, 가격, 작성일, 거래상태, 조회수를 의미합니다.</p>
<p><code>USED_GOODS_USER</code> 테이블은 다음과 같으며 <code>USER_ID</code>, <code>NICKNAME</code>, <code>CITY</code>, <code>STREET_ADDRESS1</code>, <code>STREET_ADDRESS2</code>, <code>TLNO</code>는 각각 회원 ID, 닉네임, 시, 도로명 주소, 상세 주소, 전화번호를 를 의미합니다.</p>
<h3 id="문제">문제</h3>
<p><code>USED_GOODS_BOARD</code>와 <code>USED_GOODS_USER</code> 테이블에서 완료된 중고 거래의 총금액이 70만 원 이상인 사람의 회원 ID, 닉네임, 총거래금액을 조회하는 SQL문을 작성해주세요. 결과는 총거래금액을 기준으로 오름차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>USED_GOODS_BOARD</p>
<table>
<thead>
<tr>
<th>Column Name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>BOARD_ID</td>
<td>VARCHAR(5)</td>
<td>FALSE</td>
</tr>
<tr>
<td>WRITER_ID</td>
<td>VARCHAR(50)</td>
<td>FALSE</td>
</tr>
<tr>
<td>TITLE</td>
<td>VARCHAR(100)</td>
<td>FALSE</td>
</tr>
<tr>
<td>CONTENTS</td>
<td>VARCHAR(1000)</td>
<td>FALSE</td>
</tr>
<tr>
<td>PRICE</td>
<td>NUMBER</td>
<td>FALSE</td>
</tr>
<tr>
<td>CREATED_DATE</td>
<td>DATE</td>
<td>FALSE</td>
</tr>
<tr>
<td>STATUS</td>
<td>VARCHAR(10)</td>
<td>FALSE</td>
</tr>
<tr>
<td>VIEWS</td>
<td>NUMBER</td>
<td>FALSE</td>
</tr>
</tbody></table>
<p>USED_GOODS_USER</p>
<table>
<thead>
<tr>
<th>Column Name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>USER_ID</td>
<td>VARCHAR(50)</td>
<td>FALSE</td>
</tr>
<tr>
<td>NICKNAME</td>
<td>VARCHAR(100)</td>
<td>FALSE</td>
</tr>
<tr>
<td>CITY</td>
<td>VARCHAR(100)</td>
<td>FALSE</td>
</tr>
<tr>
<td>STREET_ADDRESS1</td>
<td>VARCHAR(100)</td>
<td>FALSE</td>
</tr>
<tr>
<td>STREET_ADDRESS2</td>
<td>VARCHAR(100)</td>
<td>TRUE</td>
</tr>
<tr>
<td>TLNO</td>
<td>VARCHAR(20)</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저, 거래 완료된 게시글만 조회하기 위해 <code>USED_GOODS_BOARD</code> 테이블에서 <code>WHERE</code>을 사용하여 필터링합니다.그 다음, 거래한 사용자의 회원 ID(WRITER_ID)를 기준으로 <code>USED_GOODS_USER</code>과 <code>JOIN</code>하여 닉네임 정보를 가져옵니다. 같은 회원이 여러 건의 거래를 완료했을 수 있으므로 <code>GROUP BY</code>를 사용하여 ID별로 그룹화하고, <code>SUM()</code>를 활용해 각 사용자의 총 거래 금액을 계산합니다. 이후, <code>HAVING</code>을 사용하여 총거래금액이 70만 원 이상인 회원만 조회합니다. 마지막으로, 결과를 총거래금액 기준으로 오름차순 정렬하기 위해 <code>ORDER BY</code>를 적용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">with temp1 as (
    SELECT
    WRITER_ID,
    PRICE
from USED_GOODS_BOARD b
where STATUS = &quot;DONE&quot;
)
select
    t.WRITER_ID,
    u.NICKNAME,
    sum(t.PRICE) as TOTAL_SALES
from temp1 t 
join USED_GOODS_USER u on t.WRITER_ID = u.USER_ID
group by t.WRITER_ID
having sum(t.PRICE) &gt;= 700000
order by TOTAL_SALES</code></pre>