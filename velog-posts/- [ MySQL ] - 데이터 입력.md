<h3 id="insert">INSERT</h3>
<p><code>INSERT</code> 은 행을 삽입하는 명령어입니다. 예시 코드는 다음과 같습니다.</p>
<pre><code class="language-sql">INSERT INTO table_name(column_name, column_name)
VALUES (value_1, value_2)
</code></pre>
<p>예를 들어 다음과 같은 테이블을 생성합니다.</p>
<pre><code class="language-sql">CREATE TABLE cats (
    name VARCHAR(50),
    age INt
);</code></pre>
<p>위 <code>dog</code> 테이블에 <code>INSERT</code> 명령어를 사용하여 데이터에 값을 삽입합니다.</p>
<pre><code class="language-sql">INSERT INTO cats(name, age)
VALUES ('야옹', 3);</code></pre>
<p>위 <code>INSERT</code> 문의 컬럼 이름을 반대로 하여 입력할 수 있습니다.</p>
<pre><code class="language-sql">INSERT INTO dogs(age, name)
VALUES (5, '감자');</code></pre>
<p>컬럼 이름을 생략하여 <code>INSERT</code> 문을 사용할 수 있습니다. 대신 테이블을 생성할 때 나열한 속성 순으로 삽입합니다.</p>
<pre><code class="language-sql">INSERT INTO dogs
VALUES ('치즈', 4);</code></pre>
<p><code>INSERT</code> 문을 통해 많은 데이터를 삽입 할 수 있습니다.</p>
<pre><code class="language-sql">INSERT INTO dogs(name, age)
VALUES     ('멍멍이1', 5),
        ('멍멍이2', 4),
        ('멍멍이3', 1);
</code></pre>
<p>위 코드를 실행한 뒤 테이블을 조회하면 다음과 같은 결과가 나옵니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/3f92acd7-b0ee-4163-b650-0f8105da6b6c/image.png" /></p>
<h3 id="null-not-null">NULL, NOT NULL</h3>
<p><code>DESC</code>명령어를 통해 테이블의 정보를 확인할 수 있습니다.</p>
<pre><code class="language-sql">DESC dogs;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/1f65910a-8746-4cf2-b0d9-50bd6db9c81e/image.png" />
위 사진을 보면 NULL 컬럼에 YES로 되어 있는 것을 확인할 수 있습니다. 이 뜻은 값을 설정할 때 NULL값이 허용된다는 뜻입니다. 즉 <code>INSERT</code> 문을 실행할 때 값을 지정하지 않는다면 NULL로 저장됩니다.</p>
<pre><code class="language-sql">INSERT INTO dogs()
VALUES ()</code></pre>
<p>위 코드를 실행한 뒤 테이블을 조회하면 다음과 같은 결과가 나옵니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/1ce320bb-953d-4c57-8c4a-86e349e40a39/image.png" />
위 사진을 보시면 7번 행에 <code>name</code> 과 <code>age</code>가 NULL로 설정되어 있는 것을 확인할 수 있습니다.</p>
<p>여기서 NULL값을 허용하지 않을려면 NOT NULL 제약 조건을 설정해야합니다.</p>
<h3 id="not-null-제약조건">NOT NULL 제약조건</h3>
<p>제약 조건이란 데이터의 상태를 제약하는 조건을 말합니다. 즉 데이터를 삽입할 때 지켜야할 규칙입니다. 제약 조건을 설정한 새로운 테이블을 생성해보겠습니다.</p>
<pre><code class="language-sql">CREATE TABLE dogs2(
    name VARCHAR(50) NOT NULL,
    age INT NOT NULL
);</code></pre>
<p>위 테이블의 정보를 <code>DESC</code>명령어를 통해 확인하면 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/ac43ed32-ea1e-4540-94cf-2af3f6907369/image.png" /></p>
<p>이렇게 데이터를 생성하면 데이터 삽입을 할 때 <code>name</code> 속성 값이 NULL로 설정하면 에러가 발생합니다.</p>
<pre><code class="language-sql">INSERT INTO dogs2(age)
VALUES (20);</code></pre>
<p>위 코드를 실행하면 다음과 같은 결과가 나옵니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/8d792983-1283-47e6-8102-565b9f53a473/image.png" />
따라서 <code>dogs2</code> 테이블에 데이터를 삽입하는 방법은 두 컬럼에 대한 값을 모두 입력해야 합니다.</p>
<pre><code class="language-sql">INSERT INTO dogs2(name, age)
VALUES ('고구마',20);</code></pre>
<p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/aeeb56fe-110d-479b-a39f-febb198bd9c3/image.png" /></p>
<h3 id="default">DEFAULT</h3>
<p><code>dogs</code> 와 <code>dogs2</code> 테이블의 정보를 보면 <code>Default</code>에 NULL로 설정된 것을 확인할 수 있습니다. 이는 데이터 삽입시 아무런 정보가 없다면 기본적으로 설정될 값이 NULL로 설정된다는 것을 의미합니다. 만약 데이터 삽입시 특정 컬럼에 아무 값도 넣지 않았을 때 기본적으로 가지고 있는 값을 설정하기 위해선 <code>Default</code>를 사용하면 됩니다.</p>
<pre><code class="language-sql">CREATE TABLE dogs3 (
    name VARCHAR(50) DEFAULT &quot;강아지이름&quot;,
    age INT DEFAULT 1000
);

INSERT INTO dogs3()
VALUES ();</code></pre>
<p>위 코드를 실행한 뒤 테이블을 조회하면 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/2122f040-06b5-4134-999e-93227b13b7d0/image.png" /></p>
<p><code>INSERT</code> 문에 아무 값도 설정하지 않았지만 테이블을 생성할 때 <code>Default</code>에 쓴 값이 설정된 것을 확인할 수 있습니다.</p>