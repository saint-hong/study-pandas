# study-pandas
summary pandas

# 01_basic_series_dataframe
### 시리즈
- 시리즈 생성
   - pd.Series([value, value, value], index=["label", "label", "label"])
- index, values 조회
   - s.index
   - s.values
- 이름 붙이기
   - s.name
   - s.index.name
- 시리즈 연산
- 시리즈 인덱싱
   - 열 인덱싱
      - s["열라벨"] : 열 인덱싱
      - s[정수] : 열 인덱싱
   - 배열 인덱싱
      - s[[1, 2, 3]]
      - s[["서울", "대구"]]
- 불리언 값을 사용하여 인덱싱
   - s[(250e < s)]
- 슬라이싱
   - s[1:3]
   - s["서울":"인천"]
- 시리즈와 딕셔너리 자료형
   - 딕셔너리 객체를 사용하여 시리즈 생성
- 인덱스 기반 연산

### 데이터프레임
- 데이터의 갱신, 추가, 삭제
- 데이터프레임
   - 생성
   - df.values
   - df.columns
   - df.index
- 행, 열 인덱스 이름 설정
   - df.index.name
   - df.columns.name
- 데이터프레임 전치하기
   - df.T
- 열 인덱스 갱신, 추가, 삭제   

### 데이터프레임 인덱싱
- 열 인덱싱
   - 열 라벨이 키 값
   - 인덱싱 방법에 따라서 반환되는 형태가 다름
   - 시리즈, 데이터프레임
- 행 인덱싱
   - 행 인덱싱은 항상 슬라이싱 기호 사용
   - 기본적으로 행의 정수 인덱스 사용
- 개별 데이터 인덱싱
- 열 라벨 리스트에 리스트
   - df[["col1", "col2"]]
- 정수 인덱싱 = 행 인덱싱 = 데이터 프레임

# 02_data_input_output

### 데이터 입력
- %%writefile
   - 텍스트 파일 만드는 명령
- csv 파일 입력
   - pd.read_csv("파일명", encoding="")
- 열 인덱스가 따로 없는 경우
   - 첫번째 행이 열 라벨이 됨
- names 인수사용하여 열 인덱스 설정
   - pd.read_csv("sample.csv", names=["col1", "col2"])
- 행 인덱스 지정
   - pd.read_csv("sample.csv", index_col="col1")
