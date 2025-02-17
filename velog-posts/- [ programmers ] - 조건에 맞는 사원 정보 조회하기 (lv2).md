<h3 id="문제-설명">문제 설명</h3>
<p><code>HR_DEPARTMENT</code> 테이블은 회사의 부서 정보를 담은 테이블입니다. <code>HR_DEPARTMENT</code> 테이블의 구조는 다음과 같으며 <code>DEPT_ID</code>, <code>DEPT_NAME_KR</code>, <code>DEPT_NAME_EN</code>, <code>LOCATION</code>은 각각 부서 ID, 국문 부서명, 영문 부서명, 부서 위치를 의미합니다.</p>
<p><code>HR_EMPLOYEES</code> 테이블은 회사의 사원 정보를 담은 테이블입니다. <code>HR_EMPLOYEES</code> 테이블의 구조는 다음과 같으며 <code>EMP_NO</code>, <code>EMP_NAME</code>, <code>DEPT_ID</code>, <code>POSITION</code>, <code>EMAIL</code>, <code>COMP_TEL</code>, <code>HIRE_DATE</code>, <code>SAL</code>은 각각 사번, 성명, 부서 ID, 직책, 이메일, 전화번호, 입사일, 연봉을 의미합니다.</p>
<p><code>HR_GRADE</code> 테이블은 2022년 사원의 평가 정보를 담은 테이블입니다. <code>HR_GRADE</code>의 구조는 다음과 같으며 <code>EMP_NO</code>, <code>YEAR</code>, <code>HALF_YEAR</code>, <code>SCORE</code>는 각각 사번, 연도, 반기, 평가 점수를 의미합니다.</p>
<h3 id="문제">문제</h3>
<p><code>HR_DEPARTMENT</code>, <code>HR_EMPLOYEES</code>, <code>HR_GRADE</code> 테이블에서 2022년도 한해 평가 점수가 가장 높은 사원 정보를 조회하려 합니다. 2022년도 평가 점수가 가장 높은 사원들의 점수, 사번, 성명, 직책, 이메일을 조회하는 SQL문을 작성해주세요.</p>
<p>2022년도의 평가 점수는 상,하반기 점수의 합을 의미하고, 평가 점수를 나타내는 컬럼의 이름은 SCORE로 해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>HR_DEPARTMENT</p>
<table>
<thead>
<tr>
<th>Column name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>DEPT_ID</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>DEPT_NAME_KR</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>DEPT_NAME_EN</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>LOCATION</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
</tbody></table>
<p>HR_EMPLOYEES</p>
<table>
<thead>
<tr>
<th>Column name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>EMP_NO</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>EMP_NAME</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>DEPT_ID</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>POSITION</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>EMAIL</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>COMP_TEL</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>HIRE_DATE</td>
<td>DATE</td>
<td>FALSE</td>
</tr>
<tr>
<td>SAL</td>
<td>NUMBER</td>
<td>FALSE</td>
</tr>
</tbody></table>
<p>HR_GRADE</p>
<table>
<thead>
<tr>
<th>Column name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>EMP_NO</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
<tr>
<td>YEAR</td>
<td>NUMBER</td>
<td>FALSE</td>
</tr>
<tr>
<td>HALF_YEAR</td>
<td>NUMBER</td>
<td>FALSE</td>
</tr>
<tr>
<td>SCORE</td>
<td>NUMBER</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>두 개의 테이블에서 정보를 조회해야 하므로 <code>JOIN</code>을 사용하여 데이터를 결합합니다. 이후, 상반기와 하반기 점수를 합산하여 <code>SCORE</code> 컬럼을 생성해야 하므로, <code>GROUP BY</code>를 사용하여 사번별로 데이터를 그룹화하고 <code>SUM()</code> 함수를 활용해 점수를 합산합니다. 그런 다음, <code>SCORE</code>를 기준으로 내림차순 정렬하고, <code>LIMIT</code>을 적용하여 가장 높은 점수를 가진 데이터를 조회합니다. 내림차순 정렬 시, 가장 상위에 위치한 데이터가 최고 점수를 갖기 때문입니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT 
    SUM(hg.SCORE) AS SCORE,
    e.EMP_NO,
    e.EMP_NAME,
    e.POSITION,
    e.EMAIL
from HR_EMPLOYEES e
join HR_GRADE hg ON e.EMP_NO = hg.EMP_NO
group by e.EMP_NO
order by SCORE DESC
LIMIT 1;
</code></pre>