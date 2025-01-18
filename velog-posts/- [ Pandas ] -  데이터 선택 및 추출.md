<p>이 글은 다음과 같은 데이터를 사용합니다.</p>
<pre><code>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 891 entries, 0 to 890
Data columns (total 12 columns):
 #   Column       Non-Null Count  Dtype  
---  ------       --------------  -----  
 0   PassengerId  891 non-null    int64  
 1   Survived     891 non-null    int64  
 2   Pclass       891 non-null    int64  
 3   Name         891 non-null    object 
 4   Sex          891 non-null    object 
 5   Age          714 non-null    float64
 6   SibSp        891 non-null    int64  
 7   Parch        891 non-null    int64  
 8   Ticket       891 non-null    object 
 9   Fare         891 non-null    float64
 10  Cabin        204 non-null    object 
 11  Embarked     889 non-null    object 
dtypes: float64(2), int64(5), object(5)
memory usage: 83.7+ KB</code></pre><h3 id="행-열-조회">행, 열 조회</h3>
<p>행에서 데이터를 조회하는 방법은 슬라이스 기호를 통해 할 수 있습니다.</p>
<pre><code class="language-python">df[:3]</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/042b5898-6338-4697-9e5f-c1dbf9245988/image.png" /></p>
<p>열에서 데이터를 가져오려면 데이터프레임에 칼럼 이름(column name)을 대괄호 안에 넣으면 됩니다.</p>
<pre><code class="language-python">df['Fare'] </code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>0       7.2500
1      71.2833
2       7.9250
3      53.1000
4       8.0500
        ...   
886    13.0000
887    30.0000
888    23.4500
889    30.0000
890     7.7500
Name: Fare, Length: 891, dtype: float64</code></pre><h3 id="fancyindexing-사용">FancyIndexing 사용</h3>
<p>FancyIndexing을 사용하여 원하는 행의 데이터를 추출할 수 있다.Fancy Indexing은 Python의 NumPy 라이브러리에서 제공하는 고급 인덱싱 방법으로, 정수 배열이나 Boolean 배열을 사용해 배열의 특정 요소를 선택할 수 있는 기능입니다</p>
<pre><code class="language-python">columns = ['Survived', 'Pclass', 'Name']
df[columns]</code></pre>
<p>위 코드의 실행 결과는 다음과 같습니다.
<img src="https://velog.velcdn.com/images/1113mj/post/ce4d5934-eec7-48b8-bfb2-81678e3c37a9/image.png" /></p>
<h3 id="loc-iloc">loc[], iloc[]</h3>
<p><code>loc[]</code> 는 데이터프레임의 column과 row를 검색할 수 있는 속성입니다. 여기서 <code>loc[]</code> 는 괄호 안에 column이나 row의 이름을 받습니다.</p>
<pre><code class="language-python">df.loc[3:5, 'Name'] </code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>3    Futrelle, Mrs. Jacques Heath (Lily May Peel)
4                        Allen, Mr. William Henry
5                                Moran, Mr. James
Name: Name, dtype: object</code></pre><p><code>iloc[]</code>는 데이터프레임의 column과 row를 숫자 인덱스로 검색할 수 있는 속성입니다. <code>iloc()</code> 는 괄호 안에 숫자 인덱스를 받습니다.</p>
<pre><code class="language-python">df.iloc[3:5, 2]</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>3    1
4    3
Name: Pclass, dtype: int64</code></pre><h3 id="loc를-이용한-조건-추출">loc[]를 이용한 조건 추출</h3>
<p><code>loc[]</code>를 통해 행(레코드)에 대한 조건을 설정하여 원하는 조건에 맞는 행만 추출할 수 있습니다.</p>
<pre><code class="language-python">mask = df['Pclass'] == 1
mask
df.loc[mask]</code></pre>
<p>마스크(mask)는 조건에 따라 True 또는 False 값을 가지는 Boolean 배열입니다.
이 마스크를 데이터프레임이나 배열에 적용하면, True에 해당하는 데이터만 필터링됩니다.</p>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/2f0f8116-174e-4012-9c69-696c26dbfa1c/image.png" /></p>
<h3 id="query">query()</h3>
<p><code>query()</code>는 문자열 기반으로 조건을 지정하여 검색할 수 있는 메서드입니다.</p>
<pre><code class="language-python">df.query('Pclass == 1 and Age &gt;= 30')[[&quot;Name&quot;, &quot;Age&quot;, &quot;Pclass&quot;]]</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/15f73430-c596-4bc8-91ee-1358e84794f0/image.png" /></p>