- 구분자 지정
   - 정규표현식 사용하여 구분자를 지정
   - pd.read_csv("sample.csv", sep="/s+"
- 행 건너뛰기
   - pd.read_csv("sample.csv", skiprows=[0, 1])
- nan 값 바꾸기
   - pd.read_csv("sample.csv", na_values=["누락"])

### 데이터 출력
- df.to_csv("sample.csv")
- 파일 내용 확인
   - 윈도우 : !type 파일명
   - 맥, 리눅스 : !cat 파일명
- 구분자 변경하기
   - df.to_csv("sample.csv", sep="/")
- nan 값 변경하여 저장하기
   - df.to_csv("sample.csv", na_rap="누락")
- index, header 출력 여부 지정
   - 파일을 불러올 때 출력할지 말지 여부 설정
   - df.to_csv("sample.csv", index=False, header=False)
- 인터넷 상의 csv 파일 입력
   - pd.read_csv("url 주소")
- 행의 디스플레이 갯수 설정
   - pd.set_option("display.max_rows", 5)
- head, tail
   - df.head(int), df.tail(int)
- 인터넷상의 데이터 베이스 자료 입력

# 03_indexing

### 인덱싱
- 열 인덱싱
   - 열의 라벨 : 시리즈 반환
   - 라벨 리스트(이중리스트) : 데이터프레임 반환
- 행 인덱싱
   - 인덱스데이터(정수) 슬라이스 : 데이터프레임 반환
- 개별데이터 선택
   - df["열 라벨"]["행 라벨"]
- loc 인덱서
   - 행의 라벨값 기반의 2차원 인덱싱
- iloc 인덱서
   - 순서를 나타내는 정수 인덱스를 사용한 인덱싱

# 04_data_transform
### 데이터 갯수 세기
- count()
- value_counts()

### 정렬
- 행 인덱스 기준 정렬
   - sort_index()
- 데이터 기준 정렬
   - sort_values()
- 내림차순 정렬
   - sort_values(ascending=False)
- 데이터 프레임에서 정렬
   - df.sort_values(by="col2")
   - df.sort_values(by=["col1", "col2"])
   
### 행, 열 합계
- sum()
   - axis=0 : 열 단위 합 : 0=행이 없어진다는 의미
   - axis=1 : 행 단위 합 : 1=열이 없어진다는 의미
- mean()
- apply() 변환
   - df.apply(lambda x : x.max() - x.min(), axis=1)
   - 계산해서 없어지는 열을 axis의 값으로 설정
   - 열 라벨 사용시 axis=1 설정
- 각 열별 데이터 갯수 계산
   - df.apply(pd.value_counts())
- 람다함수에 조건문 추가
- 결측 데이터 변환
   - df.fillna()
- 자료형 변경
   - df.astype(int)
   - df.age.astype(int)
- 카테고리 값 변환
   - pd.cut(data, bins=, labels=)
   - pd.qcut(data, 구간갯수, labels=)

# 05_index_transform
### 데이터프레임 인덱스 설정 및 제거
- 열을 인덱스로 설정
   - df.set_index("col1")
- 인덱스를 열로 설정
   - df.reset_index() : 인덱스를 열로 변환
   - df.reset_index(drop=True) : 기존 인덱스 삭제하고 정수 인덱스 설정
- 다중인덱스
   - columns=[[], []]
   - index=[[], []]
- 다중인덱스 이름지정
   - columns.names = ["열이름1", "열이름2"]
   - index.names = ["인덱스 이름1", "인덱스 이름2"]
- 다중 인덱스 선택하기
   - loc 인덱서 사용

### 행, 열 인덱스 교환
- 열 인덱스를 행 인덱스로 교환
   - df.stack("열라벨")
- 행 인덱스를 열 인덱스로 교환
   - df.unstack("행라벨")
   - df.unstack(0)

### 다중 인덱스의 인덱싱
- 리스트 안에 튜플 사용
   - df[("상위열라벨", "하위열라벨")]
- loc 인덱서 사용
   - 라벨값 사용
   - df.loc["행라벨", ("열라벨", "열라벨")]
   - df.loc[("행라벨" "행라벨"), ("열라벨", "열라벨")]
- iloc 인덱서 사용
   - 행의 순서값인 정수 사용
   - df.iloc[0, ("열라벨", "열라벨")]
- 슬라이싱
   - 튜플 안에는 슬라이싱 기호를 쓸 수 없다.
   - df.loc[(), :]
   - df.loc[:, ()]
- 튜플 안에 슬라이싱
   - df.loc[("행라벨", slice(None), "열라벨"]
   - df.loc["행라벨", ("열라벨", slice(None)]

### 다중 인덱스 순서 교환
- swaplevel(i, j, axis=)

### 정렬
- 행 다중 인덱스 정렬
   - df.sort_index(level=, axis=0) : level에 상위 하위 레벨 입력
- 열 다중 인덱스 정렬
   - df.sort_index(level=, axis=1) : level에 상위 하위 레벨 입력

# 06_merge_concatenate
- 병합 : merge
- 연결 : concatenate

### 데이터프레임 병합
- pd.merge(df1, df2, how="병합방식")
   - pd.merge(df1, df2, how="inner")
   - pd.merge(df1, df2, how="outer")
   - pd.merge(df1, df2, how="left")
   - pd.merge(df1, df2, how="right")
- 기준 키 값 설정
   - 병합할 때 사용할 키 값을 설정
   - pd.merge(df1, df2, on="고객명")
- 좌우 기준 키 값 설정
   - pd.merge(df1, df2, left_on="이름", right_on="성명")
   - pd.merge(df1, df2, left_on=["", ""], right_on=["", ""])
- 인덱스를 기준으로 병합
   - pd.merge(df1, df2, left_index=True, right_index=False)
- join
   - df1.join(df2, how="outer")

### 데이터프레임 연결
- pd.concat([df1, df2], axis=0)
   - 기준 열을 사용하지 않고 단순히 연결한다.
   - axis=0 : 수직으로 연결 : 행으로 연결
   - axis=1 : 수평으로 연결 : 열로 연결

# 07_pivottable_group_analysis

### pivot
- df.pivot("열이름1", "열이름2", "열이름3")
   - 열이름1 : 행 인덱스
   - 열이름2 : 열 인덱스
   - 열이름3 : 데이터로 사용할 열
- set_index + unstack() : 피봇과 같음
- 다중 인덱스 피봇
   - df.pivot(["열이름1", "열이름2"], "열이름3", "열이름4")

### gorupby 그룹분석
- GroupBy 객체를 생성해서 사용하거나, 직접 사용할 수 있다.
- df.groupby(df1.key1)
   - df.groupby([df1.key1, df1.key2])
- 그룹연산 메서드
   - size, count
   - mean, median, min, max
   - sum, prod, std, var, quantile
   - first, last
   - agg, aggregate
   - describe
   - apply
   - transform

### pivot_table
- pivot과 gorupby의 중간 성격
pivot_table(data, values-None, index=None, columns=None, aggfunc="mean", fill_value=None, margins=False, margins_name="All")
   - data : 분석할 데이터 프레임
   - values : 분석할 데이터프레임에서 분석할 열
   - index : 행 인덱스로 들어갈 키 열 또는 키 열의 리스트
   - columns : 열 인덱스로 들어갈 키 열 또는 키 열의 리스트
   - aggfunc : 분석 메서드, 디폴트 값은 평균.
   - fill_value : NaN 대체 값
   - margins : 모든 데이터를 분석한 결과를 오른쪽과 아래에 붙일지 여부
   - margins_name : 마진 열(또는 행)의 이름
- df.pivot()과 입력하는 열의 순서가 다름
- 다중 인덱스 테이블
   - df.pivot_table("열이름1", index=["열이름2", "열이름3"])

# 08_time_index


































































