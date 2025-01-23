<h3 id="변수">변수</h3>
<p>변수란 값이 저장될 수 있는 공간을 말한다. 변수는 원할때 마다 <code>값</code>을 변경 및 저장을 할 수 있다.</p>
<pre><code class="language-python">a = 1</code></pre>
<p>위 코드는 다음과 같이 해석할 수 있다.</p>
<ol>
<li>a라는 변수를 선언했다.</li>
<li>변수 a에 1이라는 값을 저장했다.</li>
</ol>
<h3 id="자료형data-type">자료형(Data Type)</h3>
<p>파이썬은 기본적으로 4가지 자료형을 가지고 있습니다.</p>
<ul>
<li>int(Integer - 정수) : -1, 3, 0과 같이 정수를 나타내는 자료형입니다.</li>
<li>float - 실수 : 3.14, -6.1, 3.0과 같이 실수를 나타내는 자료형입니다. 여기서 3.0은 실수입니다.</li>
<li>str(String - 문자열) : 문자들이 열거되어 있는 자료형입니다. 문자열을 생성할 때는 &quot;&quot;나 ''를 사용합니다.</li>
<li>bool(Boolean - 논리): 참(True)/거짓(False)을 나타내는 자료형입니다.</li>
</ul>
<pre><code class="language-python">a = 3
b = 3.0
c = 3.14123
d = &quot;hello&quot;
e = 2 &lt; 3

print(type(a))
print(type(b))
print(type(c))
print(type(d))
print(type(e))</code></pre>
<p>위 코드의 결과는 다음과 같습니다.</p>
<pre><code>&lt;class 'int'&gt;
&lt;class 'float'&gt;
&lt;class 'float'&gt;
&lt;class 'str'&gt;
&lt;class 'bool'&gt;</code></pre>