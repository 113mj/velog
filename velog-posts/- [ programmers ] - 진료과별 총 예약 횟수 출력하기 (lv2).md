<h3 id="문제-설명">문제 설명</h3>
<p>다음은 종합병원의 진료 예약정보를 담은 <code>APPOINTMENT</code> 테이블 입니다.
<code>APPOINTMENT</code> 테이블은 다음과 같으며 <code>APNT_YMD</code>, <code>APNT_NO</code>, <code>PT_NO</code>, <code>MCDP_CD</code>, <code>MDDR_ID</code>, <code>APNT_CNCL_YN</code>, <code>APNT_CNCL_YMD</code>는 각각 <code>진료예약일시</code>, <code>진료예약번호</code>, <code>환자번호</code>, <code>진료과코드</code>, <code>의사ID</code>, <code>예약취소여부</code>, <code>예약취소날짜</code>를 나타냅니다.</p>
<h3 id="문제">문제</h3>
<p><code>APPOINTMENT</code> 테이블에서 2022년 5월에 예약한 환자 수를 진료과코드 별로 조회하는 SQL문을 작성해주세요. 이때, 컬럼명은 '진료과 코드', '5월예약건수'로 지정해주시고 결과는 진료과별 예약한 환자 수를 기준으로 오름차순 정렬하고, 예약한 환자 수가 같다면 진료과 코드를 기준으로 오름차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>APPOINTMENT</p>
<table>
<thead>
<tr>
<th>Column name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>APNT_YMD</td>
<td>TIMESTAMP</td>
<td>FALSE</td>
</tr>
<tr>
<td>APNT_NO</td>
<td>NUMBER(5)</td>
<td>FALSE</td>
</tr>
<tr>
<td>PT_NO</td>
<td>VARCHAR(10)</td>
<td>FALSE</td>
</tr>
<tr>
<td>MCDP_CD</td>
<td>VARCHAR(6)</td>
<td>FALSE</td>
</tr>
<tr>
<td>MDDR_ID</td>
<td>VARCHAR(10)</td>
<td>FALSE</td>
</tr>
<tr>
<td>APNT_CNCL_YN</td>
<td>VARCHAR(1)</td>
<td>TRUE</td>
</tr>
<tr>
<td>APNT_CNCL_YMD</td>
<td>DATE</td>
<td>TRUE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>일단 먼저 진료과코드별로 조회하기 위해 <code>GROUP BY</code>를 사용했습니다. 그 다음 예약한 날짜가 2022년 5월인 정보만을 필터링 하기 위해 <code>WHERE</code>에 날짜 함수 <code>YEAR()</code>와 <code>MONTH()</code>를 사용했습니다. 마지막으로 5월예약건수와 진료과코드를 기준으로 <code>ORDER BY</code>를 사용하여 데이터들을 정렬했습니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    MCDP_CD AS &quot;진료과코드&quot;,
    count(PT_NO) AS &quot;5월예약건수&quot;
from APPOINTMENT
where YEAR(APNT_YMD) = 2022
and MONTH(APNT_YMD) = 5
group by MCDP_CD
ORDER BY 5월예약건수, 진료과코드;</code></pre>