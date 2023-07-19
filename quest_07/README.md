# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이태훈
- 리뷰어 : 이수봉


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 모델을 10 epoch 이상 학습을 진행 하였고, 주어진 문제를 해결 하였습니다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 마크다운을 통해 모델의 구조와, 코드의 역할에 대해 주석이 있었습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 아니요 없습니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 코드의 주석을 통해 작성자가 코드를 제대로 이해하고 작성했음을 알 수 있었습니다.


  > 10 epoch 학습을 진행하는 동안 손실값을 그래프로 작성해서 보여주었습니다.


  > 학습이 완료된 모델에 여러종류의 val 이미지를 넣어서 테스트를 진행 하였습니다.


- [X] 코드가 간결한가요?
  > 불필요한 코드 없이 간결했습니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
# 사칙 연산 계산기
def normalize(x):
    '''
    정규화 
    '''
    x = tf.cast(x, tf.float32)
    return (x/127.5) - 1

def denormalize(x):
    '''
    역정규화
    '''
    x = (x+1)*127.5
    x = x.numpy()
    return x.astype(np.uint8)

def load_img(img_path):
    '''
    이미지 sketch와 colored로 나누기 
    '''
    img = tf.io.read_file(img_path)
    img = tf.image.decode_image(img, 3)
    
    w = tf.shape(img)[1] // 2
    sketch = img[:, :w, :] 
    sketch = tf.cast(sketch, tf.float32)
    colored = img[:, w:, :] 
    colored = tf.cast(colored, tf.float32)
    return normalize(sketch), normalize(colored)

@tf.function()
def apply_augmentation(sketch, colored):
    stacked = tf.concat([sketch, colored], axis=-1)
    
    _pad = tf.constant([[30,30],[30,30],[0,0]])
    if tf.random.uniform(()) < .5:
        # 데이터를 반사(reflect) 모드로 패딩
        padded = tf.pad(stacked, _pad, "REFLECT")
    else:
        # 데이터를 상수(constant) 값으로 패딩
        padded = tf.pad(stacked, _pad, "CONSTANT", constant_values=1.)

    # 이미지를 무작위로 잘라내기
    out = image.random_crop(padded, size=[256, 256, 6])
    
    # 이미지를 무작위로 좌우 반전
    out = image.random_flip_left_right(out)
    
    # 이미지를 무작위로 상하 반전
    out = image.random_flip_up_down(out)
    
    if tf.random.uniform(()) < .5:
        # 이미지를 무작위로 회전
        degree = tf.random.uniform([], minval=1, maxval=4, dtype=tf.int32)
        out = image.rot90(out, k=degree)
    
    # 결과를 스케치 이미지와 컬러 이미지로 분리하여 반환
    return out[...,:3], out[...,3:]


def get_train(img_path):
#     sketch, colored = load_img(img_path)
    colored, sketch = load_img(img_path)
    sketch, colored = apply_augmentation(sketch, colored)
    return sketch, colored

# 훈련 이미지 데이터셋 생성
train_images = data.Dataset.list_files(train_path + "*.jpg")

# get_train 함수를 적용하여 이미지 데이터 전처리 및 셔플링, 배치 처리
train_images = train_images.map(get_train).shuffle(100).batch(4)

# 샘플 이미지 가져오기
sample = train_images.take(1)
sample = list(sample.as_numpy_iterator())
sketch, colored = (sample[0][0]+1)*127.5, (sample[0][1]+1)*127.5

# 시각화
plt.figure(figsize=(10,5))
plt.subplot(1,2,1); plt.imshow(sketch[0].astype(np.uint8))
plt.subplot(1,2,2); plt.imshow(colored[0].astype(np.uint8))
```

# 참고 링크 및 코드 개선
```python
# 손실 값을 그래프로 시각화해서 보여준 점이 인상 깊었습니다.
# 300 에폭에 대한 결과가 궁금한데 실수로 날아갔다고 하시니 아쉽네요
```