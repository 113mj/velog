<h3 id="apply">apply</h3>
<p><code>apply()</code> 는 판다스(Pandas)에서 데이터 프레임이나 시리즈의 데이터에 사용자 정의 함수를 적용할 때 사용되는 함수입니다. 레코드 단위로 함수가 실행되며 사용자 정의 함수는 반드시 리턴이 있어야 합니다. 인수로는 함수 이름과 <code>axis</code>가 들어갑니다.</p>
<pre><code class="language-python">def pclass_sibsp(row):
    if row['Pclass'] == 1 and row['SibSp'] ==1:
        return 1
    else:
        return 0

df1 = df.copy()
df1['pclass_sibsp_filter'] = df1.apply(pclass_sibsp, axis = 1) 
df1.head()
</code></pre>
<p>여기서 <code>axis</code>는 <code>apply()</code>의 적용 범위를 말합니다. 0이라면 행이 증가하는 방향으로 1이면 열이 증가하는 방향으로 데이터가 넘어갑니다. 
위 코드의 실행 결과는 다음과 같습니다.</p>
<pre><code>0이라면 행이 증가하는 방향 데이터가 넘어감 1이면 열이 증가하는 방향 데이터 넘어감.</code></pre><p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/6775d39a-154e-4b48-9607-ac87040c600b/image.png" /></p>
<h3 id="map">map</h3>
<p><code>map()</code>은 값을 특정 값으로 치환하거나 변환할 때 사용하는 함수입니다. 데이터 전처리 과정에서 특정 값을 다른 값으로 바꾸거나 매핑할 때 자주 사용됩니다.</p>
<pre><code class="language-python">gender_map = {
    &quot;male&quot; : &quot;남자&quot;,
    &quot;female&quot; : &quot;여자&quot;
}

df1['Sex_kr'] = df1['Sex'].map(gender_map)
df1.head()</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/9cc3b49d-95e8-4c29-90e9-15fcf6f18cc9/image.png" /></p>