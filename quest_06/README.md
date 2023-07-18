# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이태훈
- 리뷰어 : 김연수


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네, 모든 코드가 정상적으로 동작하며, 주어진 과제를 해결했습니다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네, 주석이 알기 쉽게 적혀있어서 코드 이해에 도움이 되었습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 결과값으로 보아, 에러를 유발할 코드는 없는 것으로 보입니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네, 작성한 코드에 대해 짧게 얘기해보는 시간을 가졌는데, 충분한 이해를 바탕으로 코드를 작성하신 것 같습니다.
- [X] 코드가 간결한가요?
  > 네, 간결합니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.

### 1) 주석이 이해하기 쉽게 적혀있어서 코드 이해에 도움이 되었습니다.
```python
# 샘플 길이 안넘는 애들만 살리기
# 샘플 길이를 넘으면 사용안함
# text_max_len = 50
# summary_max_len = 14
def check_length(row):
    text_len = len(row['text'].split())
    summary_len = len(row['headlines'].split())
    return text_len <= text_max_len and summary_len <= summary_max_len

# apply 함수와 lambda 식을 사용하여 조건에 맞는 샘플만 남기기
data = data[data.apply(lambda row: check_length(row), axis=1)]

# 결과 출력
print('전체 샘플수 :', (len(data)))
```
### 2) 추출요약 과정에서 summa 사용시 blank 값이 많이 나온다는 문제점을 발견하고, 대안을 적용했습니다.  
- textsummarizer.py사용
  ```python
  def generate_summary(text, top_n):
    # 영어 불용어(stop words)를 사용하기 위해 stopwords.words('english')를 호출합니다.
    stop_words = stopwords.words('english')
    summarize_text = []
    
    # 텍스트를 문장 단위로 분리합니다. (read_article 함수 호출)
    sentences = read_article(text)
    
    # 문장 간 유사도 행렬을 생성합니다. (build_similarity_matrix 함수 호출)
    sentence_similarity_matrix = build_similarity_matrix(sentences, stop_words)
    
    # 유사도 그래프를 생성합니다. (넘파이 배열을 이용하여 nx.from_numpy_array 호출)
    sentence_similarity_graph = nx.from_numpy_array(sentence_similarity_matrix)
    
    # 문장별 점수를 계산합니다. (페이지랭크 알고리즘을 사용하여 nx.pagerank 호출)
    scores = nx.pagerank(sentence_similarity_graph)
    
    # 점수에 따라 문장을 정렬합니다.
    ranked_sentences = sorted(((scores[i], s) for i, s in enumerate(sentences)), reverse=True)
    
    # 상위 top_n개의 문장을 선택합니다.
    for i in range(top_n):
        summarize_text.append(ranked_sentences[i][1])
    
    # 선택된 문장들을 하나의 문자열로 결합하여 반환합니다.
    return " ".join(summarize_text), len(sentences)
```

# 참고 링크 및 코드 개선
```python
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
전반적으로 코드가 잘 작동하며, Flowchart와 rouge를 사용한 성능평가가 작성되어 이해하는 데에 큰 도움이 되었습니다.
