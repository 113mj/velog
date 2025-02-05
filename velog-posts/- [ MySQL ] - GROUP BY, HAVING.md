<h3 id="group-by">GROUP BY</h3>
<p><code>GROUP BY</code> 는 데이터를 요약 혹은 집계하여 하나의 열로 만들어 줍니다. 사용 예시는 다음과 같습니다.</p>
<pre><code class="language-sql">SELECT author_lname, COUNT(*) FROM books GROUP BY author_lname;</code></pre>
<p>위 코드는 <code>author_lname</code>으로 묶은 뒤 <code>author_lname</code>와 데이터 수를 출력하라는 의미입니다.
위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/0a582200-fdbb-4dfa-949f-8a629ab6dcfb/image.png" />
위 결과를 보면 <code>author_lname</code> 으로 묶인 뒤 데이터의 수를 출력된 것을 확인할 수 있습니다.
참고로 <code>GROUP BY</code> 를 사용하면 그룹별 데이터의 행의 개수는 오로지 1개라는 것을 알 수 있습니다.</p>
<h3 id="다중-group-by">다중 GROUP BY</h3>
<p><code>GROUP BY</code> 의 집계 기준은 여러 열을 대상으로 만들 수 있습니다. 그리고 그룹은 선언한 순서대로 만들어집니다. 먼저 데이터를 더 삽입하겠습니다. </p>
<pre><code class="language-sql">INSERT INTO books
    (title, author_fname, author_lname, released_year, stock_quantity, pages)
VALUES ('10% Happier', 'Dan', 'Harris', 2014, 29, 256), 
       ('fake_book', 'Freida', 'Harris', 2001, 287, 428),
       ('Lincoln In The Bardo', 'George', 'Saunders', 2017, 1000, 367);</code></pre>
<p>그리고 다음과 같이 <code>GROUP BY</code> 를 실행하겠습니다.</p>
<pre><code class="language-sql">SELECT author_fname, author_lname, COUNT(*)
FROM books
GROUP BY author_lname, author_fname;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/ad49a5d0-85fa-46a6-9926-bb2b8d061b95/image.png" />
아래에 보면 <code>author_lname</code> 이 Harris인 그룹이 두 개 생긴것을 확인할 수 있습니다. 왜냐하면 먼저 <code>author_lname</code> 로 먼저 그룹화를 한 뒤 <code>author_fname</code> 로 그룹화를 했기 때문입니다. 그래야만 Harris인 그룹이 두 개가 나옵니다. </p>
<h3 id="having">HAVING</h3>
<p><code>HAVING</code> 은 <code>GROUP BY</code> 에 의해 집계된 데이터에 대한 조건을 설정할 수 있는 기능입니다. <code>WHERE</code> 은 테이블 자체에서 조건을 통해 필터링을 하고, <code>HAVING</code> 은 집계의 결과에 대해 필터링을 합니다. 사용 예시는 다음과 같습니다.</p>
<pre><code class="language-sql">SELECT author_lname, AVG(pages)
FROM books
WHERE released_year &gt;= 2000
GROUP BY author_lname
HAVING AVG(pages) &gt;= 250;</code></pre>
<p>위 코드의 의미는 <code>released_year</code> 가 2000 이상인 데이터를 <code>author_lname</code> 으로 그룹화한 뒤 그룹의 <code>pages</code> 의 평균이 250 이상인 <code>author_lname</code> 과 <code>pages</code> 평균을 조회하는 뜻입니다.
위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/8e86e01e-8d87-4748-be68-d6790a3ed9fd/image.png" />
위 코드의 의미처럼 집계된 것을 확인할 수 있습니다.
그리고 <code>HAVING</code> 은 <code>SELECT</code> 보다 뒤에 실행되기 때문에 부여한 <code>Alias</code> 를 사용할 수 있습니다.</p>
<h3 id="with-rollup">WITH ROLLUP</h3>
<p><code>WITH ROLLUP</code> 은 <code>GROUP BY</code> 를 사용할 때, 그룹별 집계뿐만 아니라 그룹의 총합까지 함께 계산할 수 있도록 해주는 기능입니다. 즉, 그룹별 합계뿐만 아니라 전체 합계도 구할 때 유용하게 사용할 수 있습니다. 예시 코드는 다음과 같습니다. </p>
<pre><code class="language-sql">SELECT author_lname, COUNT(*)
FROM books
GROUP BY author_lname WITH ROLLUP;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/3fa04e04-a2d2-44b5-9bf3-071117545fec/image.png" />
위 사진을 보시면, 마지막 NULL은 데이터의 전체 합계입니다. 이를 통해 전체 데이터의 개수를 확인할 수 있습니다. 
<code>GROUP BY</code> 과 <code>WITH ROLLUP</code> 을 사용하면 상위 그룹에 대한 합계가 나옵니다.</p>
<pre><code class="language-sql">SELECT author_fname, author_lname, COUNT(*)
FROM books
GROUP BY author_lname, author_fname WITH ROLLUP;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/ab2edca8-00d6-4f9d-be14-2641e351d6f9/image.png" /></p>
<p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/2dad449e-46bb-423c-b40d-a46aa9cd7ba7/image.png" /></p>
<p>위 사진을 보시면 <code>author_lname</code> 이 Haris인 데이터의 합계는 2이며 <code>author_lname</code> 이 Haris이며, <code>author_fname</code> 이 Dan, Freida 인 사람의 데이터 합계가 각각 1인 것을 볼 수 있다. 이는 <code>WITH ROLLUP</code>을 사용하면 개별 그룹별 합계뿐만 아니라 상위 그룹의 합계까지도 쉽게 구할 수 있다는 것을 보여줍니다.</p>