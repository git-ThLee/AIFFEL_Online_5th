# LSTM

## RNN의 한계 - 장기 의존성(Long-Term Dependency)

입력데이터가 길어질 수록 데이터 앞쪽의 정보가 뒤쪽까지 전달이 잘 안되는 현상, 이는 RNN의 hidden layer를 학습하는 과정에서 기울기 소실 문제가 발생하기 때문에 발생합니다.  


## LSTM

LSTM은 Long Short-Term Memory의 약어로 **기울기 소실 문제를 해결하기 위해 고안된 RNN 레이어**입니다.

- [LSTM가 gradient vanishing에 강한이유?(+수식)](https://curt-park.github.io/2017-04-03/why-is-lstm-strong-on-gradient-vanishing/)  


- 수식으로 하면 어려우니까 수식 없이 설명

![image](https://d3s0tskafalll9.cloudfront.net/media/images/Screen_Shot_2022-02-18_at_4.29.30_PM.max-800x600.png)  

[RNN 그래프(왼쪽), LSTM 그래프(오른쪽)]  

![image](https://d3s0tskafalll9.cloudfront.net/media/images/lstm1.max-800x600.png)  

RNN에서는 볼 수 없던 $C_{t}$ 가 새롭게 등장했는데요. 이는 Cell state의 약자로 LSTM의 핵심 아이디어라고 할 수 있습니다. 전체 체인을 관통해 흐르며 long-term memory의 역할을 수행합니다.


