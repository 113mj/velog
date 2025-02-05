<p><code>JOIN</code> 은 두 개 이상의 테이블을 묶어서 하나의 데이터로 만들어내는 기능입니다. 즉 테이블을 연결해 데이터를 조회하는 것이 <code>JOIN</code> 입니다. <code>JOIN</code> 의 종류를 하나씩 보겠습니다.</p>
<h3 id="외래키">외래키</h3>
<p><code>JOIN</code> 을 하기 위해서는 각 테이블이 관계를 가져야 합니다. 그 관계의 종류는 다음과 같습니다.</p>
<ul>
<li>1 대 1 관계: 하나의 데이터가 다른 테이블의 하나의 데이터와 관계를 맺는 것을 말합니다. 예를 들면 어느 회사에서 직급 마다 월급이 결정되어 있다면 직급과 월급은 1 대 1 관계입니다.</li>
<li>1 대 다 관계: 가장 많이 사용되는 관계로 하나의 데이터가 다른 테이블의 여러 데이터와 관계를 맺는 것을 말합니다. 예를 들어 A 부서에 속한 사람은 여러 명이지만, 한 직원이 속한 부서는 1개이므로 1 대 다 관계입니다.  </li>
<li>다 대 다 관계: 여러 데이터가 다른 테이블의 여러 데이터와 관계를 맺는 것을 말합니다. 하나의 책을 여러 명의 작가가 쓰며 한 작가가 여러 개의 책을 쓸 수 있으므로 이 두 데이터는 다 대 다 관계입니다.</li>
</ul>
<p>이러한 관계에서 테이블끼리 <code>JOIN</code> 을 하기 위해선 서로의 테이블을 참조할 수 있는 키가 필요합니다. 이러한 키를 <code>외래키</code> 라고 합니다. </p>
<p>외래키를 설정하기 위해 다음과 같이 테이블을 생성합니다.</p>
<pre><code class="language-sql">CREATE TABLE customers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    email VARCHAR(50)
);</code></pre>
<p>이후 <code>customers</code> 를 참조할 테이블을 생성합니다.</p>
<pre><code class="language-sql">CREATE TABLE orders (
    id INT PRIMARY KEY AUTO_INCREMENT,
    order_date DATE,
    amount DECIMAL(8,2),
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);</code></pre>
<p>마지막 줄에 <code>orders</code> 의 <code>customer_id</code> 가 <code>customers</code> 의 <code>id</code> 를 참조한 것을 확인할 수 있습니다. 이제 다음과 같은 데이터들을 삽입합니다.</p>
<pre><code class="language-sql">INSERT INTO customers (first_name, last_name, email) 
VALUES ('Boy', 'George', 'george@gmail.com'),
       ('George', 'Michael', 'gm@gmail.com'),
       ('David', 'Bowie', 'david@gmail.com'),
       ('Blue', 'Steele', 'blue@gmail.com'),
       ('Bette', 'Davis', 'bette@aol.com');


INSERT INTO orders (order_date, amount, customer_id)
VALUES ('2016-02-10', 99.99, 1),
       ('2017-11-11', 35.50, 1),
       ('2014-12-12', 800.67, 2),
       ('2015-01-03', 12.50, 2),
       ('1999-04-11', 450.25, 5);</code></pre>
<h3 id="join-종류">JOIN 종류</h3>
<h3 id="cross-join">CROSS JOIN</h3>
<p>Cartesian Join라고도 하는 <code>CROSS JOIN</code> 은 모든 행에대해 조인을 수행하는 연산입니다. 즉 N개의 행을 가진 테이블과 M 개의 행을 가진 테이블이 있으면, 이 행들에 대해 모두 조인을 합니다.</p>
<pre><code class="language-sql">SELECT * FROM customers, orders;</code></pre>
<p>위 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/1b1fd138-3494-454a-802c-d0731a618bc9/image.png" />
결과를 보면 <code>id</code> 가 같지 않아도 모든 행들에 대해 <code>Join</code> 연산이 수행된 것을 확인할 수 있습니다.</p>
<h3 id="inner-join">INNER JOIN</h3>
<p><code>INNER JOIN</code> 은 양쪽 모두의 테이블의 키와 매칭되는 데이터를 출력합니다. 즉 두 테이블에서 교집합인 부분이 출력된다고 생각하면 됩니다.</p>
<pre><code class="language-sql">SELECT *
FROM customers c
JOIN orders o ON c.id = o.customer_id;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/9c41abc6-fe79-49f1-84f3-e32101e9bd96/image.png" />
위 사진을 보시면 id가 같은 데이터들끼리 <code>Join</code> 이 된 것을 확인할 수 있습니다.</p>
<h3 id="left-join">LEFT JOIN</h3>
<p><code>LEFT JOIN</code> 은 기준이 되는 테이블을 왼쪽을 중심으로 오른쪽 테이블을 매치시킵니다. </p>
<pre><code class="language-sql">SELECT c.first_name, c.last_name, o.order_date, o.amount
FROM customers c
LEFT JOIN orders o ON o.customer_id = c.id;</code></pre>
<p>여기서 <code>FROM</code> 절에 위치한 테이블이 <code>LEFT</code> 테이블이 됩니다.
위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/0236e174-e2d5-43a8-863f-690a3179752c/image.png" /></p>
<h3 id="right-join">RIGHT JOIN</h3>
<p><code>RIGHT JOIN</code>은 <code>LEFT JOIN</code>과 반대로 <code>JOIN</code> 절에 위치한 테이블이 기준이 되는 연산입니다.</p>
<pre><code class="language-sql">SELECT c.first_name, c.last_name, o.order_date, o.amount
FROM orders o
RIGHT JOIN customers c ON o.customer_id = c.id;</code></pre>
<p>위 코드의 결과는 다음과 같습니다.
<img alt="" src="https://velog.velcdn.com/images/1113mj/post/bd1294c3-c1eb-4ab1-919d-bd593b56ccc9/image.png" /></p>