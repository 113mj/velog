<h3 id="문제-설명">문제 설명</h3>
<p>어느 한 게임에서 사용되는 아이템들은 업그레이드가 가능합니다.
'ITEM_A'-&gt;'ITEM_B'와 같이 업그레이드가 가능할 때
'ITEM_A'를 'ITEM_B'의 PARENT 아이템,
PARENT 아이템이 없는 아이템을 ROOT 아이템이라고 합니다.</p>
<p>예를 들어 'ITEM_A'-&gt;'ITEM_B'-&gt;'ITEM_C' 와 같이 업그레이드가 가능한 아이템이 있다면
'ITEM_C'의 PARENT 아이템은 'ITEM_B'
'ITEM_B'의 PARENT 아이템은 'ITEM_A'
ROOT 아이템은 'ITEM_A'가 됩니다.</p>
<p>다음은 해당 게임에서 사용되는 아이템 정보를 담은 <code>ITEM_INFO</code> 테이블과 아이템 관계를 나타낸 <code>ITEM_TREE</code> 테이블입니다. <code>ITEM_INFO</code> 테이블은 다음과 같으며, <code>ITEM_ID</code>, <code>ITEM_NAME</code>, <code>RARITY</code>, <code>PRICE</code>는 각각 아이템 ID, 아이템 명, 아이템의 희귀도, 아이템의 가격을 나타냅니다.</p>
<p><code>ITEM_TREE</code> 테이블은 다음과 같으며, <code>ITEM_ID</code>, <code>PARENT_ITEM_ID</code>는 각각 아이템 ID, PARENT 아이템의 ID를 나타냅니다.</p>
<p>단, 각 아이템들은 오직 하나의 PARENT 아이템 ID를 가지며, ROOT 아이템의 PARENT 아이템 ID는 NULL 입니다.</p>
<p>ROOT 아이템이 없는 경우는 존재하지 않습니다.</p>
<h3 id="문제">문제</h3>
<p>ROOT 아이템을 찾아 아이템 ID(ITEM_ID), 아이템 명(ITEM_NAME)을 출력하는 SQL문을 작성해 주세요. 이때, 결과는 아이템 ID를 기준으로 오름차순 정렬해 주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>ITEM_INFO</p>
<table>
<thead>
<tr>
<th>ITEM_ID</th>
<th>ITEM_NAME</th>
<th>RARITY</th>
<th>PRICE</th>
</tr>
</thead>
<tbody><tr>
<td>0</td>
<td>ITEM_A</td>
<td>COMMON</td>
<td>10000</td>
</tr>
<tr>
<td>1</td>
<td>ITEM_B</td>
<td>LEGEND</td>
<td>9000</td>
</tr>
<tr>
<td>2</td>
<td>ITEM_C</td>
<td>LEGEND</td>
<td>11000</td>
</tr>
<tr>
<td>3</td>
<td>ITEM_D</td>
<td>UNIQUE</td>
<td>10000</td>
</tr>
<tr>
<td>4</td>
<td>ITEM_E</td>
<td>LEGEND</td>
<td>12000</td>
</tr>
</tbody></table>
<p>ITEM_TREE</p>
<table>
<thead>
<tr>
<th>Column name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>ITEM_ID</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>PARENT_ITEM_ID</td>
<td>INTEGER</td>
<td>TRUE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>ROOT 아이템은 <code>PARENT_ITEM_ID</code>가 없는 아이템이기 때문에 <code>JOIN</code>연산을 한 뒤 <code>PARENT_ITEM_ID</code>가 없는 아이템을 추출하면 됩니다. 그 뒤로 <code>ITEM_ID</code>를 기준으로 정렬을 위해 <code>ORDER BY</code>를 사용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    i.ITEM_ID,
    i.ITEM_NAME
from ITEM_INFO i
join ITEM_TREE t on i.ITEM_ID = t.ITEM_ID
where t.PARENT_ITEM_ID is NULL
order by i.ITEM_ID</code></pre>