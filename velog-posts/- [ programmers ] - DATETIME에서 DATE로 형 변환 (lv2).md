<h3 id="문제-설명">문제 설명</h3>
<p><code>ANIMAL_INS</code> 테이블은 동물 보호소에 들어온 동물의 정보를 담은 테이블입니다. <code>ANIMAL_INS</code> 테이블 구조는 다음과 같으며, <code>ANIMAL_ID</code>, <code>ANIMAL_TYPE</code>, <code>DATETIME</code>, <code>INTAKE_CONDITION</code>, <code>NAME</code>, <code>SEX_UPON_INTAKE</code>는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.</p>
<h3 id="문제">문제</h3>
<p><code>ANIMAL_INS</code> 테이블에 등록된 모든 레코드에 대해, 각 동물의 아이디와 이름, 들어온 날짜를 조회하는 SQL문을 작성해주세요. 이때 결과는 아이디 순으로 조회해야 합니다.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<table>
<thead>
<tr>
<th>NAME</th>
<th>TYPE</th>
<th>NULLABLE</th>
</tr>
</thead>
<tbody><tr>
<td>ANIMAL_ID</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
<tr>
<td>ANIMAL_TYPE</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
<tr>
<td>DATETIME</td>
<td>DATETIME</td>
<td>FALSE</td>
</tr>
<tr>
<td>INTAKE_CONDITION</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
<tr>
<td>NAME</td>
<td>VARCHAR(N)</td>
<td>TRUE</td>
</tr>
<tr>
<td>SEX_UPON_INTAKE</td>
<td>VARCHAR(N)</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>문제 요구사항에 맞춰 날짜를 시각 정보 없이 &quot;년-월-일&quot; 형식으로 출력하기 위해 <code>DATE_FORMAT()</code> 함수를 사용했습니다. 또한, 결과를 체계적으로 정리하기 위해 <code>ANIMAL_ID</code> 기준으로 정렬하는 ORDER BY를 적용했습니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    ANIMAL_ID,
    NAME,
    DATE_FORMAT(DATETIME, &quot;%Y-%m-%d&quot;) as &quot;날짜&quot;
from ANIMAL_INS
order by ANIMAL_ID</code></pre>