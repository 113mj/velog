<h3 id="문제">문제</h3>
<p>DEVELOPERS 테이블에서 Python이나 C# 스킬을 가진 개발자의 정보를 조회하려 합니다. 조건에 맞는 개발자의 ID, 이메일, 이름, 성을 조회하는 SQL 문을 작성해 주세요.</p>
<p>결과는 ID를 기준으로 오름차순 정렬해 주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>SKILLCODES</p>
<table>
<thead>
<tr>
<th>NAME</th>
<th>TYPE</th>
<th>UNIQUE</th>
<th>NULLABLE</th>
</tr>
</thead>
<tbody><tr>
<td>NAME</td>
<td>VARCHAR(N)</td>
<td>Y</td>
<td>N</td>
</tr>
<tr>
<td>CATEGORY</td>
<td>VARCHAR(N)</td>
<td>N</td>
<td>N</td>
</tr>
<tr>
<td>CODE</td>
<td>INTEGER</td>
<td>Y</td>
<td>N</td>
</tr>
</tbody></table>
<p>DEVELOPERS</p>
<table>
<thead>
<tr>
<th>NAME</th>
<th>TYPE</th>
<th>UNIQUE</th>
<th>NULLABLE</th>
</tr>
</thead>
<tbody><tr>
<td>ID</td>
<td>VARCHAR(N)</td>
<td>Y</td>
<td>N</td>
</tr>
<tr>
<td>FIRST_NAME</td>
<td>VARCHAR(N)</td>
<td>N</td>
<td>Y</td>
</tr>
<tr>
<td>LAST_NAME</td>
<td>VARCHAR(N)</td>
<td>N</td>
<td>Y</td>
</tr>
<tr>
<td>EMAIL</td>
<td>VARCHAR(N)</td>
<td>Y</td>
<td>N</td>
</tr>
<tr>
<td>SKILL_CODE</td>
<td>INTEGER</td>
<td>N</td>
<td>N</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<table>
<thead>
<tr>
<th>NAME</th>
<th>CATEGORY</th>
<th>CODE</th>
</tr>
</thead>
<tbody><tr>
<td>C++</td>
<td>Back End</td>
<td>4</td>
</tr>
<tr>
<td>JavaScript</td>
<td>Front End</td>
<td>16</td>
</tr>
<tr>
<td>Java</td>
<td>Back End</td>
<td>128</td>
</tr>
<tr>
<td>Python</td>
<td>Back End</td>
<td>256</td>
</tr>
<tr>
<td>C#</td>
<td>Back End</td>
<td>1024</td>
</tr>
<tr>
<td>React</td>
<td>Front End</td>
<td>2048</td>
</tr>
<tr>
<td>Vue</td>
<td>Front End</td>
<td>8192</td>
</tr>
<tr>
<td>Node.js</td>
<td>Back End</td>
<td>16384</td>
</tr>
</tbody></table>
<p>위는 SKILLCODES의 예시 테이블입니다. 이를 보여준 이유는 DEVELOPERS의 <code>SKILL_CODE</code> 컬럼의 특징을 알려주기 위해서입니다. 특이한 점은 <code>CODE</code>를 2진수로 표현했을 때 각 bit로 구분될 수 있도록 2의 제곱수로 구성되어 있습니다.
그리고 문제에서 <code>SKILL_CODE</code>는 다음과 같이 설명되어 있습니다.</p>
<blockquote>
<p>SKILL_CODE 컬럼은 INTEGER 타입이고, 2진수로 표현했을 때 각 bit는 SKILLCODES 테이블의 코드를 의미합니다.</p>
</blockquote>
<p>이는 <code>SKILL_CODE</code>가 여러 기술을 동시에 표현할 수 있도록 비트마스크(bitmask) 형태로 저장된다는 것을 의미합니다. 따라서 저희는 조인을 할 때 <code>SKILL_CODE</code>와 <code>CODE</code>를 비트연산자 <code>&amp;</code>를 통해 해당 스킬이 있는지 확인 할 수 있습니다. 
조인한 뒤 데이터들 중 'C#' 과 'Python' 가 있는 데이터를 필터링하기 위해 <code>where</code>를 사용합니다. 필터링 된 정보들 중 중복이 있을 수 있기 때문에 <code>DISTINCT</code> 를 <code>ID</code>에 사용하여 중복을 제거한 뒤 <code>ORDER BY</code>를 사용해 <code>ID</code>를 기준으로 오름차순으로 출력되게 했습니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT 
    distinct(d.ID),
    d.EMAIL,
    d.FIRST_NAME,
    d.LAST_NAME
from DEVELOPERS d
join SKILLCODES s on d.SKILL_CODE &amp; s.CODE
where s.NAME in ('C#', 'Python')
order by ID;</code></pre>