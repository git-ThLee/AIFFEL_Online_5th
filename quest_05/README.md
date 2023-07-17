# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이태훈
- 리뷰어 : 이효겸


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 기존 이미지의 문제점이 아닌 자신이 만들어낸 인물모드의 문제점을 지적하지 못함
  > 모델이 만들어 낸 마스크 영역에 어떻게 적용되어 문제점을 보완하게 되는지의 메커니즘이 전혀 포함되지 않았따.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 쓰여진 주석은 이해가 잘 되었습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 고정적으로 짜여져 있어서 에러를 유발할 가능성은 없어 보입니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 단락별로 코드를 잘 나누어 실행 시킨것으로 보아 제대로 이해하고 작성한 것으로 보입니다,
- [ ] 코드가 간결한가요?
  > 코드 하나하나는 간결하나 함수 대신 for문을 이용하여 반복 코드의 작성을 방지하였지만 for문이 중복적으로 사용되었다
```python
# 세그멘테이션
for i, img_path in enumerate(img_paths):
    img_orig = cv2.imread(img_path)
    img_rgb = cv2.cvtColor(img_orig, cv2.COLOR_BGR2RGB)
    
    segvalue, output = model.segmentAsPascalvoc(img_path)
    segvalues.append(segvalue)
    outputs.append(output)
    
    axes[i].imshow(output)
    axes[i].axis('off')
plt.show()

# 배경 분리
for idx, img_orig in enumerate(img_origs):
    img_show = img_orig.copy()

    # 마스크 영역을 1 or 0 분리
    img_mask = seg_maps[idx].astype(np.uint8) * 255
    img_masks.append(img_mask)
    color_mask = cv2.applyColorMap(img_mask, cv2.COLORMAP_JET)

    img_show = cv2.addWeighted(img_show, 0.9, color_mask, 0.8, 0.0)

    #plt.imshow(cv2.cvtColor(img_show, cv2.COLOR_BGR2RGB))
    img_show = cv2.cvtColor(img_show, cv2.COLOR_BGR2RGB)
    axes[idx].imshow(img_show)
    axes[idx].axis('off')
plt.show()

# 결과
for i, img_path in enumerate(img_paths):
    img_orig = cv2.imread(img_path)
    img_rgb = cv2.cvtColor(img_orig, cv2.COLOR_BGR2RGB)
    
    segvalue, output = model.segmentAsPascalvoc(img_path)
    segvalues.append(segvalue)
    outputs.append(output)
    
    axes[i].imshow(output)
    axes[i].axis('off')
plt.show()
```

# 참고 링크 및 코드 개선
```python
단락들을 분리하여 작성한 것은 좋았지만 묶을 수 있는 것은 묶고 
단위별로 함수를 만들고 리턴값으로 이미지반환을 하면 이미지를 보기도 괜찮을 것으로 보이며
함수내 주석을 상세하게 써놓았으면 좋았을 것 같다.

대충 이런식
ex)
for image_path in image_paths:
    # 모델 적용함수
    output = seg_model(image_path)
    result = person_mode(output)
    ...

```