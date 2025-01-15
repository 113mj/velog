<p>이 글에서 다룰 데이터 정보는 다음과 같습니다.</p>
<pre><code>&lt;class 'pandas.core.frame.DataFrame'&gt;
RangeIndex: 3650 entries, 0 to 3649
Data columns (total 2 columns):
 #   Column  Non-Null Count  Dtype  
---  ------  --------------  -----  
 0   Date    3650 non-null   object 
 1   Temp    3650 non-null   float64
dtypes: float64(1), object(1)
memory usage: 57.2+ KB</code></pre><h3 id="날짜-데이터">날짜 데이터</h3>
<p>날짜 데이터는 특정 시점을 표현하거나 저장하는 데 사용되는 데이터 타입입니다. 날짜 데이터를 출력하고 저장하는 방법에 대해 이 글에서 자세히 살펴보겠습니다.</p>
<h3 id="문자형을-날짜형으로-변경">문자형을 날짜형으로 변경</h3>
<p>위 데이터를 보면 <code>Date</code> 에 들어온 데이터는 <code>object</code> 형태로 저장되어 있습니다. 여기서 <code>object</code> 는 문자열 데이터입니다. 이 데이터를 날짜형으로 변경하려면 다음과 같은 메소드를 사용하면 됩니다.</p>
<pre><code class="language-python">pd.to_datetime('column_name', format='날짜 형식')</code></pre>
<p>여기서 날짜 형식 포멧은 다음과 같습니다.</p>
<table>
<thead>
<tr>
<th align="left">형식</th>
<th align="left">설명</th>
</tr>
</thead>
<tbody><tr>
<td align="left">%Y</td>
<td align="left">0을 채운 4자리 연도</td>
</tr>
<tr>
<td align="left">%y</td>
<td align="left">0을 채운 2자리 연도</td>
</tr>
<tr>
<td align="left">%m</td>
<td align="left">0을 채운 월</td>
</tr>
<tr>
<td align="left">%d</td>
<td align="left">0을 채운 일</td>
</tr>
<tr>
<td align="left">%H</td>
<td align="left">0을 채운 시간</td>
</tr>
<tr>
<td align="left">%M</td>
<td align="left">0을 채운 분</td>
</tr>
<tr>
<td align="left">%S</td>
<td align="left">0을 채운 초</td>
</tr>
</tbody></table>
<p>위 코드를 사용한 예시는 다음과 같습니다.</p>
<pre><code class="language-python">df['Date1'] = pd.to_datetime(df['Date'], format='%Y-%m-%d')
df.info()</code></pre>
<p>위 코드는 <code>Date</code> 열의 데이터를 <code>%Y-%m-%d</code> 형식으로 변환하여, 변환된 값을 새로운 열인 <code>Date1</code>에 저장합니다.</p>
<h3 id="dfcolumn_namedtstrftimeformat">df['column_name'].dt.strftime(&quot;format&quot;)</h3>
<p><code>df['column_name'].dt.strftime(&quot;format&quot;)</code> 은 날짜 데이터 형식을 자신이 원하는 format에 맞게 저장할 수 있는 메서드입니다. 여기서 <code>column_name</code>은 변환할 날짜 데이터를 포함한 열의 이름이며, <code>format</code>은 원하는 날짜 형식을 지정하는 문자열입니다.&quot;</p>
<pre><code class="language-python">df['Date1'].dt.strftime(&quot;%Y년 %m월&quot;)</code></pre>
<p>위 코드의 실행 결과는 다음과 같습니다.</p>
<pre><code>0       1981년 01월
1       1981년 01월
2       1981년 01월
3       1981년 01월
4       1981년 01월
          ...    
3645    1990년 12월
3646    1990년 12월
3647    1990년 12월
3648    1990년 12월
3649    1990년 12월
Name: Date1, Length: 3650, dtype: object</code></pre><h3 id="날짜-계산">날짜 계산</h3>
<p>날짜 계산과 관련된 메서드는 다음과 같습니다.</p>
<ul>
<li>day 연산: <code>pd.Timedelta(day=숫자)</code></li>
<li>month 연산: <code>DateOffset(months=숫자)</code></li>
<li>year 연산: <code>DateOffset(years=숫자)</code></li>
</ul>
<p>먼저 <code>pd.Timedelta(day=숫자)</code> 부터 알아보겠습니다.</p>
<pre><code class="language-python">df['plus day1'] = df['Date1'] + pd.Timedelta(days=1)
df.head()</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<img src="https://velog.velcdn.com/images/1113mj/post/4b098028-84a9-4d82-91cb-d5644e5e3d19/image.png" width="500" />

