<h3 id="문제-설명">문제 설명</h3>
<p>다음은 식당 리뷰 사이트의 회원 정보를 담은 <code>MEMBER_PROFILE</code> 테이블입니다. <code>MEMBER_PROFILE</code> 테이블은 다음과 같으며 <code>MEMBER_ID</code>, <code>MEMBER_NAME</code>, <code>TLNO</code>, <code>GENDER</code>, <code>DATE_OF_BIRTH</code>는 회원 ID, 회원 이름, 회원 연락처, 성별, 생년월일을 의미합니다.</p>
<h3 id="문제">문제</h3>
<p><code>MEMBER_PROFILE</code> 테이블에서 생일이 3월인 여성 회원의 ID, 이름, 성별, 생년월일을 조회하는 SQL문을 작성해주세요. 이때 전화번호가 NULL인 경우는 출력대상에서 제외시켜 주시고, 결과는 회원ID를 기준으로 오름차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>MEMBER_PROFILE</p>
<table>
<thead>
<tr>
<th>Column name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>MEMBER_ID</td>
<td>VARCHAR(100)</td>
<td>FALSE</td>
</tr>
<tr>
<td>MEMBER_NAME</td>
<td>VARCHAR(50)</td>
<td>FALSE</td>
</tr>
<tr>
<td>TLNO</td>
<td>VARCHAR(50)</td>
<td>TRUE</td>
</tr>
<tr>
<td>GENDER</td>
<td>VARCHAR(1)</td>
<td>TRUE</td>
</tr>
<tr>
<td>DATE_OF_BIRTH</td>
<td>DATE</td>
<td>TRUE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>문제의 조건에 해당하는 데이터를 조회하기 위해 필터링을 해야합니다. 먼저 전화번호가 없는 사람은 대상에서 제외해야 함으로 <code>is not NULL</code>로 필터링을 합니다. 그 다음 3월에 태어난 사람을 조회하기 위해서 날짜 함수 <code>MONTH</code>를 사용하여 <code>DATE</code>타입에서 3월에 태어난 사람을 조회합니다. 그 후 여자인 사람을 뽑는 조건을 작성합니다. 마지막으로 <code>ORDER BY</code>를 사용하여 <code>MEMBER_ID</code>를 기준으로 오름차순 정렬을 합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    MEMBER_ID,
    MEMBER_NAME,
    GENDER,
    DATE_FORMAT(DATE_OF_BIRTH, '%Y-%m-%d') AS DATE_OF_BIRTH
from MEMBER_PROFILE
where TLNO is not NULL
and MONTH(DATE_OF_BIRTH) = 3
and GENDER = 'W'
order by MEMBER_ID;</code></pre>