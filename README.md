# Controller_Comparison_Group

거창한 제목에 그렇지 못한 내용

해당 레포는 nav2 오픈소스를 활용해서 여러 컨트롤러 알고리즘의 비교를 위해 만들었음.

# Enviroment (내 환경)
![ROS2 - humble](https://img.shields.io/:Build-humble-yellowgreen.svg)
![Ubuntu - 22.04](https://img.shields.io/:Ubuntu-22.04-skyblue.svg)

### test AMR : DD(Diff Drive) type model

(단위 mm)
- width : 804 * 410
- high  : 220

### Simulator Enviroment
- gazebo classic
- rviz2
- URDF MODEL

## DWB

Nav2 오픈소스는 기본 값으로 DWB 컨트롤러로 Planer를 따라간다.


https://github.com/user-attachments/assets/1773744b-04b1-434b-92f2-a111beb875c9



### Nav 개발자라면 한 번쯤 본 친구

DWB 컨트롤러는 경험상 파라메터 셋팅 값의 영향을 크게 받는 것 같다.

angular velocity 값이 빠르면 빠를 수록 커브를 돌다 장애물에 부딫힌다. 그리고 좁은 길을 잘 못 간다.

(또 속도가 느리면 잘 작동하는 것 같기도 하다.)

이유는 아마 costmap에서 비용 계산과 관련해서 처리하는 속도 때문인 것 같은데.. 아직은 확인 해봐야 할 것 같다.


## TEB

현재는 유지보수가 줄어든 것으로 알려진 TEB 컨트롤러


https://github.com/user-attachments/assets/efab79c9-251a-4e0f-b45d-37ff8f9350f5


### 후진을 위한 컨트롤러?

TEB 컨트롤러는 특이하게 목적지(Goal)에 도착하기 전에 후방으로 방향을 꺾어 도착한다.

이는 TEB 컨트롤러의 특징이기도 한데, 후진도 가능하게 만듦으로 다양한 경로 생성이 가능함.

그렇다고 후진을 위한 알고리즘은 아니고, 하나의 기능으로 동작하는 것임.

확실히 DWB와 다르게 좁은 길은 잘 다님.

근데 DWB 알고리즘과 다르게 무겁다는 느낌이 큼. 경로 생성에 많은 계산량을 사용하기 때문.

(영상에선 못 다뤘지만 갑자기 주변 환경이 바뀌게 되면 우왕좌왕하는 모습을 많이 보임)


## MPPI

경험상 DWB의 장점과 TEB의 장점을 합쳐놓은 무언가..의 상위호환 느낌이었다.



https://github.com/user-attachments/assets/1a849fc4-90ca-43d4-a0f3-2ace3eeffc96



### 차세대 컨트롤러?

해당 컨트롤러는 사용해 본지 오래되진 않았다.

꽤 정확한 동작을 보여줌. 특히, 고속으로 로봇을 제어해도 잘 작동함.

그렇지만 여전히 저스팩의 컴퓨터에선 여전히 무겁다고 느껴짐. (사용하다 시뮬레이션 다운 된 적도 있음...)

앞으로 MPPI 컨트롤러에 조금 더 연구해볼 생각.

## 시시콜콜

사실 위의 과정은 nav2 입문과정이라고 생각함. 간단하게 파라메터만 바꿔주면 금방 작동하기 때문..

(물론 컨트롤러가 어떻게 어떤 과정으로 동작하는지 구조를 좀 파악해야 겠지만?)

costmap, planner와의 상관관계도 이해를 해봐야겠고.. 행동강령도 (behaviro tree) 등등.. 아뭇튼 할 건 많다.

다음 차례엔 갑자기 장애물을 생성하면 저 3개의 컨트롤러가 어떻게 동작할지, 동적 장애물을 만나면 어떻게 동작하는지 알아보려고 한다.
