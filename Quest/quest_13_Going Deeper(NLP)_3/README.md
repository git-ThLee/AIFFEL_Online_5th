# AIFFEL Campus Online 5th Code Peer Review Templete
- 코더 : 이태훈
- 리뷰어 : 김석영


# PRT(PeerReviewTemplate) 
각 항목을 스스로 확인하고 토의하여 작성한 코드에 적용합니다.

- [X] 코드가 정상적으로 동작하고 주어진 문제를 해결했나요?
  > 네. 코드가 에러 없이 잘 동작합니다.
  > 네. 루브릭에 명시된 평가문항과 상세기준을 모두 충족하였습니다.
- [X] 주석을 보고 작성자의 코드가 이해되었나요?
  > 네. 코드에 대한 주석뿐만 아니라, Markdown을 통한 Task별 구분과 상세설명이 잘 작성돼 있어, 이해하는 데 무리가 없습니다.
- [X] 코드가 에러를 유발할 가능성이 없나요?
  > 네. 에러 유발 인자는 보이지 않습니다.
- [X] 코드 작성자가 코드를 제대로 이해하고 작성했나요?
  > 네. 모든 코드가 Task별 이해 단위로 구분돼 작성돼 있고,
  > 출력 및 시각화 결과들을 통해 제대로된 이해를 통해 코드가 작성됐음을 확인할 수 있습니다.
- [X] 코드가 간결한가요?
  > 네. 중복된 코드와 불필요한 출력 결과가 없는 간결한 코드입니다.

# 예시
1. 코드의 작동 방식을 주석으로 기록합니다.
2. 코드의 작동 방식에 대한 개선 방법을 주석으로 기록합니다.
3. 참고한 링크 및 ChatGPT 프롬프트 명령어가 있다면 주석으로 남겨주세요.
```python
results_list = sorted(results_list, key= lambda x : x[2], reverse=True )
for a, b, score in results_list:
    print(f'{a} vs {b},{score}')
    print('\t',end='')
    if score > 0 :
        print(f'▶결론 : {a} -> 예술(art), {b} -> 일반(gen)]')
    else:
        print(f'▶결론 : {b} -> 예술(art), {a} -> 일반(gen)]')
```

# 참고 링크 및 코드 개선
```python

```
