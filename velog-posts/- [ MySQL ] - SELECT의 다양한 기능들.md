<p><code>SELECT</code> 에서는 문자열 함수 외에 다양한 기능을 제공하는 함수들이 있습니다. 포스팅을 위해 테이블을 생성하겠습니다.</p>
<pre><code class="language-sql">CREATE TABLE user(
    user_id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    address VARCHAR(100) 
);</code></pre>
<p>그리고 데이터들을 테이블에 삽입하겠습니다.</p>
<pre><code class="language-sql">INSERT INTO user(username, address) 
VALUES ('A', '서울'),
             ('B', '대전'),
             ('C', '경기도'),
           ('D', NULL),
             ('E', NULL),
             ('F', '서울'),
             ('G', '경기도'),
             ('H', '대구'),
             ('I', '부산'),
             ('J', '전주'),
             ('K', '광주');</code></pre>
<h3 id="isnull">ISNULL</h3>
<p><code>ISNULL</code> 은 값이 <code>NULL</code>이면 1, 아니면 0을 반환하는 함수입니다. <code>ISNULL</code> 은 다음과 같이 사용합니다.</p>
<pre><code class="language-sql">SELECT address, ISNULL(address) FROM user;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/d093f880-b73d-4ef1-92b4-72e72393534d/image.png" />
<code>address</code> 에서 값이 <code>NULL</code> 이면 1 아니면 0이 반환되는 것을 확인할 수 있습니다.</p>
<h3 id="ifnull">IFNULL</h3>
<p><code>IFNULL</code> 은 값이 <code>NULL</code>이면 <code>NULL</code> 을 대신 다른 값으로 표현하는 함수입니다.</p>
<pre><code class="language-sql">SELECT username, IFNULL(address, '주소없음') FROM user;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/b0cf57ee-077c-4439-b7bf-9b45a7c7dd7d/image.png" />
값이 <code>NULL</code> 인 경우는 <code>주소없음</code> 으로 다른 값이 대체된 것을 확인할 수 있습니다.</p>
<h3 id="if">IF</h3>
<p><code>IF</code> 는 조건식을 통해 값을 표현할 때 사용하는 함수입니다.</p>
<pre><code class="language-sql">SELECT address, IF(address='경기도' OR address='서울', '수도권', '지방') AS region FROM user;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/bec2528f-302f-45c5-856e-45a7c0b87f69/image.png" /></p>
<p>위 사진과 코드를 보면 <code>address</code> 가 경기도 혹은 서울인 경우 수도권을, 아니면 지방으로 값이 설정되어 출력이 된 것을 확인할 수 있습니다.</p>
<h3 id="case-when-then">CASE WHEN THEN</h3>
<p><code>CASE WHEN THEN</code> 은 여러 조건의 표현식을 구현할 때 사용하는 함수입니다. <code>IF</code> 문으로 표현이 가능하나 쿼리가 복잡해지기 때문에 조건식이 여러 개일 경우에 <code>CASE WHEN THEN</code> 을 사용합니다.</p>
<pre><code class="language-sql">SELECT 
    stock_quantity,
    CASE
        WHEN stock_quantity &gt;= 50 THEN '재고 많음'
        WHEN stock_quantity &gt;= 30 THEN '재고 중간'
        ELSE '재고 부족'
    END AS 'quantity_level'</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/113b9a5d-c3ee-49e5-8dc4-95d018e11684/image.png" /></p>
<h3 id="distinct">DISTINCT</h3>
<p><code>DISTINCT</code> 은 중복된 데이터를 제거해줍니다. </p>
<pre><code class="language-sql">SELECT author_lname FROM books;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/76d1e3ae-b522-47d7-85bd-7cb2c179f7df/image.png" />
위 코드는 중복을 제거하지 않은 채 검색한 결과입니다.</p>
<pre><code class="language-sql">SELECT DISTINCT author_lname FROM books;</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/f7411faa-1d68-4e64-92a9-1eec08b237eb/image.png" />
위 코드는 중복을 제거한 결과입니다. 두 결과를 비교하시면 중복이 제거가 된 것을 확인할 수 있습니다.</p>
<h3 id="order-by">ORDER BY</h3>
<p><code>ORDER BY</code> 는 데이터를 정렬할 때 사용하는 기능입니다. 원래 데이터베이스에서 데이터가 정렬되는 기준은 삽입된 순서이지만 <code>ORDER BY</code> 를 통해 원하는 기준대로 데이터를 정렬할 수 있습니다.</p>
<pre><code class="language-sql">SELECT book_id, title, pages FROM books ORDER BY pages ASC;</code></pre>
<p>위 코드는 <code>pages</code>속성을 오름차순으로 정렬하여 <code>book_id</code>, <code>title</code>, <code>pages</code> 를 조회합니다. 위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/b37c393a-72a4-4a26-8ffb-d00329ffd8ac/image.png" />
위 사진을 보면 <code>pages</code> 를 기준으로 데이터가 정렬된 것을 확인할 수 있습니다.
만약 내림차순으로 확인하고 싶다면 <code>ASC</code> 대신 <code>DESC</code> 를 사용하면 됩니다.</p>
<pre><code class="language-sql">SELECT book_id, title, pages FROM books ORDER BY pages DESC;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/4ad26f93-9314-4b00-ba7f-d734ef0ac414/image.png" /></p>
<p>두 개 이상의 컬럼을 기준으로 데이터를 정렬할 수 있습니다.</p>
<pre><code class="language-sql">SELECT author_fname, title, pages FROM books ORDER BY author_fname ASC, pages DESC;</code></pre>
<p>위 코드의 의미는 <code>author_fname</code> 은 오름차순으로, <code>pages</code> 은 내림차순으로 정렬하는 코드입니다.
위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/4faad4c1-c038-4c9f-8e98-0851bc12761d/image.png" /></p>
<h3 id="limit">LIMIT</h3>
<p><code>LIMIT</code> 은 데이터를 조회할 때 지정한 일부만 볼 때 사용하는 기능입니다.</p>
<pre><code class="language-sql">SELECT book_id, title, author_lname FROM books LIMIT 10;</code></pre>
<p>위 코드는 첫 번째부터 10개의 데이터를 보는 코드입니다.
위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/d3ec7b4c-2d56-40c7-ac45-c832fd51ef09/image.png" />
만약 세 번째 부터 7개의 데이터를 조회하려면 <code>LIMIT</code> 에 범위를 지정하면 됩니다.</p>
<pre><code class="language-sql">SELECT book_id, title, author_lname FROM books LIMIT 2, 7;</code></pre>
<p>위 코드의 결과는 다음과 같습니다
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/b887af10-b0ee-4c6d-9119-51e1489796a5/image.png" /></p>