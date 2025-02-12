<h3 id="문제">문제</h3>
<p>FISH_INFO 테이블에서 잡은 BASS와 SNAPPER의 수를 출력하는 SQL 문을 작성해주세요.</p>
<p>컬럼명은 FISH_COUNT로 해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>FISH_INFO</p>
<table>
<thead>
<tr>
<th>Column name</th>
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
<td>FISH_TYPE</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>LENGTH</td>
<td>FLOAT</td>
<td>TRUE</td>
</tr>
<tr>
<td>TIME</td>
<td>DATE</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="두-번째-테이블">두 번째 테이블</h3>
<p>FISH_NAME_INFO</p>
<table>
<thead>
<tr>
<th>Column name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>FISH_TYPE</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>FISH_NAME</td>
<td>VARCHAR</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>일단 문제에서 조회할 column들이 두 테이블에 있기 때문에 먼저 조인을 먼저 했습니다. 다음으로 잡은 물고기가 'BASS'와 'SNAPPER'인지를 <code>where</code> 절에 <code>IN</code>을 써서 필터링은 했습니다. 마지막으로 필터링한 물고기의 수를 구하기 위해 <code>COUNT</code>를 사용했습니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    COUNT(ID) AS FISH_COUNT
from FISH_INFO i
join FISH_NAME_INFO n on i.FISH_TYPE = n.FISH_TYPE
where n.FISH_NAME IN ('BASS', 'SNAPPER');</code></pre>