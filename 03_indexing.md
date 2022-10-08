# 데이터 프레임 고급 인덱싱

## 1. 인덱싱
- `인덱싱 indexing` : 데이터 프레임에서 특정한 데이터만 골라내는 것
    - 라벨 : 열 인덱싱
    - 라벨 리스트 : 복수의 열 인덱싱
    - 인덱스데이터(정수) 슬라이스 : 행 인덱싱
- Pandas는 numpy 행렬과 같은 방식의 인덱싱도 가능하다.
    - **쉼표 사용 : 행 인덱스, 열 인덱스 : 2차원 인덱싱 지원**
    - 인덱서(indexer)
        - loc : 라벨값 기반의 2차원 인덱싱
        - iloc : 순서를 나타내는 정수 기반의 2차원 인덱싱

### 1-1. 데이터프레임 생성
- 키 리스트와 값 리스트를 zip으로 묶은 후 딕셔너리로 만들기
    - dict(zip(키리스트, 값리스트))
    - 키 리스트가 열 인덱스의 라벨이 된다.
- 값 리스트를 넘파이 배열로 만든 후 전치연산하여 변환한 후 데이터 프레임으로 만들기
    - 열 인덱스와 행 인덱스 따로 지정

#### 데이터 프레임 생성

```python
col = ["x1", "x2", "x3", "x4", "x5"]
index = ["r1", "r2", "r3", "r4", "r5"]
vals = []
for i in range(5) :
    val = [np.random.randint(1, 100) for _ in range(5)]
    vals.append(val)

data = dict(zip(col, vals))
data

>>> print

{'x1': [93, 78, 27, 18, 58],
 'x2': [68, 39, 49, 75, 77],
 'x3': [49, 88, 27, 63, 7],
 'x4': [30, 84, 21, 9, 14],
 'x5': [50, 91, 40, 49, 71]}
```

- 데이터 프레임 만들기

```python
df = pd.DataFrame(data, index=index)
df
```
![03_pandas_1.png](./images/03_pandas_1.png)


### 1-2. 기본 인덱싱

#### 열 인덱싱
- 열의 라벨 : 시리즈 반환

```python
df["x1"]

>>> print

r1    93
r2    78
r3    27
r4    18
r5    58
Name: x1, dtype: int64
```

#### 열 인덱싱
- 라벨 리스트(이중리스트) : 데이터프레임 반환

```python
df[["x1", "x2"]]
```
![03_pandas_2.png](./images/03_pandas_2.png)


#### 행 인덱싱
- 인덱스데이터(정수) 슬라이스 : 데이터프레임 반환

```python
df[:2]
```
![03_pandas_3.png](./images/03_pandas_3.png)

#### 개별 데이터 선택
- 열, 행 라벨 인덱싱

```python
df["x2"]["r2"]

>>> print

39
```

## 2. loc 인덱서
- 라벨값 기반의 2차원 인덱싱
- loc 인덱서 사용
    - df.loc[행 인덱서의 값]
    - df.loc[행 인덱싱 값, 열 인덱싱 값]
    - 행 인덱싱값 : 정수 또는 행 인덱스데이터
    - 열 인덱싱값 : 라벨 문자열
- 인덱싱 값
    - 인덱스데이터
    - 인덱스데이터 슬라이스
    - 인덱스데이터 리스트
    - 같은 행 인덱스를 가지는 불리언 시리즈(행 인덱싱의 경우)
    - 또는 위의 값들을 반환하는 함수


```python
df = pd.DataFrame(np.arange(10, 22).reshape(3,4),
                 index=["a", "b", "c"],
                 columns=["A", "B", "C", "D"])
df
```
![03_pandas_4.png](./images/03_pandas_4.png)

### 2-1. 인덱싱값을 하나만 받는 경우
- loc 인덱서를 사용하여 인덱스를 하나만 넣으면 행을 선택한다.
    - 행이 시리즈로 출력된다.

```python
df.loc["a"]

>>> print

A    10
B    11
C    12
D    13
Name: a, dtype: int32
```

### 2-2. 인덱스데이터 슬라이스
- loc를 쓰지 않은 경우와 같다.

```python
df.loc["b" : "c"]
```
![03_pandas_5.png](./images/03_pandas_5.png)

```python
df["b" : "c"]
```
![03_pandas_5.png](./images/03_pandas_5.png)


### 2-3. 인덱스 데이터의 리스트
- loc를 쓰지 않으면 에러가 난다.
    - 리스트 인덱싱은 열 라벨만 가능하기때문

```python
df.loc[["b", "c"]]
```
![03_pandas_6.png](./images/03_pandas_6.png)

- loc를 쓰지 않은 경우 라벨 인덱싱은 열 인덱싱만 가능하다.

```python
df[["B", "C"]]
```
![03_pandas_7.png](./images/03_pandas_7.png)

### 2-4. 불리언 시리즈를 반환받아 인덱싱값으로 사용

```python
df.A > 15

>>> print

a    False
b    False
c     True
Name: A, dtype: bool
```

- 불리언 시리즈를 인덱싱 값으로 넣는다.

```python
df[df.A > 15]
```
![03_pandas_8.png](./images/03_pandas_8.png)

```python
df[(df.A / 2) < 8]
```
![03_pandas_9.png](./images/03_pandas_9.png)


### 2-5. 불리언 시리즈를 반환하는 함수를 인덱싱의 값으로 사용

```python
def select_df(df) :
    return df.A > 15

select_df(df)

>>> print

a    False
b    False
c     True
Name: A, dtype: bool
```

```python
df.loc[select_df(df)]
```
![03_pandas_10.png](./images/03_pandas_10.png)

### 2-6. loc를 사용하여 열 라벨 인덱싱이나 라벨 리스트 인덱싱은 불가
- loc 인덱서는 기본적으로 행 인덱스 값을 사용하기때문이다.

```python
df.loc["A"]
```

```python
df.loc[["A"]]
```

- 라벨 인덱싱과 라벨 리스트 인덱싱을 사용하려면 loc 인덱서를 뺴고 사용해야한다.

```python
df["A"]

>>> print

a    10
b    14
c    18
Name: A, dtype: int32
```

```python
df[["A"]]
```
![03_pandas_11.png](./images/03_pandas_11.png)








































