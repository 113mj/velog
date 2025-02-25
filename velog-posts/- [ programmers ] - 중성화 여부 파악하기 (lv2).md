<h3 id="문제-설명">문제 설명</h3>
<p><code>ANIMAL_INS</code> 테이블은 동물 보호소에 들어온 동물의 정보를 담은 테이블입니다. <code>ANIMAL_INS</code> 테이블 구조는 다음과 같으며, <code>ANIMAL_ID</code>, <code>ANIMAL_TYPE</code>, <code>DATETIME</code>, <code>INTAKE_CONDITION</code>, <code>NAME</code>, <code>SEX_UPON_INTAKE</code>는 각각 동물의 아이디, 생물 종, 보호 시작일, 보호 시작 시 상태, 이름, 성별 및 중성화 여부를 나타냅니다.</p>
<h3 id="문제">문제</h3>
<p>보호소의 동물이 중성화되었는지 아닌지 파악하려 합니다. 중성화된 동물은 <code>SEX_UPON_INTAKE</code> 컬럼에 'Neutered' 또는 'Spayed'라는 단어가 들어있습니다. 동물의 아이디와 이름, 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성해주세요. 이때 중성화가 되어있다면 'O', 아니라면 'X'라고 표시해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>ANIMAL_INS</p>
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
<p><code>SEX_UPON_INTAKE</code> 컬럼의 문자열을 조건으로 설정했기 때문에 <code>IF()</code> 함수를 사용합니다. 이후, 해당 문자열에 'Neutered' 또는 'Spayed'가 포함되어 있는지 판별하기 위해 <code>LIKE</code>를 활용합니다. 두 단어 중 하나라도 포함되어 있다면 'O'를, 그렇지 않다면 'X'를 반환하는 &quot;중성화&quot;라는 새로운 컬럼을 생성합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    ANIMAL_ID,
    NAME,
    IF(SEX_UPON_INTAKE LIKE &quot;%Neutered%&quot; OR SEX_UPON_INTAKE LIKE &quot;%Spayed%&quot;, &quot;O&quot;, &quot;X&quot;) AS &quot;중성화&quot;
from ANIMAL_INS</code></pre>