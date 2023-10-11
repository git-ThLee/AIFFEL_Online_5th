# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이태훈
- 리뷰어 : 김연수


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  네, 모두 정상적으로 동작하며, 과제에 맞게 작성된 것 같습니다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 중간중간 마크다운으로 설명이 자세히 되어있어서, 전반적인 코드를 이해하는 데에 큰 도움이 되었습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 에러 없이 모두 잘 동작하는 것으로 보입니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 작성하신 내용으로 보아 코드에 대한 충분한 이해를 바탕으로 작성된 것 같습니다.
- [X] 코드가 간결한가요?
  > 네, 간결합니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.

- 주석을 보고 작성자의 코드가 이해되었나요?
```python
def process(num_words = 10000,    # 단어장 개수
            max_len_text = None,  # 데이터 길이 조정
            max_len_pad = 500,    # pad 길이
            vec_type= None,      # 벡터화 타입
            class_weight_bool = False  # class_weight 사용 여부
           ):
    # Data Load
    (x_train, y_train), (x_test, y_test) = reuters.load_data(
                                                            num_words=num_words, 
                                                            test_split=0.2
                                                        )
    
    # 데이터 길이 제한
    if max_len_text:
        x_train = [x[:max_len_text] for x in x_train]
        x_test = [x[:max_len_text] for x in x_test]
        
    # tf_idf 방식으로 텍스트를 벡터화
    if vec_type == 'tfidf' :
        x_train, x_test = tf_idf(x_train, x_test)
    else:
        # Padding - TF-IDF 에서는 필요없음.
        x_train = pad_sequences(x_train, maxlen=max_len_pad)
        x_test = pad_sequences(x_test, maxlen=max_len_pad) 
```
- 전반적으로 표와 그래프를 많이 사용하셔서, 여러가지로 실험을 해보고 분석하셨다는 것을 알 수 있었습니다.

# 참고 링크 및 코드 개선
```python
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
