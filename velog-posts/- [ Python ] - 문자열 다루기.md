<h3 id="문자열">문자열</h3>
<p>문자열이란 문자들이 나열된 형태의 자료형을 말합니다. 여기서 문자열은 나열된 상태이기 때문에 연속되어 있는 형태라고 말할 수 있고, 이는 즉 순서가 있다는 의미가 됩니다. 따라서 문자열은 문자들의 sequence의 형태입니다.</p>
<h3 id="index">index</h3>
<p>index는 sequence의 순번을 나타내는 숫자입니다. index의 종류는 다음과 같습니다.</p>
<ul>
<li>양수 인덱스:0부터 시작하며 왼쪽에서 오른쪽으로 1씩 증가합니다.</li>
<li>음수 인덱스: -1부터 시작하며 오른쪽에서 왼쪽으로 1씩 감소합니다.<pre><code class="language-python">text = &quot;Hello World!&quot;
print(text[6])
print(text[-3])</code></pre>
위 코드의 결과는 다음과 같습니다.<pre><code>W
l</code></pre><h3 id="슬라이싱">슬라이싱</h3>
슬라이싱은 index를 이용하여 sequence를 잘라내어 새로운 sequence를 만드는 작업을 말합니다. 슬라이싱은 다음과 같이 사용할 수 있습니다.<pre><code>[start : end : step]</code></pre>의미는 다음과 같습니다.<blockquote>
<p><code>start</code>부터 ~ <code>end-1</code>까지 부분을 <code>step</code>만큼 건너 뛰면서 잘라낸다.</p>
</blockquote>
</li>
</ul>
<pre><code class="language-python">text = &quot;Hello world!&quot;
print(text[1:3])</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>el</code></pre><p>여기서 start, end, step은 생략이 가능합니다. start를 생략하면 자동으로 0이 들어가며 end를 생략하면 자동으로 sequene의 길이가 들어갑니다. 그리고 step를 생략하면 자동으로 1이 들어갑니다.</p>
<pre><code class="language-python">text = &quot;Hello world!&quot;
print(text[::2])
print(text[1:5:])</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>Hlowrd
ello</code></pre><p>step에 음수가 들어가면 방향이 반대가 됩니다.</p>
<pre><code class="language-python">text = &quot;Hello world!&quot;
print(text[::-1])</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>!dlrow olleH</code></pre><h3 id="문자열-합치기">문자열 합치기</h3>
<p>파이썬에서 문자열을 합치는 방법은 합치고 싶은 문자열 사이에 <code>+</code>를 넣으면 됩니다.</p>
<pre><code class="language-python">text1 = &quot;Hello&quot;
text2 = &quot; World!&quot;
print(text1+ text2)</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>Hello World!</code></pre><h3 id="문자열-반복하기">문자열 반복하기</h3>
<p>파이썬에서 문자열을 반복하는 방법은 반복하고 싶은 문자열과 반복하고 싶은 횟수 사이에 <code>*</code>를 넣으면 됩니다.</p>
<pre><code class="language-python">text1 = &quot;Hello &quot;
print(text1 * 4)</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>Hello Hello Hello Hello </code></pre><h3 id="대소문자화">대/소문자화</h3>
<p>파이썬에서는 <code>upper()</code>와 <code>lower()</code>를 통해 문자열을 대/소문자화 할 수 있습니다.</p>
<pre><code class="language-python">text1 = &quot;hello&quot;
text2 = &quot;WORLD&quot;
print(text1.upper())
print(text2.lower())</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>HELLO
world</code></pre><h3 id="문자열-치환">문자열 치환</h3>
<p>파이썬에서는 <code>replace()</code>를 통해 문자열을 치환할 수 있습니다.</p>
<pre><code class="language-python">text = &quot;hello&quot;
text = text.replace(&quot;l&quot;, &quot;r&quot;)
print(text)</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>herro</code></pre><h3 id="문자열-포메팅">문자열 포메팅</h3>
<p>문자열 포매팅은 문자열 내에 특정한 값을 삽입하여 원하는 형식의 문자열을 동적으로 생성하는 기능입니다. 즉, 변수의 값을 문자열 내부의 특정 위치에 삽입할 수 있도록 도와줍니다. 다음 코드는 문자열 포메팅을 하는 코드입니다.</p>
<pre><code class="language-python">text = &quot;boy&quot;
text2 = &quot;안녕하세요 저의 성별은 {}입니다.&quot;
print(text2.format(text))</code></pre>
<pre><code class="language-python">text = &quot;boy&quot;
text3 = f&quot;안녕하세요 저의 성별은 {text}입니다.&quot;
print(text3)</code></pre>
<p>위 두 코드는 다음과 같은 결과가 나옵니다.</p>
<pre><code>안녕하세요 저의 성별은 boy입니다.</code></pre><h3 id="문자열-분리">문자열 분리</h3>
<p>파이썬에서는 <code>split()</code>를 통해 문자열을 쪼갤 수 있습니다. <code>split()</code>는 구분할 구분자를 인수로 받습니다.</p>
<pre><code class="language-python">text = &quot;안녕 반가워 나는 민수야&quot;
text = text.split(&quot; &quot;)
print(text)</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>['안녕', '반가워', '나는', '민수야']</code></pre><h3 id="문자열-합치기-1">문자열 합치기</h3>
<p><code>join()</code>은 <code>split()</code>와 반대로 특정 문자열을 기준으로 리스트에 들어있는 문자열을 합치는 함수입니다.</p>
<pre><code class="language-python">num = [&quot;one&quot;, &quot;two&quot;, &quot;three&quot;]
print(&quot; &quot;.join(num))
</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>one two three</code></pre>