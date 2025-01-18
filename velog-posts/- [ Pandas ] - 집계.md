<p>데이터 분석에서 집계(Aggregation)는 다수의 데이터를 하나로 요약하는 과정입니다. 이를 통해 데이터의 전반적인 특징을 빠르게 파악하거나, 의사결정을 위한 핵심 지표를 확인할 수 있습니다. 이 글에서는 데이터 집계에 사용되는 다양한 함수와 그 의미를 정리합니다.</p>
<h3 id="groupby">groupby()</h3>
<p><code>groupby()</code> 는 데이터를 하나로 묶는 기능을 가진 함수입니다. 함수의 인수로는 column의 이름이 들어갑니다. </p>
<pre><code class="language-python">df.groupby(&quot;Pclass&quot;)</code></pre>
<p>위 코드를 실행하면 다음과 같은 결과가 나옵니다.</p>
<pre><code>&lt;pandas.core.groupby.generic.DataFrameGroupBy object at 0x7fffba080910&gt;</code></pre><p>위 결과의 의미는 <code>DataFrameGroupBy</code>라는 객체가 생성되었다는 의미입니다.</p>
<h3 id="집계-함수">집계 함수</h3>
<table>
<thead>
<tr>
<th align="left">함수</th>
<th align="left">설명</th>
</tr>
</thead>
<tbody><tr>
<td align="left">count()</td>
<td align="left">행의 갯수</td>
</tr>
<tr>
<td align="left">nunique()</td>
<td align="left">행의 유니크한 갯수</td>
</tr>
<tr>
<td align="left">sum()</td>
<td align="left">합</td>
</tr>
<tr>
<td align="left">mean()</td>
<td align="left">평균</td>
</tr>
<tr>
<td align="left">min()</td>
<td align="left">최솟값</td>
</tr>
<tr>
<td align="left">max()</td>
<td align="left">최댓값</td>
</tr>
<tr>
<td align="left">std()</td>
<td align="left">표준편차</td>
</tr>
<tr>
<td align="left">var()</td>
<td align="left">분산</td>
</tr>
<tr>
<td align="left">위 함수는 그룹에 대해 계산을 할 수 있는 집계함수입니다. NaN값은 계산에서 제외됩니다.</td>
<td align="left"></td>
</tr>
</tbody></table>
<pre><code class="language-python">df.groupby(&quot;Pclass&quot;).count()</code></pre>
<p>위 코드의 실행 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/e1fe1bdb-8ef2-4335-b7c0-e6ece3e30383/image.png" /></p>
<h3 id="다중-그룹">다중 그룹</h3>
<p>다중 그룹은 둘 이상의 column 이름을 <code>groupby()</code>의 인수로 사용하여 만들 수 있습니다.</p>
<pre><code class="language-python">df.groupby([&quot;Sex&quot;, &quot;Pclass&quot;]).mean(numeric_only=True)</code></pre>
<p>코드에서 <code>numeric_only = True</code> 를 사용한 이유는 문자열 데이터도 계산하기 때문입니다. 위 코드의 결과는 다음과 같습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/4377758e-523a-4aff-bd59-38b8f660a7a3/image.png" /></p>
<h3 id="crosstab">crosstab</h3>
<p><code>crosstab()</code>은 범주형 데이터를 비교 분석하는 데 유용한 도구로, 데이터 간 관계를 이해하거나 특정 기준에 따라 데이터를 요약할 때 사용됩니다. 행에는 그룹핑할 데이터, 열에는 계산을 할 데이터를 지정합니다.</p>
<pre><code class="language-python">pd.crosstab(df['Sex'], df['Survived'])</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/bd88d340-10ae-48be-8e60-7150d20bec47/image.png" /></p>
<h3 id="범주별-비율-구하기">범주별 비율 구하기</h3>
<p><code>normalize</code>은 <code>crosstab()</code>으로 생성된 데이터를 비율로 변환해주는 옵션입니다. 이를 통해 데이터의 상대적인 분포를 파악할 수 있습니다.
여기서 사용할 수 있는 옵션은 다음과 같습니다.</p>
<ul>
<li>normalize='all': 전체 데이터를 기준으로 비율 계산 (전체 합이 100%).</li>
<li>normalize='index': 각 행별 데이터를 기준으로 비율 계산 (행별 합이 100%).</li>
<li>normalize='columns': 각 열별 데이터를 기준으로 비율 계산 (열별 합이 100%).</li>
</ul>
<p>그리고 <code>margins</code>은 행과 열의 합계를 포함한 총계(row/column-wise total) 추가됩니다. </p>
<pre><code class="language-python">pd.crosstab(df['Sex'], df['Survived'], normalize='all', margins = True)</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/ed5260df-1970-4324-9083-919fe3234ee8/image.png" /></p>
<h3 id="다중-인덱스-다중-컬럼의-범주표">다중 인덱스, 다중 컬럼의 범주표</h3>
<p><code>crosstab()</code>로 다중 인덱스, 다중 컬럼을 출력하는 방법은 인수에 리스트형으로 출력하고자 하는 index와 column을 기입하면 됩니다.</p>
<pre><code class="language-python">pd.crosstab(index=[df['Sex'], df['Pclass']], columns=[df['Survived'], df['Embarked']])</code></pre>
<p>위 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/31e08821-bcdb-454c-b128-fb3819838cc7/image.png" />
위 결과를 통해 데이터에서 <code>sex</code>속성이 'female'이며 <code>Pclass</code>속성이 1인 사람이 <code>Survived</code>속성이 0이며 <code>Embarked</code>속성이 'C'인 사람은 1명이다는 정보를 알 수 있습니다.</p>
<h3 id="pivot-table">pivot table()</h3>
<p><code>pivot_table()</code> 는 데이터를 특정 기준으로 그룹화하고, 계산하여 표 형태로 변환하는 함수입니다. 인수로 받는 값은 다음과 같습니다.</p>
<ul>
<li>data: 사용할 데이터프레임</li>
<li>index: 테이블의 행으로 들어갈 기존 데이터프레임의 열</li>
<li>columns: 테이블의 열로 들어갈 기존 데이터프레임의 열</li>
<li>values: 집계할 데이터를 포함하는 열.</li>
<li>aggfunc: 각 그룹 별로 값들을 조회할 함수</li>
<li>fillvalue: NaN값을 대체할 값.</li>
</ul>
<pre><code class="language-python">pd.pivot_table(
    df,
    index='Sex',
    columns='Pclass',
    values='Fare',
    aggfunc='mean',
    margins = True
)</code></pre>
<p>위 코드의 결과는 다음과 같다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/2fa2176c-85ac-435d-931d-f8d2aeed3a16/image.png" />
위 결과를 통해 데이터에서 <code>sex</code> 속성이 'female'인 사람중 <code>Pclass</code> 속성이 1인 사람들의 <code>Fare</code> 의 평균은 106.125798이다라는 정보를 알 수 있습니다.</p>
<p><code>pivot_table()</code>도 마찬가지로 다중 인덱스와 다중 컬럼을 사용할 수 있습니다.</p>
<pre><code class="language-python">pd.pivot_table(
    df,
    index=['Sex','Pclass'],
    columns=['Survived', 'Embarked'],
    values = 'Fare',
    aggfunc = 'mean'
)</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/fd5fdc0c-0c71-4cbc-a924-ad52449c1256/image.png" /></p>
<h3 id="stack-unstack">stack(), unstack()</h3>
<p><code>stack()</code>은 column 레벨에서 index 레벨로 데이터프레임을 변경하는 함수입니다.
<code>unstack()</code>은 <code>unstack()</code>과 반대로 index 레벨에서 column 레벨로 데이터프레임을 변경하는 함수입니다.
두 함수 인수로 변경할 레벨을 입력 받습니다.</p>
<pre><code class="language-python">pivot = pd.pivot_table(
    df,
    index = ['Sex', 'Pclass'],
    values=['Survived', &quot;Fare&quot;],
    aggfunc=['mean', 'median', 'sum']
)
pivot</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/8b9f748d-0386-49e6-879c-659dff1ba2fe/image.png" /></p>
<pre><code class="language-python">pivot.stack(0) </code></pre>
<p>위 코드를 실행하면 다음과 같은 결과가 나옵니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/e5d9859f-ace4-48a9-96b5-a70704847cd5/image.png" />
위 표를 보시면 column의 첫 번째 레벨인 <code>mean</code>, <code>median</code>, <code>sum</code>가 row로 내려간 것을 확인할 수 있습니다.</p>
<pre><code>pivot.unstack(0) # 행 index의 첫 번째 레벨을 column으로 올린다.</code></pre><p>위 코드를 실행하면 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/dc8c3601-9f39-4c17-b586-8b6506ec96ab/image.png" />
위 표를 보시면 row의 첫번째 레벨인 <code>sex</code>가 column으로 올라간 것을 확인할 수 있습니다.</p>
<h3 id="melt">melt()</h3>
<p><code>melt()</code>는 데이터프레임의 column 값을 행으로 변환하는 함수입니다. </p>
<pre><code class="language-python">data = {
    '이름': ['Alice', 'Bob', 'Charlie'],
    '국어': [85, 90, 95],
    '수학': [88, 92, 96],
    '영어': [87, 91, 93]
}
df = pd.DataFrame(data)
df</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/18f7bad0-827c-4c07-ad8d-c221fa894f8b/image.png" />
여기서 <code>melt()</code>를 사용하면 다음과 같습니다.</p>
<pre><code class="language-python">melted_df = pd.melt(
    df,
    id_vars=['이름'],
    value_vars=['국어', '수학', '영어'],
    var_name='과목',
    value_name='점수'
)
melted_df</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/7ff95ad5-68a0-4f04-b0c5-8861b9e8076b/image.png" />
위 사진을 보면 <code>이름</code>이라는 속성을 기준으로 다른 column이 index로 들어온 것을 확인할 수 있다.</p>
<p>column -&gt; record:  melt
column -&gt; index : stack</p>