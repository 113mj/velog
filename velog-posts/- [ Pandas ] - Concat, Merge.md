<h3 id="concat">Concat</h3>
<p><code>concat()</code>은 데이터프레임을 <code>axis</code>을 기준으로 붙이는 함수입니다. <code>axis</code>는 기본값으로 0으로 설정되어 있습니다. 데이터가 없는 값은 NaN값으로 설정됩니다.</p>
<pre><code class="language-python">df1 = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
df2 = pd.DataFrame({'A': [5, 6], 'B': [7, 8]})

# 행 방향으로 결합
result = pd.concat([df1, df2], axis=0)
print(result)</code></pre>
<p>위 결과는 다음과 같습니다.</p>
<pre><code>   A  B
0  1  3
1  2  4
0  5  7
1  6  8</code></pre><p>아래는 <code>axis</code>가 1인 경우 입니다.</p>
<pre><code class="language-python">df3 = pd.DataFrame({'A': [1, 2]}, index=[0, 1])
df4 = pd.DataFrame({'B': [3, 4]}, index=[1, 2])

result = pd.concat([df3, df4], axis=1)
print(result)</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>     A    B
0  1.0  NaN
1  2.0  3.0
2  NaN  4.0
</code></pre><h3 id="merge">Merge</h3>
<p><code>merge()</code>는 특정한 고유 키를 기준으로 데이터를 병합하는 함수입니다.
<code>how</code>를 통해 병합 방식(INNER, LEFT, RIGHT, OUTER)을 설정할 수 있습니다.</p>
<ul>
<li>inner: 공통된 키에 해당하는 데이터만 결합합니다 (기본값).</li>
<li>outer: 두 데이터프레임의 모든 키를 포함합니다.</li>
<li>left: 왼쪽 데이터프레임의 모든 키를 유지하며, 오른쪽 데이터를 병합합니다.</li>
<li>right: 오른쪽 데이터프레임의 모든 키를 유지하며, 왼쪽 데이터를 병합합니다.<pre><code class="language-python">df1 = pd.DataFrame({'key': ['A', 'B', 'C'], 'value1': [1, 2, 3]})
df2 = pd.DataFrame({'key': ['A', 'B', 'D'], 'value2': [4, 5, 6]})
result = pd.merge(df1, df2, on='key', how='inner')
print(result)</code></pre>
위 코드의 결과는 다음과 같습니다.<pre><code>key  value1  value2
0   A       1       4
1   B       2       5</code></pre>옵션이 <code>inner</code>이기 때문에 공통된 키인 A와 B만 결합된 것을 확인할 수 있습니다.</li>
</ul>