# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이태훈
- 리뷰어 : 손정민


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 정상적으로 실행되었고 전처리, 모델 구성, 평가까지 문제 없이 진행하였다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 주석이 상세했을 뿐만 아니라 마크다운을 통한 이론적 설명이 있었고, 시각화도 포함되어 코드 이해가 용이했다.
  ```python
  def create_padding_mask(x):
    """
    패딩 마스크를 생성하는 함수입니다.

    Args:
      x: 입력 시퀀스 텐서. 정수로 구성된 텐서로서, 0은 패딩 값을 나타냅니다.
         (예: [2, 4, 6, 0, 0]는 패딩이 적용된 길이가 5인 시퀀스입니다.)

    Returns:
      mask: 패딩 마스크. 패딩 위치에 1을 표시하는 텐서입니다. (pad 위치: True, 그 외: False)
            3차원 텐서로서, (batch_size, 1, 1, sequence_length)의 크기를 가집니다.
            이 마스크는 트랜스포머에서 패딩된 부분을 무시하는 데 사용됩니다.
    """

    # x에서 값이 0인 위치를 찾아서 True로, 그 외 위치를 False로 변환합니다.
    mask = tf.cast(tf.math.equal(x, 0), tf.float32)

    # 차원을 늘려서 마스크를 (batch_size, 1, 1, sequence_length) 크기로 변환합니다.
    # 이렇게 하면 브로드캐스팅을 이용하여 패딩 마스크를 인코더 및 디코더에서 사용할 수 있게 됩니다.
    mask = mask[:, tf.newaxis, tf.newaxis, :]

    return mask
  ```
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 에러 없이 잘 실행되었다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 여러 condition에서의 테스트를 진행하였다. 회고에서도 결과에 영향을 주는 요소를 찾고 추가해볼 수 있는 방법을 제시했다. 또한 문제점에 대해서 코드 내부의 오류를 찾고 해결한 점에서 프로젝트와 코드에 대한 이해도가 높음을 알 수 있었다.
- [X] 코드가 간결한가요?
  > 직관적인 함수명과 변수명을 사용했다. 시각화하는 부분의 경우 함수화하여 코드가 반복되는 것을 방지했고, 코드 내의 적절한 개행과 공백으로 가독성을 높였다.
  ```python
  def show_log(history, case):
    fig, ax = plt.subplots(2,1, figsize = (5, 8))
    ax[0].set_title(f"{case} Accuracy : {history.history['accuracy'][-1]}")
    ax[0].plot(range(len(history.history['accuracy'])), history.history['accuracy'], 'orange', label = 'accuracy')...
  ```

# 참고 링크 및 코드 개선
개선할 부분은 없는 것 같습니다.