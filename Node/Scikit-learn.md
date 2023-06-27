# 싸이킷런

## 주로 사용하는 API

![image](https://github.com/git-ThLee/AIFFEL_Online_5th/assets/55564114/beb1f952-7953-4ff2-8313-6fbca2689be9)  


## 데이터 표현법

- **특성 행렬(Feature Matrix)**
    - `입력 데이터를 의미`합니다.
    - `특성(feature)`: 데이터에서 수치 값, 이산 값, 불리언 값으로 표현되는 개별 관측치를 의미합니다. 특성 행렬에서는 열에 해당하는 값입니다.
    - `표본(sample)`: 각 입력 데이터, 특성 행렬에서는 행에 해당하는 값입니다.
    - `n_samples`: 행의 개수(표본의 개수)
    - `n_features`: 열의 개수(특성의 개수)
    - `X`: 통상 특성 행렬은 변수명 X로 표기합니다.
    - `[n_samples, n_features]`은 [행, 열] 형태의 2차원 배열 구조를 사용하며 이는 NumPy의 ndarray, Pandas의 DataFrame, SciPy의 Sparse Matrix를 사용하여 나타낼 수 있습니다.

- **타겟 벡터 (Target Vector)**
    - `입력 데이터의 라벨(정답) 을 의미`합니다.
    - `목표(Target)`: 라벨, 타겟값, 목표값이라고도 부르며 특성 행렬(Feature Matrix)로부터 예측하고자 하는 것을 말합니다.
    - `n_samples`: 벡터의 길이(라벨의 개수)
    타겟 벡터에서 n_features는 없습니다.
    - `y`: 통상 타겟 벡터는 변수명 y로 표기합니다.
    - 타겟 벡터는 보통 1차원 벡터로 나타내며, 이는 NumPy의 ndarray, Pandas의 Series를 사용하여 나타낼 수 있습니다.
    - (단, 타겟 벡터는 경우에 따라 1차원으로 나타내지 않을 수도 있습니다. 이 노드에서 사용되는 예제는 모두 1차원 벡터입니다.)