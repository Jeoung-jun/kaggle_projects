# 전처리 과정 

## 이상치 제거
---
```
- IQR을 활용한 이상치 제거
- Log transformation
```

> IQR을 활용한 이상치 제거

- 데이터의 분포가 정규분포를 이루지 않거나 한 쪽으로 skewed한 경우, IQR을 이요해서 이상치를 탑지함
- IQR = 3분위수 - 1분위수
- 이상치 판단 기준: 1분위수 - 1.5 * IQR, 3분위수 + 1.5*IQR
- 다른 이상치 제거 방법들
    - z-score
    - isolation forest
    - DBSCAN 
    - 다음의 블로그를 사용해서 공부하면 좋겠다. [이상치 관련 블로그](https://claryk.tistory.com/5)

> Log Transformation

- 로그 변환을 해야할 때
    1. 회귀 선이 (0,0)을 지나야 할 떄, 입력과 출력 모두 로그 변환이 요구된다. 
    2. 만약에 변수가 상대적인 스케일에 있을 때, 또는 퍼센트로 된 스케일에 있다면 로그 변환이 요구된다. 
    3. 변수들이 왼쪽 끝에서 0이고, 오른쪽에서는 이론적으로 임의의 큰 값을 상대적인 스케일에서 가질 떄 요구된다. 
    4. 히스토그램을 봤을 떄 왼쪽으로 치우쳐져 있는 상황에서 로그 변환을 통해서 큰 값들은 작게, 작은 값은 작은 상태를 유지하게 스케일을 변화시켜준다. 
- 주의점
    - 음수 값을 가지는 입출력 변수에 대해서 로그 변환이나, 로그-로그 모델은 적합하지 않다. 
    - log transform된 데이터 해석
    - [여러가지 함수 변환](https://seeyapangpang.tistory.com/34)
    - 다음의 블로그를 사용해서 공부해보자. [회귀분석에서 로그변환 시 계수 해석](https://danbi-ncsoft.github.io/study/2018/08/07/logwithlevel.html)


## 결측치 처리
---
```
- 문자열 데이터
- 수치 데이터
```

> 문자열 데이터 결측값 처리
---
```
#아래와 같은 방법으로 문자열 데이터만 따로 뽑아낼 수 있다. 
df.select_dtypes(exclude=[np.number])

#아래와 같은 방법으로 최빈값을 뽑아낼 수 있다. 
value = df.mode()[0]
```

## 수치 데이터 왜도 값 처리
--- 
```
왜도
Box-Cox변환
```
>왜도
- 왜도는 분포의 비대칭도를 나타내는 통계량을 의미한다. 
- 예측 변수를 활용할 떄 이러한 왜도를 보정하는 것이 또한 중요하다. 
```
from scipy.stats import skew
skew(dataframe)
```

>Box-Cox 변환
- 왜도가 높으면 Box-Cox Transformation을 사용한다. 

## 범주형 변수 변환
```
- 더미 변환(2개) -> Data Binding 이라고도함
- Label Encoding, Ordinal Encoding, One-Hot Encoding(3개 이상)
```

>더미 변환
- 간단하게 남자이면 0 여자이면 1처럼 두가지의 범주로 나누어 주는 변환 방식이다. 

>Label Encoding
- 대상 데이터: 종속변수(y)
- 0~ 클래스 개수 -1 까지 대상 레이블을 인코딩한다. x가 아니라 종속 변수인 y이어야 함이 중요하다.
>Ordinal Encoding
- 대상 데이터: 독립변수(X)
- 범주형 변수를 정수로 인코딩한다. 
- Tree 기반 알고리즘에 적용할 때  더 좋은 성능을 보여준다고 알려져있다. 
>One-Hot Encoding
- 대상 데이터: 독립변수(X)
- 범주형 변수를 0과 1의 정수 배열로 인코딩한다. 
- 선형회귀, 로지스틱 회귀, Support vector machine과 같은 non-tree기반 알고리즘이 더 좋은 성능을 보여준다고 알려져있다. 
