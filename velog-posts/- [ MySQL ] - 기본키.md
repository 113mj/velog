<p>저번에 사용한 <code>dogs3</code> 테이블의 정보를 확인하면 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/e07f10fa-450e-418a-a910-f1752fa155a2/image.png" />
이번에 저희가 볼 부분은 <code>Key</code> 컬럼 입니다. 이에 대해 알아보기전 <code>dogs</code> 테이블에 여러 개의 데이터를 넣어보겠습니다.</p>
<pre><code class="language-sql">INSERT INTO dogs VALUES (&quot;unnamed&quot;, 99);
INSERT INTO dogs VALUES (&quot;unnamed&quot;, 99);
INSERT INTO dogs VALUES (&quot;unnamed&quot;, 99);
INSERT INTO dogs VALUES (&quot;unnamed&quot;, 99);
INSERT INTO dogs VALUES (&quot;unnamed&quot;, 99);
INSERT INTO dogs VALUES (&quot;unnamed&quot;, 99);
INSERT INTO dogs VALUES (&quot;unnamed&quot;, 99);</code></pre>
<p>위 코드를 실행한 뒤 테이블을 조회하면 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/1ccf10aa-9004-4638-82bc-aa30dff7eab3/image.png" />
위 데이터를 보면 강아지에 대한 정보가 많이 들어 있지만 <code>unnamed</code> 라는 강아지가 전부 다른 강아지라면 각 강아지를 구별할 방법이 없습니다.
따라서 모든 강아지에 대해 고유한 값을 부여해서 서로가 다르다는 것을 구분하게 해야합니다. 이 때 사용하는 것이 <code>Key</code> 입니다.</p>
<p>다음과 같은 코드를 작성하여 <code>Key</code> 기능을 추가한 테이블을 생성하겠습니다.</p>
<pre><code class="language-sql">CREATE TABLE dogs4 (
    dog_id INT NOT NULL,
    name VARCHAR(50),
    age INT
);
</code></pre>
<p>이렇게 생성된 <code>dogs4</code> 테이블은 데이터를 삽입할 때마다 <code>dog_id</code>를 집어 넣어야합니다. 하지만 다음과 같은 오류가 발생합니다.</p>
<pre><code class="language-sql">INSERT INTO dogs4 VALUES(1, 'a', 1);
INSERT INTO dogs4 VALUES(2, 'a', 1);
INSERT INTO dogs4 VALUES(3, 'a', 1);
INSERT INTO dogs4 VALUES(2, 'a', 1);</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/03ea83b2-7943-4c85-8949-c84154662b81/image.png" /></p>
<p>위 사진을 보면 <code>dog_id</code> 로 구분하려고 했으나 중복으로 저장이 가능하여 구분이 불가능합니다.</p>
<h3 id="primary-key기본키">Primary Key(기본키)</h3>
<p>Primary Key는 각 행을 대표하는 Key입니다. 즉 Primary Key는 중복되지 않으며, NULL도 허용되지 않는 값입니다. 다음과 같은 코드를 작성하여 <code>PRIMARY KEY</code> 기능을 추가한 테이블을 생성하겠습니다.</p>
<pre><code class="language-sql">CREATE TABLE dog5 (
    dog_id INT NOT NULL PRIMARY KEY,
    name VARCHAR(50),
    age INT
);</code></pre>
<p>위 코드를 통해서 <code>dog_id</code> 는 <code>PRIMARY KEY</code> 기능을 갖게 되어 중복되면 않되며 NULL값이 허용되지 않는 컬럼이 되었습니다.</p>
<pre><code class="language-sql">INSERT INTO dogs5 VALUES(1, 'a', 1);
INSERT INTO dogs5 VALUES(1, 'a', 1);</code></pre>
<p>따라서 위 코드를 실행하면 다음과 같은 결과가 나옵니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/c515ac53-7f0c-4d08-929c-1fed80b91aae/image.png" /></p>
<p>첫 번째 문장의 <code>INSERT</code> 는 실행되었지만, 두 번째 <code>INSERT</code> 는 위와 같은 오류가 발생하여 삽입되지 않는 것을 확인할 수 있습니다.</p>