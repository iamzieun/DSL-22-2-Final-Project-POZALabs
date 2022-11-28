# POZALABs-DTW

<br>

## Project 배경/목표

### Project 배경

- POZAlabs: AI 기술을 활용한 작곡 서비스 제공
- 제공 되는 서비스의 질을 높이기 위해 해결해야할 주요 과제: 잠재적 표절 가능성 최소화 하기

### Project 목표

- 코드 진행의 유사도를 평가하는 모델을 개발해 잠재적 표절 가능성 최소화 하기
- 사용 모델: DTW

## DATA SET

![image](https://user-images.githubusercontent.com/108792199/204002628-842b7991-04f3-4dfa-8040-d64766f9b4d1.png)

--- 

<br>

```
Credit:   강건우 박수빈 ✊
```

<br>

## DTW에 대한 간략한 설명

![image](https://user-images.githubusercontent.com/108792199/204003634-81dc72d2-7152-4190-b369-5e9425ec4fef.png)

유클리드 계산 법으로는 같은 시점의 거리만을 고려할 수 밖에 없지만 dtw 는 그 거리가 최소화되는 방향으로 매칭시켜 누적 거리가 최소가 되는 warping(뒤틀림) 경로를 찾습니다. DTW는 최근에 자동음성 인식 분야에서 두각을 보이며 다른 속도를 가지는 음성을 인식하도록 해주는데,
이러한 부분이 음악 길이가 다름에도 유사성을 측정해야 하는 저희의 task에 적합할 것이라고 생각했습니다

### DTW 계산 방법
![image](https://user-images.githubusercontent.com/108792199/204006404-ba039bcf-6da6-4eca-8027-ce087e1b1e0c.png)

위 계산 행렬을 사용하여 메트릭스를 채워 넣습니다.
시작점 (오른쪽 위 코너: 15) 을 기반으로 시작점과 연속되면서 그 수가 작은 쪽으로 와핑거리를 계산할 수 있습니다.
그 값을 모두 더한 와핑 거리의 총합을 통해서 우리는 시계열이 얼마나 유사한지 알 수 있습니다.

---
### DTW 계산: [DTW 계산방법 자세히 보기](https://medium.com/walmartglobaltech/time-series-similarity-using-dynamic-time-warping-explained-9d09119e48ec)
---

<br>

## 진행과정
1. 포자랩스 Commu Data 불러오기 
2. 전체 chord_progressions 리스트 형태로 변화 시키기
3. chord_progression을 DTW에 적용 시키기 위해 시계열 형태로 변환 시키기
5. DTW 시행하기
6. 샘플들 1대1로 비교해보기
8. DTW에 사용하게 될 샘플 50개 무작위로 뽑기
9. Indexing 과정을 거친 후 데이터 프레임으로 바꿔주기
10. Clustering 진행하기
11. 유사하다는 기준을 세우기 위해 Sigmoid 사용해보기
12. 검증

##### 정확한 과정은 DTW_정리.ipnyb에서 확인 할 수 있습니다.

---

![image](https://user-images.githubusercontent.com/108792199/204011733-f9fd929b-2b2c-4b80-93a8-6328231e21d7.png)

#### clustering을 통해 만들어진 군집군 중 하나에 속한 샘플들을 가지고 DTW를 돌려보고 sigmoid 함수를 통해 기준을 세우는 과정입니다

![image](https://user-images.githubusercontent.com/108792199/204012199-98033bac-5120-433d-ac08-46b904aa425b.png)

#### DTW 결과를 그래프로 나타낸 것입니다. 
보이는 주황색과 검정색 선이 와핑 거리를 나타냅니다. 와핑거리의 합이 alignment cost 이고 alignment cost 가 작을수록 두 코드 진행은 유사합니다


---


<br>

---

## conclusion

---

![image](https://user-images.githubusercontent.com/108792199/204013641-a03cec51-b31c-4cbe-a957-bc544a544ee7.png)

#### 실제로 시그모이드 함수가 작을수록 두 코드 진행이 유사한 것을 볼 수 있다. 

---

## 보완점

---

1. 50개보다 많은 샘플들을 사용해봐야 한다. 점차적으로 사용하는 샘플의 수를 늘리는 과정이 필요하다
2. Indexing에 있어서 좀 더 다양한 방법을 시도해볼 것.
3. 음 이외에 다른 요소들을 어떻게 고려할 것인지 고민해 볼 것.
