# DSL-22-2-Final-Project-POZALabs
[2022-2학기 DSL X POZALabs 기업연계 프로젝트] 코드 진행 간 유사도 측정 기준 확립 및 구현

## BC3Nd - Evaluating Distance of Chord Progressions with 5-dimensional chord vectors

### 1. Base

#### 1-1. Bass Definition
코드의 근음을 나타내는 부분. <br>
0부터 11까지의 값을 가진다.

#### 1-2. Bass difference calculation
두 코드의 근음 차이는 단순히 두 근음을 빼는 것이 아닌, <br>
5도권 (Circle of Fifth) 상에서의 거리를 계산하는 방식으로 구해진다. <br>
시계방향은 양수, 반시계방향은 음수의 값을 가진다.

### 2. Chord

#### 2-1. Chord Definition
코드의 나머지 구성음을 나타내는 부분. <br>
하나의 코드는 총 3~4개의 음을 가지나, <br>
길이를 통일하기 위해 모든 코드의 음의 개수를 4개로 통일함. <br>
(원래 음이 3개인 경우, 근음의 한 옥타브 위 음이 있다고 가정하고 추가함) <br>
모든 Chord 부분은 근음으로부터의 상대적인 거리로 계산되며,  <br>
Chord 유형에 따라 획일화된 값을 가지므로 이를 미리 Dictionary에 저장해 사용함.

#### 2-2. Chord Difference calculation
앞의 코드의 코드 벡터에서 뒤 코드의 코드 벡터를 빼서 계산하게 된다.

### 3. Non-diatonic Notes
(주의. 코드 상에서 Non-diatonic note와 관련된 내용은 모두 'special'이라는 이름으로 기록되어 있음)

#### 3-1. Non-diatonic notes Definition
코드 내의 구성음 4개 중에서 Non-diatonic 음의 개수를 나타냄. <br>
commu data 상에서는 모든 조가 A minor 혹은 C Major 이므로, <br>
Diatonic note는 항상 도/레/미/파/솔/라/시 이며, <br>
나머지 음은 모두 Non-Diatonic note가 된다.

#### 3-2. Non-diatonic notes difference calculation
Non-diatonic note의 경우 코드가 변화하면서 차이가 나는 개수가 중요한 것이 아니라, <br>
현재 몇 개의 Non-diatonic note가 들리는지가 중요하다고 판단, <br>
뒤 코드의 Non-diatonic note의 개수를 그대로 가져와 사용하게 함.

### 4. Functions

#### 4-1. make_chord_matrix_fifth_circle()
하나의 코드 진행이 있을 때, 그 코드 진행을 BC3Nd에 의해 변환해 주는 함수.

#### 4-2. compare_chord_fifth_circle()
하나의 행렬 안에 있는 2개의 코드 진행에 대해, 두 개의 코드 진행의 차를 계산해 주는 함수.

#### 4-3. similarity_calculation_fifth_circle()
하나의 행렬 안에 있는 n개의 코드 진행에 대해, <br>
가능한 모든 조합을 비교해 가며 두 개의 코드 진행의 차를 계산해 주는 함수. <br>

#### 4-4. one_to_one_error_calc()
4-2.와 같은 역할을 해 주는 함수. <br>
단, input으로 행렬을 받지 않고 2개의 코드 진행 list를 받게 됨.

#### 4-5. t, b, s, c
t: Total error <br>
b: Bass error <br>
s: Non-diatonic error <br>
c: Chord error <br>
로, 각각의 원인 별로 어디에서 값이 커지거나 작아졌는지를 비교할 수 있다.