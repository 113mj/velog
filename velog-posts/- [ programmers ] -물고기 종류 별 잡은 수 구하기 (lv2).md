<h3 id="문제-설명">문제 설명</h3>
<p>낚시앱에서 사용하는 <code>FISH_INFO</code> 테이블은 잡은 물고기들의 정보를 담고 있습니다. <code>FISH_INFO</code> 테이블의 구조는 다음과 같으며 <code>ID</code>, <code>FISH_TYPE</code>, <code>LENGTH</code>, <code>TIME</code>은 각각 잡은 물고기의 ID, 물고기의 종류(숫자), 잡은 물고기의 길이(cm), 물고기를 잡은 날짜를 나타냅니다.</p>
<p>단, 잡은 물고기의 길이가 10cm 이하일 경우에는 LENGTH 가 NULL 이며, LENGTH 에 NULL 만 있는 경우는 없습니다.</p>
<p><code>FISH_NAME_INFO</code> 테이블은 물고기의 이름에 대한 정보를 담고 있습니다. <code>FISH_NAME_INFO</code> 테이블의 구조는 다음과 같으며, <code>FISH_TYPE</code>, <code>FISH_NAME</code> 은 각각 물고기의 종류(숫자), 물고기의 이름(문자) 입니다.</p>
<h3 id="문제">문제</h3>
<p><code>FISH_NAME_INFO</code>에서 물고기의 종류 별 물고기의 이름과 잡은 수를 출력하는 SQL문을 작성해주세요.</p>
<p>물고기의 이름 컬럼명은 FISH_NAME, 잡은 수 컬럼명은 FISH_COUNT로 해주세요.
결과는 잡은 수 기준으로 내림차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>FISH_INFO</p>
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
<p>FISH_NAME_INFO</p>
<table>
<thead>
<tr>
<th>Column Name</th>
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
<p>문제에서 물고기의 종류에 대한 수와 이름을 출력해야하기 때문에 <code>GROUP BY</code>를 사용합니다. 여기서 물고기에 대한 그룹화를 <code>fish_name</code> 을 사용합니다. 왜냐하면 물고기의 이름을 출력해야 하며 <code>FISH_TYPE</code>와 <code>FISH_NAME</code>은 1 대1로 매핑이 되기 때문에 <code>FISH_TYPE</code> 으로 그룹화를 한 결과와 <code>FISH_NAME</code> 으로 그룹화 한 결과가 같기 때문입니다. 그 다음 <code>COUNT()</code> 를 통해 물고기의 수를 세며 마지막으로 물고기의 수로 데이터 정렬을 하기 위해 <code>ORDER BY</code> 를 사용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">select
    count(ID) as FISH_COUNT,
    n.FISH_NAME
from FISH_NAME_INFO n
join FISH_INFO i on n.FISH_TYPE = i.FISH_TYPE
group by (n.FISH_NAME)
order by FISH_COUNT DESC;</code></pre>