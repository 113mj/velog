<h3 id="문제-설명">문제 설명</h3>
<p>다음은 어느 자동차 대여 회사에서 대여중인 자동차들의 정보를 담은 <code>CAR_RENTAL_COMPANY_CAR</code> 테이블입니다. <code>CAR_RENTAL_COMPANY_CAR</code>테이블은 아래와 같은 구조로 되어있으며, <code>CAR_ID</code>, <code>CAR_TYPE</code>, <code>DAILY_FEE</code>, <code>OPTIONS</code> 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.</p>
<p>자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(옵션 리스트 값 예시: '열선시트', '스마트키', '주차감지센서')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.</p>
<h3 id="문제">문제</h3>
<p><code>CAR_RENTAL_COMPANY_CAR</code> 테이블에서 '통풍시트', '열선시트', '가죽시트' 중 하나 이상의 옵션이 포함된 자동차가 자동차 종류 별로 몇 대인지 출력하는 SQL문을 작성해주세요. 이때 자동차 수에 대한 컬럼명은 <code>CARS</code>로 지정하고, 결과는 자동차 종류를 기준으로 오름차순 정렬해주세요.</p>
<h3 id="테이블-구조">테이블 구조</h3>
<p>CAR_RENTAL_COMPANY_CAR</p>
<table>
<thead>
<tr>
<th>Column name</th>
<th>Type</th>
<th>Nullable</th>
</tr>
</thead>
<tbody><tr>
<td>CAR_ID</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>CAR_TYPE</td>
<td>VARCHAR(255)</td>
<td>FALSE</td>
</tr>
<tr>
<td>DAILY_FEE</td>
<td>INTEGER</td>
<td>FALSE</td>
</tr>
<tr>
<td>OPTIONS</td>
<td>VARCHAR(255)</td>
<td>FALSE</td>
</tr>
</tbody></table>
<h3 id="풀이-과정">풀이 과정</h3>
<p>자동차 종류별로 차량 수를 구해야 하므로 <code>GROUP BY</code>를 사용합니다. 또한, 특정 옵션(가죽시트, 열선시트, 통풍시트)이 포함된 차량만 필터링해야 하므로 <code>LIKE</code> 조건을 활용합니다. 이때, 하나의 옵션이라도 포함된 경우를 찾아야 하므로 <code>OR</code> 연산자를 사용합니다. 이후, 필터링된 차량을 종류별로 집계하기 위해 <code>COUNT</code> 함수를 적용하고, 결과를 자동차 종류 기준으로 정렬하기 위해 <code>ORDER BY</code>를 사용합니다.</p>
<h3 id="정답">정답</h3>
<pre><code class="language-sql">SELECT
    CAR_TYPE,
    count(*) as CARS
from CAR_RENTAL_COMPANY_CAR
where OPTIONS like '%가죽시트%'
or OPTIONS like '%열선시트%'
or OPTIONS like '%통풍시트%'
group by CAR_TYPE
order by CAR_TYPE</code></pre>