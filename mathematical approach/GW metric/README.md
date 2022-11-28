## POZALabs project 
## __TF-IDF와 Bag of word를 활용한 유사도 검사__

### 0) __Data Set__
![image](https://user-images.githubusercontent.com/108792199/204002628-842b7991-04f3-4dfa-8040-d64766f9b4d1.png)

<br>

### 1) __아이디어 및 방법론__
> + 표절에 대한 판례를 살펴보면 음악저작물은 멜로디,리듬,화성의 3요소로 구성되어 있으며, 이 3요소에 대한 질적, 양적 정도를 감안하여 표절 유무를 판단함. <br><br>
> + 그렇지만 주어진 데이터를 통해 멜로디를 알 수 없으며 주어진 task는 코드 간 진행만을 통해 유사도를 판단하는 것임. <br><br>
> + 따라서 코드 간 진행을 하나의 sequence로 인식하고 NLP의 방법론인 TF-IDF를 적용하고자하며 희소한 코드 간 진행을 찾고 그 진행을 공유하는 두 commu data를 표절이 아닌가 의심하고자함. 

<br>

### 2) __수식 전개__
> + <Step 1> 마디 구분을 없앤 'chord_list' 변수 생성
>    + 코드 1개 당 8분의 1박자로 구분되어 마디수, 박자 구분이 되어있는 기존 'chord_progression' 변수에서 마디 구분을 없앰 <br><br>
> + <Step 2> 'chord_list'의 시작과 끝에 'soc(start of chord)' & 'eoc(end of chord)' 추가
>    + 어떠한 코드로 시작하는지, 어떠한 코드로 끝나는지 고려할 수 있음 <br><br>
> + <Step 3> BPM을 구간화한 bpm_group 변수 생성
>    + 보통 빠르기를 나타내는 90 bpm을 기준으로 30 bpm씩 구간화 <br><br>
> + <Step 4> n 개의 코드로 구성된 'chord_prog_token' 변수 생성
>    + __Key Point__
>    + NLP에서의 TF-IDF는 단어의 빈도수만 고려하므로 그대로 적용할 경우 코드 간 진행에 대한 고려를 하지 못함
>    + n 개의 코드를 하나의 토큰으로 만들어 코드 간 진행을 고려함. <br><br>
> + <Step 5> TF-IDF Matrix 생성
>    + A) 코드 간 진행 토큰을 행으로 하고 commu data의 개수를 열로 하는 matrix생성
>    ![그림1](https://user-images.githubusercontent.com/102268412/204111013-dc9095f3-8163-4e3e-9514-605ff22ee301.jpg) <br><br>
>    + B) TF-Score(코드 간 진행 토큰이 각 commu data에서 등장하는 횟수 / commu data의 총 토큰의 수)와 IDF-Count(해당 코드 간 진행 토큰이 등장한 commu data의 수) 계산
>    ![그림2](https://user-images.githubusercontent.com/102268412/204111030-5dbb8766-56be-4304-a183-b53f161f3e9d.jpg) <br><br>
>    + C) IDF-Score(log[총 commu data의 수 / (1 + IDF-Count)]) 계산
>    ![그림3](https://user-images.githubusercontent.com/102268412/204111059-d0263800-e6d5-4085-8521-8ff631a79ed9.jpg) <br><br>
>    + D) TF-Score x IDF-Score matrix 생성
>    ![그림4](https://user-images.githubusercontent.com/102268412/204111065-bf365f58-8b05-4281-9149-dc3c7c5b859e.jpg) <br><br>
>    + E) D에서 생성한 matrix를 전치시켜 Bag of Chord vector 생성 및 코사인 유사도 계산
>    ![그림5](https://user-images.githubusercontent.com/102268412/204111074-c767e81d-de69-4bf1-abb1-bfbb975d0eaf.jpg) <br><br>

<br>

### 3) __한계__
> + A) 마디수를 고려하지 않아 코드 간 진행은 같지만 마디수만 다른 두 commu data를 구분할 수 있는 수단이 bpm_group으로 한정되어 코사인 유사도가 1인 case가 상당수 존재함. <br><br>
> + B) Bag of Chord vector이 굉장히 sparse해 코사인 유사도가 0인 case 역시 상당수 존재함. <br><br>
> + A & B로 인해 코사인 유사도가 0 or 1에 편향돼 scaling하는데 어려움이 발생함. <br><br>
> + C) 정량평가가 어려움.
>    + 'chord_prog_token' 변수를 만들 때, n = 2 or n = 3 등 다양한 n으로 수식을 전개하였으나 무엇이 낫다라는 명확한 기준이 부재함. <br><br>
> + D) 새로운 commu data가 추가될 때 update의 cost가 상당함.
