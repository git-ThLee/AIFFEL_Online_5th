# RNN

순차 데이터를 처리하기 위해 고안된 것이 바로 **Recurrent Neural Network 또는 Recurrent 레이어(이하 RNN)** 입니다. 반복되는 성격을 가지고 있다고 해서 Recurrent라는 이름이 붙었습니다.

![image](https://d3s0tskafalll9.cloudfront.net/media/images/rnn1.max-800x600.png)  

RNN의 입력으로 들어가는 모든 단어만큼 Weight를 만드는 게 아님에 유의합니다. (입력의 차원, 출력의 차원)에 해당하는 단 하나의 Weight를 순차적으로 업데이트하는 것이 RNN입니다. 그렇다 보니 한 문장을 읽고 처리하는 데에도 여러 번의 연산이 필요해 다른 레이어에 비해 느리다는 단점이 있어요.  

![image](https://d3s0tskafalll9.cloudfront.net/media/original_images/F-24-13.png)  

`What`의 정보가 마지막 입력인 `?`에 다다라서는 거의 희석된 모습을 보여주고 있죠. 이것이 RNN의 고질적인 문제점인데, **입력의 앞부분이 뒤로 갈수록 옅어져 손실이 발생**합니다. 이를 `기울기 소실(Vanishing Gradient)` 문제라고 합니다.







