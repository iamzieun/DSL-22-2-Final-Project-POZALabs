# DSL-22-2-Final-Project-POZALabs
[2022-2학기 DSL X POZALabs 기업연계 프로젝트] 코드 진행 간 유사도 측정 기준 확립 및 구현

## 수식을 통한 코드 진행 간 유사도 구하기
- 참고 논문: A music similarity measure based on chord progression and song segmentation analysis (Chaisup Wongsaroj, Nakornthip Prompoon, Athasit Surarerks)

### 1. Data Preprocessing
commu_meta.csv의 chord_progressions을 list 형태로 변환 

### 2. Chord Similarity (C_Sim)
모든 chord간의 유사도 측정
C_{-} \operatorname{Sim}\left(C_1, C_2\right)=\frac{\left|P\left(C_1\right) \cap P\left(C_2\right)\right|}{\left|P\left(C_1\right) \cup P\left(C_2\right)\right|}

$C_{-} \operatorname{Sim}\left(C_1, C_2\right)=\frac{\left|P\left(C_1\right) \cap P\left(C_2\right)\right|}{\left|P\left(C_1\right) \cup P\left(C_2\right)\right|}$

$$
C_{-} \operatorname{Sim}\left(C_1, C_2\right)=\frac{\left|P\left(C_1\right) \cap P\left(C_2\right)\right|}{\left|P\left(C_1\right) \cup P\left(C_2\right)\right|}

\begin{equation}
C_{-} \operatorname{Sim}\left(C_1, C_2\right)=\frac{\left|P\left(C_1\right) \cap P\left(C_2\right)\right|}{\left|P\left(C_1\right) \cup P\left(C_2\right)\right|}
\end{equation}
$$
