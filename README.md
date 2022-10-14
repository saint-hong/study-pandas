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














































































