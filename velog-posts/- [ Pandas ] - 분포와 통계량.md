<p>집계를 하면 반드시 하나의 결과값이 나옵니다.
이러한 과정을 공학적으로 Reduce 통계적으로 aggregation(집계)라고 합니다.
1개의 값은 대표값, 통계량이라고 표현됩니다. 
통계량에는 (평균, 표준편차, 분산, 중앙값, 최빈값, .. )것들이 있습니다.</p>
<h3 id="describe">describe()</h3>
<p><code>describe()</code>은  column별 값의 개수, 평균, 표준편차, 최솟값, 최댓값, 사분위수 보여주는 메서드입니다.</p>
<pre><code class="language-python">import pandas as pd

df=pd.read_csv(&quot;./data/titanic_train.csv&quot;)
df.describe()</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/ee591b51-7e31-41ee-91dc-a0c1981480fa/image.png" /></p>
<h3 id="대푯값">대푯값</h3>
<table>
<thead>
<tr>
<th align="left">메소드</th>
<th align="left">설명</th>
</tr>
</thead>
<tbody><tr>
<td align="left">min()</td>
<td align="left">최솟값</td>
</tr>
<tr>
<td align="left">max()</td>
<td align="left">최댓값</td>
</tr>
<tr>
<td align="left">mean()</td>
<td align="left">평균</td>
</tr>
<tr>
<td align="left">median()</td>
<td align="left">중간값</td>
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
<td align="left">quantile()</td>
<td align="left">분위수</td>
</tr>
</tbody></table>
<p>위 메서드를 통해 데이터프레임의 대푯값이나, 특정 컬럼에 대한 대푯값을 구할 수 있습니다.</p>
<pre><code class="language-python">df.median(numeric_only=True)</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>PassengerId    446.0000
Survived         0.0000
Pclass           3.0000
Age             28.0000
SibSp            0.0000
Parch            0.0000
Fare            14.4542
dtype: float64</code></pre><h3 id="corr">corr</h3>
<p><code>corr()</code>는 데이터프레임에서 각 열 간의 상관관계를 계산하는 메서드입니다. 
상관계수는 두 변수가 얼마나 함께 변하는지를 나타내는 값으로, 다음과 같은 정의를 가집니다 </p>
<blockquote>
<p>상관계수(𝑟) = 두 변수가 함께 변하는 정도 (동분산) / 각 변수가 변하는 정도 (각 분산의 곱)</p>
</blockquote>
<p>상관계수의 값은 -1부터 1 사이로 나타나며, 다음과 같이 해석됩니다.</p>
<ul>
<li>1: 완벽한 양의 상관관계 (한 변수가 증가하면 다른 변수도 비례적으로 증가)</li>
<li>0: 상관관계 없음 (두 변수 간에 패턴이 없음)</li>
<li>-1: 완벽한 음의 상관관계 (한 변수가 증가하면 다른 변수는 반비례적으로 감소)<pre><code class="language-python">df.corr(numeric_only=True)</code></pre>
위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/5ee74eab-2f04-44e0-bc7d-ebf544b12958/image.png" /></li>
</ul>