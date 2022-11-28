## DataScienceLab-Yonsei-POZAlabs-CNN

### 1. 프로젝트 개요
Commu data를 활용하여 코드프로그레션 간 유사도 측정 알고리즘 개발 <br>
<데이터출처: POZAlabs gitub>
https://github.com/POZAlabs 

### 2. Ideation
코드프로그레션을 그래프로 표현한 후 <br>
CNN 알고리즘 적용해 이미지 유사도 측정

### 3. 코드프로그레션의 그래프 표현
Wongsaroj et al. (2014)의 Signature 공식을 사용 <br>
<논문 링크> https://ieeexplore.ieee.org/document/6821675/
![image](https://user-images.githubusercontent.com/108214382/204088554-458f8da1-31e6-44e5-a1f8-a7f06bb4be07.png)

### 4. 그래프로 표현한 코드프로그레션에 VGG-16 모델 적용
![image](https://user-images.githubusercontent.com/108214382/204088591-226a2be2-6525-4ffd-aad8-35a5937e0ffb.png) <br>
<모델 설명 이미지 링크> https://bskyvision.com/504 <br>
<코드 참조> https://mapadubak.tistory.com/121

### 5. 구현 결과 예시
![image](https://user-images.githubusercontent.com/108214382/204088854-caa79375-d3c1-4c7c-b8b9-b2298be4f7b7.png)