<p>다음 <code>DateOffset(months=숫자)</code> 를 사용해보겠습니다.</p>
<pre><code class="language-python">from pandas.tseries.offsets import DateOffset

df['plus month1'] = df['Date1'] + DateOffset(months=1)
df.head()</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<img src="https://velog.velcdn.com/images/1113mj/post/ed80369c-7a09-4912-b774-44ec11384a5c/image.png" width="600" />

<p>마지막으로 <code>DateOffset(years=숫자)</code>를 사용해보겠습니다.</p>
<pre><code class="language-python">df['plus year1'] = df['Date1'] + DateOffset(years=1)
df.head()</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img src="https://velog.velcdn.com/images/1113mj/post/518ee9e9-ce47-47fa-92e2-98317146f7ab/image.png" width="600" /></p>
<h3 id="날짜-구간-데이터-만들기">날짜 구간 데이터 만들기</h3>
<p><code>pd.date_range(start=시작일자, end=종료일자, periods=기간수, freq=주기)</code></p>
<table>
<thead>
<tr>
<th align="left">형식</th>
<th align="left">설명</th>
</tr>
</thead>
<tbody><tr>
<td align="left">D</td>
<td align="left">일별</td>
</tr>
<tr>
<td align="left">W</td>
<td align="left">주별</td>
</tr>
<tr>
<td align="left">M</td>
<td align="left">월별 말일</td>
</tr>
<tr>
<td align="left">MS</td>
<td align="left">월별 시작일</td>
</tr>
<tr>
<td align="left">A</td>
<td align="left">연도별 말일</td>
</tr>
<tr>
<td align="left">AS</td>
<td align="left">연도별 시작일</td>
</tr>
<tr>
<td align="left">날짜 구간 데이터는 특정 시작일과 종료일 사이에 일정한 간격으로 날짜를 생성해야 할 때 사용합니다. 아래는 이를 활용한 코드 예시입니다.</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">```python</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">pd.date_range(start = '2024-01-01', end = &quot;2035-12-15&quot;, freq = &quot;A&quot;)</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">```</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">위 코드의 결과는 다음과 같습니다.</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">```</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">DatetimeIndex(['2024-12-31', '2025-12-31', '2026-12-31', '2027-12-31',</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">'2028-12-31', '2029-12-31', '2030-12-31', '2031-12-31',</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">'2032-12-31', '2033-12-31', '2034-12-31'],</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">dtype='datetime64[ns]', freq='A-DEC')</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">```</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">### rolling()</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">rolling 함수는 지정한 기간만큼의 데이터를 하나의 컨텍스트로 묶어 계산하거나 분석할 수 있도록 도와줍니다.</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">```python</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">df[&quot;ma7&quot;] = df['Temp'].rolling(7).mean()</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">df.head(20)</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">```</td>
<td align="left"></td>
</tr>
<tr>
<td align="left">위 코드의 출력 결과는 다음과 같습니다.</td>
<td align="left"></td>
</tr>
</tbody></table>
<p><img src="https://velog.velcdn.com/images/1113mj/post/35621897-d4b0-40e7-9b86-69108bad08eb/image.png" width="200" />
 전의 데이터가 부족하면 NaN값을 출력합니다. 위 사진을 보면 0 ~ 5번까지는 데이터가 부족하여 NaN값을 출력하는 것을 볼 수 있습니다.</p>
<h3 id="shift">shift()</h3>
<p> shift 함수는 행 데이터를 옮길 때 사용하는 함수입니다. </p>
<pre><code class="language-python"> df['Time Shift1'] = df['Temp'].shift(1)
df.head()</code></pre>
<p> 위 코드를 실행한 결과는 다음과 같습니다.
<img src="https://velog.velcdn.com/images/1113mj/post/05f958ae-5d5e-45d4-b021-d2e227835f73/image.png" width="300" />
위 사진을 보시면 <code>Temp Shift1</code>은 <code>Temp</code>에서 하나씩 아래의 열로 이동되는 것을 볼 수 있습니다.</p>