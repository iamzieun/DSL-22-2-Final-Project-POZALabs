# DSL-22-2-Final-Project-POZALabs
[2022-2학기 DSL X POZALabs 기업연계 프로젝트] 코드 진행 간 유사도 측정 기준 확립 및 구현

## 수식을 통한 코드 진행 간 유사도 구하기
- 참고 논문: A music similarity measure based on chord progression and song segmentation analysis (Chaisup Wongsaroj, Nakornthip Prompoon, Athasit Surarerks)

### 1. Data Preprocessing
commu_meta.csv의 chord_progressions을 list 형태로 변환 

### 2. Chord Similarity (C_Sim)
모든 chord간의 유사도 측정
$C_{-} \operatorname{Sim}\left(C_1, C_2\right)=\frac{\left|P\left(C_1\right) \cap P\left(C_2\right)\right|}{\left|P\left(C_1\right) \cup P\left(C_2\right)\right|}$

### 3. Sequence Similarity (S_Sim)
코드 진행 간 유사도 측정
\operatorname{CS} \operatorname{Sim}\left(S_1, S_2\right)=\max _{\substack{0 \leq i \leq m-n_{-} u n i t, 0 \leq j \leq n-n_{-} \text {unit }}} \frac{\sum_{k=1}^{n_{-} \text {unit }} C_{-} \operatorname{Sim}(a[i+k], b[j+k])}{n_{-} u n i t}

### 4. 구현 결과 예시
![image](https://user-images.githubusercontent.com/97666193/204125719-618ae38f-1fd4-47f4-9305-e88c58263d84.png)
