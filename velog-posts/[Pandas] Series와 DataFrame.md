<h3 id="series">Series</h3>
<p>Series는 엑셀의 한 열(column)이나 리스트에 해당하는 데이터구조입니다. 각각의 값은 인덱스와 연결되어 있으며, 하나의 데이터 속성을 표현합니다.</p>
<pre><code class="language-python"># dict를 이용해 Series 만들기
sample_dict = {&quot;a&quot; : 1, &quot;b&quot; : 2, &quot;c&quot; : 3} # a, b, c: 각 타겟의 고유한 값
dict_series = pd.Series(sample_dict)
print(dict_series)</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>a    1
b    2
c    3
dtype: int64</code></pre><h3 id="dataframe">DataFrame</h3>
<p>DataFrame은 엑셀의 전체 시트(sheet)처럼 행(row)과 열(column)로 구성된 데이터 테이블입니다. 여러 개의 Series가 열 단위로 모여서 만들어집니다.</p>
<pre><code class="language-python">sample_dict = {
    'Name': [&quot;A&quot;, &quot;B&quot;, &quot;C&quot;],
    'height': [180.5, 173.1, 178.3],
}

df = pd.DataFrame(sample_dict)
df</code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>    Name    height
0    A        180.5
1    B        173.1
2    C        178.3</code></pre><h3 id="series를-합쳐서-dataframe-만들기">Series를 합쳐서 DataFrame 만들기</h3>
<pre><code class="language-python">name_series = pd.Series([&quot;A&quot;, &quot;B&quot;, &quot;C&quot;])
height_series = pd.Series([180.3, 175.3, 178.3])

df = pd.DataFrame({&quot;name&quot;: name_series, 'height': height_series})
df</code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>    name    height
0    A        180.3
1    B        175.3
2    C        178.3</code></pre><h3 id="jsonarray-형식으로-된-데이터를-데이터프레임으로-만들기">JSONArray 형식으로 된 데이터를 데이터프레임으로 만들기.</h3>
<pre><code>json_sample_array = [
    {&quot;name&quot; : &quot;A&quot;, 'height': 180.3},
    {&quot;name&quot; : &quot;B&quot;, 'height': 178.3},
    {&quot;name&quot; : &quot;C&quot;, 'height': 175.3}
]
df = pd.DataFrame(json_sample_array)
df</code></pre><p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>    name    height
0    A        180.3
1    B        178.3
2    C        175.3</code></pre>