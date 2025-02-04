<p>문자열 함수는 텍스트 열에서 다양한 연산을 수행할 수 있도록 해줍니다. 따라서 MySQL에서는 문자열 함수를 활용하여 데이터를 조회할 때 여러 방식으로 표현할 수 있습니다. 먼저 포스팅에 쓸 데이터와 테이블을 선언하겠습니다.</p>
<pre><code class="language-sql">CREATE TABLE books 
    (
        book_id INT NOT NULL AUTO_INCREMENT,
        title VARCHAR(100),
        author_fname VARCHAR(100),
        author_lname VARCHAR(100),
        released_year INT,
        stock_quantity INT,
        pages INT,
        PRIMARY KEY(book_id)
    );

INSERT INTO books (title, author_fname, author_lname, released_year, stock_quantity, pages)
VALUES
('The Namesake', 'Jhumpa', 'Lahiri', 2003, 32, 291),
('Norse Mythology', 'Neil', 'Gaiman',2016, 43, 304),
('American Gods', 'Neil', 'Gaiman', 2001, 12, 465),
('Interpreter of Maladies', 'Jhumpa', 'Lahiri', 1996, 97, 198),
('A Hologram for the King: A Novel', 'Dave', 'Eggers', 2012, 154, 352),
('The Circle', 'Dave', 'Eggers', 2013, 26, 504),
('The Amazing Adventures of Kavalier &amp; Clay', 'Michael', 'Chabon', 2000, 68, 634),
('Just Kids', 'Patti', 'Smith', 2010, 55, 304),
('A Heartbreaking Work of Staggering Genius', 'Dave', 'Eggers', 2001, 104, 437),
('Coraline', 'Neil', 'Gaiman', 2003, 100, 208),
('What We Talk About When We Talk About Love: Stories', 'Raymond', 'Carver', 1981, 23, 176),
(&quot;Where I'm Calling From: Selected Stories&quot;, 'Raymond', 'Carver', 1989, 12, 526),
('White Noise', 'Don', 'DeLillo', 1985, 49, 320),
('Cannery Row', 'John', 'Steinbeck', 1945, 95, 181),
('Oblivion: Stories', 'David', 'Foster Wallace', 2004, 172, 329),
('Consider the Lobster', 'David', 'Foster Wallace', 2005, 92, 343);</code></pre>
<h3 id="concat">CONCAT</h3>
<p><code>CONCAT</code> 는 문자열을 연결하거나 결합하는 함수입니다.</p>
<pre><code class="language-sql">SELECT CONCAT(author_fname, ' ', author_lname) as full_name FROM books;</code></pre>
<p>위 코드는 <code>author_fname</code> 과 <code>author_lname</code> 의 문자열을 합치는 코드입니다.
코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/cb86658f-89e6-44d7-89e8-75209764dcfd/image.png" /></p>
<h3 id="concat_ws">CONCAT_WS</h3>
<p><code>CONCAT_WS</code> 는 문자열 사이에 구분자를 넣어 합치는 함수입니다.</p>
<pre><code class="language-sql">SELECT CONCAT(title,'-', author_fname,'-', released_year) FROM books;</code></pre>
<p>위 코드는 <code>title</code>, <code>author_fname</code>, <code>released_year</code> 사이에 '-'를 넣어 합치는 코드입니다.
코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/ded6f5b5-5df2-429c-b6bd-207746849605/image.png" /></p>
<h3 id="substring">SUBSTRING</h3>
<p><code>SUBSTRING</code> 은 문자열에서 원하는 부분을 잘라낼 때 사용되는 함수입니다. 파이썬의 슬라이싱과 유사합니다.
하지만 파이썬과 다르게 인덱스는 0번이 아닌 1번부터 시작합니다. <code>SUBSTRING</code> 을 사용하는 방법은 다음과 같습니다.</p>
<pre><code class="language-sql">SUBSTRING(문자열, 시작인덱스, 문자 개수)</code></pre>
<pre><code class="language-sql">SELECT SUBSTRING('HELLO', 2, 3);</code></pre>
<p>위 코드는 'HELLO'에서 인덱스 2번부터 3글자를 출력한다는 의미입니다. 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/4aadbb18-51ce-4318-b197-1d753f426d09/image.png" /></p>
<p>그리고 문자 개수를 지정하지 않으면 제일 끝에 있는 문자까지를 추출합니다.</p>
<pre><code class="language-sql">SELECT SUBSTRING('HELLO', 2);</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/356e1359-028a-40d8-95c2-911188885376/image.png" /></p>
<h3 id="replace">REPLACE</h3>
<p><code>REPLACE</code> 는 문자열을 치환할 때 사용하는 함수입니다. 사용 방법은 다음과 같습니다.</p>
<pre><code class="language-sql">REPLACE(원본 문자열, 바꿀 문자열, 바뀔 문자열)</code></pre>
<pre><code>SELECT REPLACE(title, ' ', '-') FROM books;</code></pre><p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/c7020615-af9c-4c3b-b2f7-a0c3623dcdef/image.png" /></p>
<h3 id="char_length-length">CHAR_LENGTH, LENGTH</h3>
<p><code>CHAR_LENGTH</code> 와 <code>LENGTH</code> 는 문자열의 길이를 잴 때 사용됩니다. 두 함수 모두 영어 문자열에 사용할 땐 같은 값이 나오지만 다른 언어를 사용할 때 다르게 나옵니다. <code>LENGTH</code> 는 문자열의 바이트 수를 반환하는 함수이며 <code>CHAR_LENGTH</code>는 문자열의 문자 개수를 반환하는 함수입니다.</p>
<pre><code class="language-sql">SELECT LENGTH(&quot;민수&quot;), CHAR_LENGTH(&quot;민수&quot;);</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/e5a9c98d-0f98-4abc-b882-4ef2c4cdee46/image.png" />
위 결과를 보면 <code>LENGTH</code>은 문자열의 바이트 수인 6이 출력되며 <code>CHAR_LENGTH</code> 은 문자열의 문자 개수인 2가 출력됩니다.</p>
<h3 id="upper-lower">UPPER, LOWER</h3>
<p><code>UPPER</code> 와 <code>LOWER</code> 는 각각 대문자, 소문자로 문자열을 변한하는 함수입니다. </p>
<pre><code class="language-sql">SELECT UPPER(author_fname), LOWER(author_fname) FROM books;</code></pre>
<p>위 함수의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/e915bef6-fac4-4b8d-95d2-f7a2b18783f4/image.png" /></p>