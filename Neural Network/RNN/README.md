# RNN을 이용한 코드 간 유사도 구하기
- 참고 논문 : COMPARING RNN PARAMETERS FOR MELODIC SIMILARITY (Tian Cheng, Satoru Fukayama, Masataka Goto)

## RNN_code.ipynb

### 1. Initialize
- unique한 292개의 코드 데이터를 모델에 학습시킴
- GRU model 사용

### 2. Individualize
- Initialize와 동일한 모델 구조
- 각 코드 별 고유한 모델 학습 (500 iter)
- 모델의 파라미터끼리의 유사도를 통해 코드 간 유사도 구함
- 사용한 파라미터 : gru layer, fc layer

## initialization_model.pt
- Initialize 단계에서 학습된 베이스 모델
- batch = 16, epoch = 60
- n_layers = 2
- input_dim = 63
- emb_dim, hid_dim = 32


## individualized_parameters.csv
- Individualize 단계에서 코드 별 학습된 각 모델의 파라미터