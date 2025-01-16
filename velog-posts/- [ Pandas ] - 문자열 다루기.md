<h3 id="문자열-다루기">문자열 다루기</h3>
<p>pandas에는 데이터들의 문자열을 다룰 수 있는 메소드들이 있습니다. 이 메소드들은 다음과 같습니다. </p>
<table>
<thead>
<tr>
<th align="left">메소드</th>
<th align="left">설명</th>
</tr>
</thead>
<tbody><tr>
<td align="left"><code>.str.contains(문자열)</code></td>
<td align="left">문자열을 포함하고 있는지 유무</td>
</tr>
<tr>
<td align="left"><code>.str.replace(기존문자열, 대치문자열)</code></td>
<td align="left">문자열 대치</td>
</tr>
<tr>
<td align="left"><code>.str.split(문자열, expand=True/False, n=개수)</code></td>
<td align="left">특정 문자열을 기준으로 쪼개기</td>
</tr>
<tr>
<td align="left"><code>.str.lower()</code></td>
<td align="left">소문자로 바꾸기</td>
</tr>
<tr>
<td align="left"><code>.str.upper()</code></td>
<td align="left">대문자로 바꾸기</td>
</tr>
</tbody></table>
<p>예시는 다음과 같습니다.</p>
<pre><code class="language-python">df2 = df.copy()

miss_mask = df2['Name'].str.contains(&quot;Miss&quot;)
df2.loc[miss_mask].head()</code></pre>
<p>여기서 시리즈 내에 문자열에 하나하나 접근을 하기 위해 str을 사용합니다.
위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/fe5c4630-0c01-46c8-ad99-5a2dbfb7fe35/image.png" /></p>