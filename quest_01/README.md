# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이태훈
- 리뷰어 : 윤상현


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [✓] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
- [✓] 주석을 보고 작성자의 코드가 이해되었나요?
  각 라인별로 마크다운을 통해 큰 틀을 잡아준 뒤,
  주석으로 설명해주시는 부분이 좋았습니다.
- [✓] 코드가 에러를 유발할 가능성이 없나요?
- [✓] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  마크다운에 있는 설명과 주석을 보면,
  확실하게 이해하고 작성한 것으로 보입니다.
- [✓] 코드가 간결한가요?
  코드별 길이가 짧고, 변수명도 직관적이라 이해하기 쉬웠습니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 각각을 def로 함수화하여 진행하신 부분이 좋았습니다.
# 해당 부분에 대해서는 추후 module이나 class로 묶어서 사용할 수 있을 것 같아
# OOP의 사용성을 극대화시켰다고 판단됩니다.

W = np.random.rand(10)
b = np.random.rand()

# 모델 함수를 구현해주세요.
def model(X, W, b):
    predictions = 0
    for i in range(10):
        predictions += X[:, i] * W[i]
    predictions += b
    return predictions

# 손실함수를 MSE 함수로 정의해주세요.
def MSE(a, b):
    mse = ((a - b) ** 2).mean()  # 두 값의 차이의 제곱의 평균
    return mse

def loss(X, W, b, y):
    predictions = model(X, W, b)
    L = MSE(predictions, y)
    return L

# 기울기를 계산하는 gradient 함수를 구현해주세요.
def gradient(X, W, b, y):
    # N은 데이터 포인트의 개수
    N = len(y)

    # y_pred 준비
    y_pred = model(X, W, b)

    # 공식에 맞게 gradient 계산
    dW = 1/N * 2 * X.T.dot(y_pred - y)

    # b의 gradient 계산
    db = 2 * (y_pred - y).mean()
    return dW, db

losses = []
for i in range(1, 10001):
    dW, db = gradient(x_train, W, b, y_train)
    W -= LEARNING_RATE * dW
    b -= LEARNING_RATE * db
    L = loss(x_train, W, b, y_train)
    losses.append(L)
    if i % 10 == 0:
        print('Iteration %d : Loss %0.4f' % (i, L))

```

# 참고 링크 및 코드 개선
```python
# 없습니다. 
```
