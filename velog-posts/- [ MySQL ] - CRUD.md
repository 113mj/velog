<h3 id="crud">CRUD</h3>
<p>CRUD는 데이터를 관리하는 기본적인 작업을 의미합니다. CRUD는 다음과 같은 의미를 갖습니다.</p>
<ul>
<li>C: Create입니다. 데이터의 생성을 의미합니다.</li>
<li>R: Read입니다. 데이터의 조회를 의미합니다.</li>
<li>U: Update입니다. 데이터의 수정을 의미합니다.</li>
<li>D: Delete입니다. 데이터의 삭제를 의미합니다.</li>
</ul>
<p>이번 포스팅에서는 전반적인 CRUD에 대해 알아보겠습니다.</p>
<h3 id="데이터-준비하기">데이터 준비하기</h3>
<p>새로운 데이터테이블을 생성하겠습니다.</p>
<pre><code class="language-sql">CREATE TABLE cats(
    cat_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    breed VARCHAR(100),
    age INT
);</code></pre>
<p>이어서 고양이 정보도 삽입하겠습니다.</p>
<pre><code class="language-sql">INSERT INTO cats(name, breed, age) 
VALUES ('Ringo', 'Tabby', 4),
       ('Cindy', 'Maine Coon', 10),
       ('Dumbledore', 'Maine Coon', 11),
       ('Egg', 'Persian', 4),
       ('Misty', 'Tabby', 13),
       ('George Michael', 'Ragdoll', 9),
       ('Jackson', 'Sphynx', 7);</code></pre>
<h3 id="select">SELECT</h3>
<p><code>SELECT</code> 문은 <code>CRUD</code>의 <code>Read</code>에 해당하며 테이블에 존재하는 데이터를 조회하는 명령어입니다. </p>
<pre><code class="language-sql">SELECT *
FROM cats;</code></pre>
<p>위 코드의 뜻을 풀어서 설명하면 다음과 같습니다.</p>
<ol>
<li><code>FROM</code> 절에는 조회 대상이 되는 테이블을 지정합니다.</li>
<li><code>SELECT *</code>의 의미는 모든 열 (<code>*</code> - ASTERISK)을 조회한다는 의미입니다.</li>
</ol>
<p>즉 <code>cats</code> 의 모든 열을 조회한다는 의미가 됩니다. 여기서 만약 원하는 컬럼만 조회하고 싶다면 다음과 같이 코드를 작성하면 됩니다.</p>
<pre><code class="language-sql">SELECT name, breed FROM cats;</code></pre>
<h3 id="where">WHERE</h3>
<p><code>WHERE</code> 문은 조건절로 불리며 데이터 검색, 삭제, 수정시 조건에 해당하는 행을 필터링하는 역할을 수행합니다.</p>
<pre><code class="language-sql">SELECT * FROM cats WHERE age = 4;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/868fbb78-4894-4942-a6b9-c774ec1a8564/image.png" />
숫자뿐만 아니라 텍스트를 통해서 검색할 수 있습니다.</p>
<pre><code class="language-sql">SELECT * FROM cats WHERE name='Ringo';</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/2828bd35-237c-411a-98c7-c9c22b30a8d1/image.png" />
참고로 문자열은 대소문자를 구분하지 못하기 때문에 <code>name = 'rINGO'</code> 로 조회해도 위 사진과 같은 결과가 나옵니다.</p>
<h3 id="alias">Alias</h3>
<p>Alias는 테이블의 이름이나 컬럼 이름 등 또 다른 이름을 붙여주는 기능입니다. 실제 컬럼의 이름이 바뀌는 것이 아닌 쿼리를 사용할 때만 사용되는 임시 이름입니다.</p>
<pre><code class="language-sql">SELECT age AS &quot;나이&quot; FROM cats;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/695567e1-692d-42e5-ad02-cf14ec265bf0/image.png" /></p>
<h3 id="update">UPDATE</h3>
<p><code>UPDATE</code> 문은 CRUD의 U에 해당합니다. 즉 데이터의 수정을 할 때 사용됩니다. <code>UPDATE</code>문의 사용 방법은 다음과 같습니다.</p>
<pre><code class="language-sql">UPDATE &lt;TABLE_NAME&gt;
SET COLUMN1=VALUE, COLUME2=VALUE
WHERE CONDITION1, CONDITION2</code></pre>
<ol>
<li><code>UPDATE</code> 구문에 수정할 데이터가 들어있는 테이블의 이름을 지정합니다.</li>
<li><code>SET</code> 구문에 컬럼의 이름과 컬럼에 수정될 값을 지정합니다. 여러 컬럼을 지정할 수 있으며 쉼표(,)로 구분합니다.</li>
<li><code>WHERE</code> 구문을 이용해 조건에 맞는 행에 대해서만 수정하게 할 수 있습니다. <code>WHERE</code>구문을 지정하지 않으면 모든 데이터가 수정되기 때문에 주의해야 합니다.</li>
</ol>
<p>예를 들어 <code>breed</code>가 <code>Tabby</code>인 고양이의 나이를 -1로 수정하고 싶다면 다음과 같이 쿼리를 작성하면 됩니다.</p>
<pre><code class="language-sql">UPDATE cats
SET age=-1
WHERE breed='Tabby';</code></pre>
<p>위 코드를 실행한 뒤 데이터를 조회한 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/16928c12-111a-4f9b-858a-67126daaa700/image.png" /></p>
<h3 id="delete">DELETE</h3>
<p><code>DELETE</code> 문은 CRUD의 D에 해당하며, 데이터를 삭제할 때 사용합니다. <code>DELETE</code> 문의 사용 방법은 다음과 같습니다.</p>
<pre><code class="language-sql">DELETE FROM &lt;TABLE_NAME&gt; WHERE CONDITION1, CONDITION2</code></pre>
<p><code>SELECT</code> 문과 다르게 컬럼을 선택하는 부분이 없습니다. 즉 <code>DELETE</code> 문은 컬럼이 아닌 행을 삭제하는 개념입니다. </p>
<pre><code class="language-sql">DELETE
FROM cats
WHERE age = 4;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/593bd3fd-96bb-42a8-b61f-ba541e945dac/image.png" />
위 사진을 보면 나이가 4인 고양이의 행이 사라진 것을 확인할 수 있습니다.</p>