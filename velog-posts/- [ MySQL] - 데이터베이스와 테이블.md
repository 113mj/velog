<p>앞으로 데이터베이스 시리즈에는 DBeaver툴을 사용하여 포스팅할 것입니다.</p>
<h3 id="데이터베이스-생성">데이터베이스 생성</h3>
<p>데이터베이스는 <code>CREATE DATABASE</code> 명령어를 통해 생성할 수 있습니다. 예시 코드는 다음과 같습니다.</p>
<pre><code class="language-sql">CREATE DATABASE computer_shop;
CREATE DATABASE pet_shop;</code></pre>
<h3 id="데이터베이스-삭제">데이터베이스 삭제</h3>
<p>데이터베이스는 <code>DROP DATABASE</code> 명령어를 통해 삭제할 수 있습니다. 예시 코드는 다음과 같습니다.</p>
<pre><code class="language-sql">DROP DATABASE computer_shop;</code></pre>
<h3 id="데이터베이스-사용">데이터베이스 사용</h3>
<p>데이터베이스는 <code>USE DATABASE</code> 명령어를 통해 사용할 수 있습니다. 예시 코드는 다음과 같습니다.</p>
<pre><code class="language-sql">USE DATABASE pet_shop;</code></pre>
<p>현재 사용중인 데이터베이스를 확인하고 싶다면 <code>SELECT DATABASE()</code>를 사용하면 됩니다.</p>
<pre><code class="language-sql">SELECT DATABASE();</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<p><img alt="" src="https://velog.velcdn.com/images/1113mj/post/e5842a35-57d0-42c1-80c0-eefba25934d7/image.png" /></p>
<h3 id="테이블">테이블</h3>
<p>테이블은 여러 데이터가 모여 있는 집합을 의미하며, 이러한 테이블들이 모여 하나의 데이터베이스를 구성합니다. 테이블은 특정한 형식과 구조를 정의하고, 해당 형식을 따르는 데이터의 집합을 저장하는 역할을 합니다. 데이터베이스 내에서 구조화된 형식으로 관련된 데이터를 체계적으로 관리하는 단위가 바로 테이블입니다.</p>
<h3 id="열column">열(Column)</h3>
<p>컬럼은 테이블에서 어떤 데이터가 존재하는지를 알려주는 머릿부분(Header)입니다. 대부분의 경우에 세로로 구분합니다.</p>
<h3 id="행rows">행(Rows)</h3>
<p>행은 다른 말로 레코드(Record)라고도 하며, 실제 엔트리(데이터)입니다. 대부분의 경우에 가로로 구분합니다.</p>