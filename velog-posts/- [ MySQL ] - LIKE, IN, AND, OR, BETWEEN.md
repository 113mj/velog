<h3 id="like">LIKE</h3>
<p><code>LIKE</code> 는 문자열을 이용해 데이터를 필터링 할 때 사용할 수 있는 연산입니다. <code>LIKE</code> 는 문자열 중 일부가 같으면 조회하는 기능을 갖고 있습니다. 여기서 <code>LIKE</code> 는 와일드 카드라는 기능을 사용합니다.</p>
<h3 id="와일드카드">와일드카드</h3>
<p>와일드카드는 대표적으로 <code>%</code> 와 <code>_</code> 가 있습니다. 두 가지의 의미는 다음과 같습니다.</p>
<ul>
<li>% : 0개 이상의 문자를 대체합니다.</li>
<li>_ : 한 개의 문자를 대체합니다.</li>
</ul>
<p>예를 들면 <code>W%</code> 는 W로 시작하는 문자열을 의미하며, <code>_W</code>는 W로 끝나는 두 글자의 문자열을 의미합니다.</p>
<pre><code class="language-sql">SELECT title FROM books WHERE title LIKE 'Wh%';</code></pre>
<p>위 코드는 <code>title</code> 중 wh로 시작하는 제목을 출력하는 뜻입니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/9d02f927-54b9-4af3-8d95-bda3075ce75b/image.png" />
위 사진을 보면 wh로 시작하는 제목을 출력한 것을 확인할 수 있습니다.</p>
<pre><code class="language-sql">select author_fname from books where author_fname like '_a___';</code></pre>
<p>위 코드는 <code>author_fname</code> 가 5글자이며 두 번째 글자가 a인 값을 출력하는 뜻입니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/658bc414-2682-4e8c-a881-66e9a1f19d90/image.png" />
위 사진을 보면 글자 수가 5개이며 두 번째 글자가 a인 <code>author_fname</code> 를 출력하는 것을 확인할 수 있습니다.</p>
<h3 id="in">IN</h3>
<p><code>IN</code> 은 여러 개의 값 중에서 특정한 값이 존재하는지 확일할 때 사용하는 연산입니다.</p>
<pre><code class="language-sql">SELECT title, author_lname FROM books WHERE author_lname IN ('Lahiri', 'Gaiman');</code></pre>
<p>위 코드는 <code>author_lname</code> 이 'Lahiri'거나 'Gaiman'인 사람의 <code>title</code> 과 <code>author_lname</code> 을 출력하는 의미입니다.
위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/54a6f36b-1d90-4314-8099-71cf9e62dc34/image.png" /></p>
<h3 id="and-or">AND, OR</h3>
<p><code>AND</code> 연산은 모든 조건이 참일 경우에 True가 되는 논리 연산이며 <code>OR</code> 은 모든 존건 중 하나만 참일 경우 True가 되는 연산입니다. 참고로 두 연산을 같이 사용할 때는 우선적으로 처리해야할 조건에 괄호를 사용하는 것이 좋습니다. 왜냐하면 <code>AND</code> 연산이 <code>OR</code> 연산보다 우선순위를 갖고 있기 때문입니다. 두 연산을 사용하는 방법은 다음과 같습니다.</p>
<pre><code class="language-sql">SELECT title, author_lname, released_year, pages
             FROM books
       WHERE ( author_lname LIKE 'L%' OR pages &lt;= 300) AND released_year &lt; 2000;</code></pre>
<p>위 코드의 의미는 <code>author_lname</code> 의 첫 글자가 L이거나 <code>pages</code>가 300 이하면서 <code>released_year</code> 가 2000보다 낮은 행의 <code>title</code>, <code>author_lname</code>, <code>released_year</code>, <code>pages</code> 를 조회하는 의미입니다.
위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/11702510-2e4a-4fab-a7fa-fb088dff3961/image.png" /></p>
<h3 id="between">BETWEEN</h3>
<p><code>BETWEEN</code> 은 같은 컬럼에 대해 크기를 비교할 때 사용하는 연산입니다. </p>
<pre><code class="language-sql">SELECT title, released_year FROM books WHERE released_year BETWEEN 2004 AND 2015;</code></pre>
<p>위 코드는 <code>released_year</code>가 2004 이상 2015 이하인 행의 <code>title</code>, <code>released_year</code> 를 출력합니다. 위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/4e3cb372-ea42-4f0a-9480-d072e3af2ee7/image.png" /></p>