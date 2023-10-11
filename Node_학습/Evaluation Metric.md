

## Loss와 Metric

- Loss : 모델 학습시 학습데이터(train data) 를 바탕으로 계산되어, `모델의 파라미터 업데이트에 활용`되는 함수

- Metric : 모델 학습 종료 후 테스트데이터(test data) 를 바탕으로 계산되어, `학습된 모델의 성능을 평가`하는데 활용되는 함수

## Confusion Matrix 와 Precision/Recall

![images](https://d3s0tskafalll9.cloudfront.net/media/images/F-38-1.max-800x600.png)  

`True Positive (TP)` - 모델이 양성(Positive)을 양성으로 맞혔을 때
`True Negative (TN)` - 모델이 음성(Negative)을 음성으로 맞혔을 때
`False Positive (FP)` - 모델이 음성(Negative)을 양성(Positive)으로 잘못 예측했을 때
`False Negative (FN)` - 모델이 양성(Positive)을 음성(Negative)으로 잘못 예측했을 때
  
![image](https://www.researchgate.net/publication/336402347/figure/fig3/AS:812472659349505@1570719985505/Calculation-of-Precision-Recall-and-Accuracy-in-the-confusion-matrix.ppm)


# Accuracy(정확도)

![image](https://github.com/git-ThLee/AIFFEL_Online_5th/assets/55564114/50cc6ae0-4a30-4e43-b538-a1a5e6e89df1)


- 예시 문제

```python
TP(실제로 암이면서, 암으로 예측한 결과) = 1
TN(실제로 정상이고, 정상으로 예측한 결과) = 90
FN(실제로 암이지만, 정상으로 예측한 결과) = 8
FP(실제로 정상이지만, 암으로 예측한 결과) = 1

# Acc = (TP + TN) / (TP + TN + FP + FN)
Accuracy = (1 + 90) / (1 + 90 + 1 + 8) # 91 %
```
​
## Precision(정밀도)

![image](https://github.com/git-ThLee/AIFFEL_Online_5th/assets/55564114/b0a43da6-0dad-4dbe-bec6-13fb05768527)


이 개념은 모델이 `양성으로 규정한 것이 얼마나 정확한지`를 보고 싶은 것입니다. 모델이 음성으로 규정한 것에 대해서는 크게 관심이 없습니다. 정밀도가 높다는 것은 FP가 낮다는 것입니다. `즉 모델이 양성으로 잘못 규정한 것이 적을수록 정밀도는 올라갑니다.`

```python
TP(실제로 암이면서, 암으로 예측한 결과) = 1
TN(실제로 정상이고, 정상으로 예측한 결과) = 90
FN(실제로 암이지만, 정상으로 예측한 결과) = 8
FP(실제로 정상이지만, 암으로 예측한 결과) = 1

# Precision = (TP) / (TP + FP)
Precision = (1) / (1 + 1) # 50 %
```

## Recall(재현율) 

![image](https://github.com/git-ThLee/AIFFEL_Online_5th/assets/55564114/e17cfa20-a7e4-4a55-b6d1-d4d4d4db9d4e)  

​
 이 개념은 `실제로 양성이 것들이 얼마나 모델에 의해 정확하게 탐지되었나`를 보고 싶은 것입니다. 실제로 음성인 것을 양성으로 잘못 규정한 것에 대해서는 관심이 없습니다. 재현율이 높다는 것은 FN이 낮다는 것입니다. `즉 모델이 실제 양성을 분류해 내지 못한 경우가 적을 수록 재현율은 올라갑니다.`

```python
TP(실제로 암이면서, 암으로 예측한 결과) = 1
TN(실제로 정상이고, 정상으로 예측한 결과) = 90
FN(실제로 암이지만, 정상으로 예측한 결과) = 8
FP(실제로 정상이지만, 암으로 예측한 결과) = 1

# Recall = (TP) / (TP+FN)
Recall = (1) / (1 + 8) # 11 %
```

## Precision-Recall 커브

![image](https://github.com/git-ThLee/AIFFEL_Online_5th/assets/55564114/f46e084e-7e3e-4ef6-b690-3ee9b72eb0cc)  

PR(Precision-Recall) 커브는 Recall을 X축, Precision을 Y축에 놓고 Threshold 변화에 따른 두 값의 변화를 그래프로 그린 것

우리가 원하는 값은 Precision이든 Recall이든 모두 1에 가깝기를 원합니다. 이상적으로는 그래프가 (1, 1)에 찍히면 좋겠습니다만, 가급적 위 그래프가 (1, 1)에 근접하도록 그려지길 바랍니다.

## ROC 커브

![image](https://d3s0tskafalll9.cloudfront.net/media/original_images/F-38-4.png)  

