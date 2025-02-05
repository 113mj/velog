<p>집계 함수는 데이터를 모아서 계산하는 함수입니다. 즉 집계 함수는 각 데이터를 어떠한 기준을 통해 모아 하나의 통계적인 값으로 표현할 수 있습니다. 글에서 사용할 테이블은 저번에 사용한 <code>books</code> 테이블입니다.</p>
<h3 id="max-min">MAX, MIN</h3>
<p> <code>MAX</code> 는 최댓값, <code>MIN</code> 은 최솟값을 계산하는 함수입니다. 사용 예시는 다음과 같습니다.</p>
<pre><code class="language-sql"> SELECT MAX(pages), MIN(pages) FROM books;</code></pre>
<p> 위 코드는 <code>pages</code> 중 최댓값과 최솟값을 조회합니다.
 위 코드의 결과는 다음과 같습니다.
 <img alt="" src="https://velog.velcdn.com/images/1113mj/post/f0e4a8ac-06d7-4c08-bd0a-90021ccea241/image.png" /></p>
<h3 id="sum-avg-std">SUM, AVG, STD</h3>
<p><code>SUM</code> 은 합계, <code>AVG</code> 는 평균, <code>STD</code> 는 표준편차를 구하는 함수입니다. 사용 예시는 다음과 같습니다.</p>
<pre><code class="language-sql">SELECT SUM(pages), AVG(pages), STD(pages) FROM books;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/87462081-835f-4b01-978d-38fa26d9cc71/image.png" /></p>
<h3 id="count">COUNT</h3>
<p><code>COUNT</code> 는 NULL이 아닌 데이터의 행의 수를 세는 함수입니다. 먼저 임시로 NULL 데이터를 삽입하겠습니다.</p>
<pre><code class="language-sql">INSERT INTO books(title, pages) VALUES(NULL, NULL);</code></pre>
<p>사용 예시는 다음과 같습니다.</p>
<pre><code class="language-sql">SELECT COUNT(*), COUNT(pages), COUNT(title) FROM books;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/df29f66c-5792-46e3-b833-53e094613081/image.png" />
위 코드를 보면 NULL이 있는 행은 세어지지 않는 것을 확인할 수 있습니다.</p>