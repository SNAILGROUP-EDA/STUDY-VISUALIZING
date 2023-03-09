## ❓ 결측치 처리

<details><summary><h3>결측치(Missing Value)란 무엇인가</h3></summary>

- **정의 : 기입되지 않은 데이터**

- **`None` 과 `NaN` 의 구분**
    - `None`(Null) : 아무것도 존재하지 않는 데이터
    - `NaN`(Not a Number) : 정의되거나 표현되지 못하는 데이터

- **발생 원인 규명 가능 여부에 따른 구분**
    - **완전 무작위 결측(Missing completely at Random; MCA)** : 발생 원인을 파악할 수 없는 결측치
    - **무작위 결측(Missing at Random; MAR)** : 발생 원인을 완전히 설명할 수는 없는 결측치
    - **비무작위 결측(Missing at Not Random; MNAR)** : 발생 원인을 완전히 설명할 수 있는 결측치

- **결측치 처리 권장 방식**
    - **비무작위 결측의 처리**
        - 대표값에 영향을 미치지 않는 특정 값으로 대체함
            - 결측치를 나타내는 특정 값을 정의하고 해당 값으로 대체
            - 평균(수치형 변수), 최빈값(범주형 변수) 등 대표값으로 대체
    
    - **무작위 결측의 처리**
        - 10% 미만 : 해당 레코드 제거
        - 20% 미만 : 평균(수치형 변수), 최빈값(범주형 변수) 등 대표값으로 대체
        - 20% 이상 : 결측치를 처리하는 머신러닝 모델 설계

</details>

<details><summary><h3>결측치 탐색</h3></summary>
    
- **메소드 `isnull()`를 통한 결측치 탐색**

    ```
    # 결측치가 존재할 경우 True, 존재하지 않을 경우 False를 기입한 데이터프레임 반환
    df.isnull()

    # 데이터프레임 df의 컬럼별 결측치 개수 반환
    df.isnull().sum()

    # 데이터프레임 df의 컬럼별 결측치 비율 반환
    df.isnull().mean()
    ```

- **모듈 `missingno`를 통한 결측치 분포 시각화**

    ```
    import missingno as msno

    # 데이터프레임 df의 컬럼별 결측치 위치 시각화
    msno.matrix(df = df)
    
    # 데이터프레임 df의 컬럼별 결측치 비율 시각화
    msno.bar(df = df)
    ```

</details>

<details><summary><h3>결측치 처리</h3></summary>

- **메소드 `dropna()`를 통한 결측치가 포함된 레코드 제거**

    ```
    df.dropna()
    ```

    - `how = 'any'` : 삭제 조건 세부 설정
        
        - `any` : 결측치가 하나라도 포함된 레코드를 제거함
        - `all` : 모든 컬럼이 결측치인 레코드만 제거함

- **메소드 `fillna()`를 통한 결측치 대체**

    ```
    # 범주형 설명변수의 결측치를 최빈값으로 대체함
    mode_value = df[cat_col].mode(
        axis = 1, 
        numeric_only = False, 
        dropna = True
        )
    df[cat_col] = df[cat_col].fillna(mode_value)

    # 수치형 설명변수의 결측치를 평균으로 대체함
    mean_value = df[num_col].mean()
    df[num_col] = df[num_col].fillna(mean_value)
    ```

</details>
