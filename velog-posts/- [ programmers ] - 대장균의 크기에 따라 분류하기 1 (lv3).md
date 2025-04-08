<h3 id="문제-설명">문제 설명</h3>
<p>대장균들은 일정 주기로 분화하며, 분화를 시작한 개체를 부모 개체, 분화가 되어 나온 개체를 자식 개체라고 합니다.
다음은 실험실에서 배양한 대장균들의 정보를 담은 <code>ECOLI_DATA</code> 테이블입니다. <code>ECOLI_DATA</code> 테이블의 구조는 다음과 같으며, <code>ID</code>, <code>PARENT_ID</code>, <code>SIZE_OF_COLONY</code>, <code>DIFFERENTIATION_DATE</code>, <code>GENOTYPE</code> 은 각각 대장균 개체의 ID, 부모 개체의 ID, 개체의 크기, 분화되어 나온 날짜, 개체의 형질을 나타냅니다.
최초의 대장균 개체의 <code>PARENT_ID</code> 는 NULL 값입니다.</p>
<h3 id="문제">문제</h3>
<p>대장균 개체의 크기가 100 이하라면 'LOW', 100 초과 1000 이하라면 'MEDIUM', 1000 초과라면 'HIGH' 라고 분류합니다. 대장균 개체의 ID(ID) 와 분류(SIZE)를 출력하는 SQL 문을 작성해주세요.이때 결과는 개체의 ID 에 대해 오름차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<table>
<thead>
<tr>
<th>Column Name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>ID</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>PARENT_ID</td>
<td>INTEGER</td>
<td>TRUE</td>
</tr>
<tr>
<td>SIZE_OF_COLONY</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>DIFFERENTIATION_DATE</td>
<td>DATE</td>
<td>FALSE</td>
</tr>
<tr>
<td>GENOTYPE</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>먼저 개체의 크기에 따라 분류해야 하기 때문에 <code>CASE</code>문을 통해 크기에 따라 분류를 합니다. 먼저 100이하인 조건을 보기 때문에 100이하라면 LOW를 배정합니다. 그 다음 100초과 1000이하는 MEDIUM, 1000초과면 HIGH로 분류를 합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">select 
    ID,
    case
        when SIZE_OF_COLONY &lt;= 100 then &quot;LOW&quot;
        when SIZE_OF_COLONY &lt;= 1000 then &quot;MEDIUM&quot;
        else &quot;HIGH&quot;
    end as SIZE
from ECOLI_DATA</code></pre>