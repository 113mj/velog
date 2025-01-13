<p>NumPy는 Python에서 과학 연산을 위한 가장 기본적인 패키지 중 하나입니다.  NumPy는 데이터 분석, 데이터 처리, 선형 대수, 머신 러닝 등 다양한 분야에서 널리 사용되고 있습니다.</p>
<p>Numpy의 특징으론 다음과 같습니다.</p>
<ul>
<li>Numpy는 C언어로 구현되어 있어 연산 속도가 빠릅니다.</li>
<li>수치 연산에 관련된 방대한 라이브러리가 존재합니다. ( with scipy )</li>
<li>일반 파이썬을 이용한 수치 연산보다 훨씬 빠릅니다.</li>
<li>특히 배열 병렬 연산에 특화 되어 있습니다.</li>
</ul>
<h2 id="0-numpy-모듈-불러오기">0. numpy 모듈 불러오기</h2>
<p>numpy를 사용하기 위해서는 먼저 numpy 모듈을 불러와야 합니다. numpy 모듈을 불러오는 코드는 다음과 같습니다.</p>
<pre><code class="language-python"># numpy 모듈 불러오기
import numpy as np</code></pre>
<h2 id="1-ndarray">1. ndarray</h2>
<p><code>ndarray</code>는 Numpy에서 제공하는 다차원 배열 객체로, 동일한 데이터 타입을 가진 요소로 구성된 배열입니다.
python의 리스트를 ndarray로 만드는 과정은 다음과 같습니다.</p>
<pre><code class="language-python">py_lst = [1, 2, 3]

arr1 = np.array(py_lst) # np.array : 파이썬의 리스트를 ndarray화
arr1</code></pre>
<h2 id="2-numpy의-함수-알아보기">2. numpy의 함수 알아보기</h2>
<h3 id="1-nparange">1. np.arange()</h3>
<p><code>np.arrange()</code>는 범위 내의 일정 간격을 가진 배열을 생성하는 함수입니다. 함수의 인수로는 생성할 배열의 범위와 간격을 지정합니다. 파이썬의 range()함수와 흡사하게 사용됩니다.</p>
<pre><code class="language-python">np.arange(1, 10, 2) 
</code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>[1 3 5 7 9]</code></pre><h3 id="2-npzeros">2. np.zeros()</h3>
<p><code>np.zeros()</code>는 0으로 채워진 배열을 만들 때 사용합니다. 함수의 인수로는 shape(형상)을 입력받습니다.</p>
<pre><code class="language-python">np.zeros((3, 2))</code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>[[0. 0.]
 [0. 0.]
 [0. 0.]]</code></pre><h3 id="3-npones">3. np.ones()</h3>
<p><code>np.ones()</code>는 1로 채워진 배열을 만들 때 사용합니다. 함수의 인수로는 <code>np.zeros()</code>와 같이 shape(형상)을 입력받습니다.</p>
<pre><code class="language-python">np.ones(5)</code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>[1. 1. 1. 1. 1.]</code></pre><h3 id="4-npfull">4. np.full()</h3>
<p><code>np.full()</code>는 지정한 숫자로 배열을 만들 때 사용합니다. 함수의 인수로는 앞엔 shape, 뒤에는 채울 숫자를 입력받습니다.</p>
<pre><code class="language-python">np.full((2, 3), 7)
</code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>[[7 7 7]
 [7 7 7]]</code></pre><h3 id="5-nplinspace">5. np.linspace()</h3>
<p> <code>np.linspace()</code>는 범위 내에서 균등 간격으로 원하는 개수의 배열을 생성합니다. 인수로는 시작 값, 끝 값, 생성할 데이터 수를 받습니다.</p>
<pre><code class="language-python">np.linspace(1, 10, 3)
</code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>[ 1.   5.5 10. ]</code></pre><h3 id="6-nprandomrand">6. np.random.rand()</h3>
<p><code>np.random.rand()</code>는 0과 1 균등 분포에서 난수를 생성하여 배열을 만드는 함수입니다. 함수의 인수로는 shape를 받습니다.</p>
<pre><code class="language-python">np.random.rand(2, 3)</code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>[[0.66394392 0.03015166 0.48187234]
 [0.5854829  0.28808383 0.16924803]]</code></pre><h3 id="7-nprandomrandn">7. np.random.randn()</h3>
<p><code>np.random.randn()</code>는 평균이 0이고 표준편차가 1인 정규 분포를 따르는 난수를 생성하여 배열을 만드는 함수입니다. 함수의 인수로는 <code>np.random.rand()</code>와 같이 배열의 shape를 받습니다.</p>
<pre><code class="language-python">np.random.randn(16)</code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>[ 0.06751993  0.49481617  1.45377871  0.49295155 -0.05503713  0.43659366
 -0.43338015 -1.15205585 -0.98363672 -2.33598625  0.6001808   0.57975685
 -0.00717542 -1.27329527  1.01392436 -1.1330409 ]</code></pre><h3 id="8-nprandomuniform">8. np.random.uniform()</h3>
<p><code>np.random.uniform()</code>은  <code>np.random.rand()</code>와 비슷하게 균일 분포에서 난수를 생성하는데 사용하지만 <code>np.random.uniform()</code>은 범위를 설정하여 원하는 구간의 난수를 생성하는 함수입니다. 인수로는 시작 값, 끝 값, shape 순으로 받습니다.</p>
<pre><code class="language-python">np.random.uniform(1.0, 3.0, size = (4, 5)) </code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>[[2.55752745 1.52754581 1.53850947 2.31543273 2.14299603]
 [1.9052815  1.65771296 1.46036962 2.78939883 2.64073966]
 [2.02382006 2.29119511 1.59647249 1.76267449 2.31768143]
 [1.7015004  1.35017402 2.14816339 1.00845003 1.98943171]]</code></pre><h3 id="9-nprandomchoice">9. np.random.choice()</h3>
<p><code>np.random.choice()</code>은 0부터 (끝 값 -1)의 정수를 랜덤하게 샘플링한 배열을 복원 추출하는 함수입니다. 인수로는 끝 값, 배열의 크기로 받습니다. 비복원 추출을 하고 싶으면 인수 뒤에 <code>replace = False</code> 추가하면 됩니다.</p>
<pre><code class="language-python">np.random.choice(10, size = (2, 3)) </code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>[[2 5 1]
 [0 4 5]]</code></pre><h3 id="10-nprandomrandint">10. np.random.randint()</h3>
<p> <code>np.random.randint()</code>은 주어진 정수 범위에서 난수를 생성을 만들 때 사용하는 함수입니다. 인수로는 시작 값, 끝 값, 배열의 크기를 받습니다.</p>
<pre><code class="language-python"> np.random.randint(10, 100, size = (3, 4))</code></pre>
<p>위 코드의 출력 결과는 다음과 같습니다.</p>
<pre><code>[[90 37 66 66]
 [25 72 91 51]
 [34 36 33 26]]</code></pre>