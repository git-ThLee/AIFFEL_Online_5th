# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이태훈
- 리뷰어 : 김석영

# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네. 모든 코드가 정상적으로 동작하고, 루브릭의 평가문항과 그 기준도 충족했습니다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네. 주석, Task 구분과 설명, 출력 내용까지 상세히 작성돼 이해하는 데 큰 도움이 됩니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 네. Task 및 단계별로 상세하고 명확하게 작성이 된 코드로 에러 유발 인자는 찾을 수 없었습니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네. 필요 시 진행내용을 확인하는 코드들이 부분 부분 있으며, 학습노드와 같은 내용들에도 본인만의 스타일로 코드를 작성하였습니다.
- [X] 코드가 간결한가요?
  > 네. 반복되는 내용들을 함수화하여 전체적으로 간결하게 코드가 작성됐습니다.

# 예시
```python
def preprocessing(df):
    print(f'{len(df)} ->' ,end=' ')
    # 중복 제거
    df = df.drop_duplicates(subset=['ko'])
    df = df.drop_duplicates(subset=['en'])
    
    # 정규식
    def preprocess_sentence_kor(sentence):
        sentence = sentence.strip()                                         # 문장의 양쪽 공백 제거
        sentence = re.sub(r"([?.!,])", r" \1 ", sentence)                   # 특수 문자 및 구두점 주변에 공백 추가
        sentence = re.sub(r'[" "]+', " ", sentence)                         # 여러 개의 공백을 하나의 공백으로 대체
        sentence = re.sub(r"[^ㄱ-ㅎㅏ-ㅣ가-힣a-zA-Z?.!,]+", " ", sentence)  # 한글 및 영어 이외의 문자는 공백으로 대체
        sentence = sentence.strip()                                         # 다시 양쪽 공백 제거
        return sentence
    def preprocess_sentence_eng(sentence):
        sentence = sentence.lower().strip()
        sentence = re.sub(r"([?.!,])", r" \1 ", sentence)
        sentence = re.sub(r'[" "]+', " ", sentence)
        sentence = re.sub(r"[^a-zA-Z?.!,]+", " ", sentence)
        sentence = sentence.strip()
        return sentence
    
    # 'ko'와 'en' 열에 정규식 전처리 함수 적용
    df['ko'] = df['ko'].apply(preprocess_sentence_kor)
    df['en'] = df['en'].apply(preprocess_sentence_eng)
    
    # 길이가 0 인 데이터 제거
    df = df[(df['ko'].str.len() > 0) & (df['en'].str.len() > 0)]
    
    # en 에 <start> , <end> 토큰 추가
    df['en'] = df['en'].apply(lambda x : '<start> '+ x + ' <end>')
    
    # 토큰화 , ko : mecab , en : split
    mecab = Mecab()
    df['ko'] = df['ko'].apply(lambda x : mecab.morphs(x)) # nouns
    df['en'] = df['en'].apply(lambda x : x.split())
    
    # 토큰의 길이가 20 이하인 데이터를 선별하여 
    df = df[(df['ko'].str.len() < 21) & (df['en'].str.len() < 21)]
    print(f'{len(df)}')
    return df

train = preprocessing(train)
train.head()
print('덧셈', c.add()) 
```

# 참고 링크 및 코드 개선
```python
```
