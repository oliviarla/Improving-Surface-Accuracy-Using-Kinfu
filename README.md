# Kinect camera를 활용한 3D Scanning의 표면 텍스쳐 정확도 향상을 위한 기법
## Technique for improving surface texture accuracy of 3D scanning using Kinect camera

## 프로젝트 정보
📌 캡스톤디자인2 프로젝트 Capstone Design2 Project

📌 경희대학교 컴퓨터공학과 김민경 Kyung Hee Univ Computer Engineering, Minkyeong Kim


## 연구 목표
 Microsoft Kinect camera를 활용하여 정확하고 디테일한 정보까지 포함하는 3D Scanning을 일반인이 사용할 수 있을 정도로 간단하게 수행될 수 있도록 하는 것이 최종 목표이다. 
 
 이를 가능하게 하기 위해 첫 번째로 표면 디테일이 유지될 수 있는 3D스캐닝 기능을 구현하는 것이 가장 중요하다. 카메라와 물체 간의 거리를 적외선 값을 활용한 깊이 맵으로 알아낸 후, 거리가 가까울 때의 3D point 정보에 가중치를 높게 설정하여 Kinect Fusion Algorithm이 실행되도록 한다.

 두 번째, 스캐닝된 3D 정보를 저장하는 기능을 구현하여openGL, maya 등과 같은 3D 프로그램을 활용하여 확인할 수 있도록 한다. 이를 가능하게 한다면 사용자가 임의로 스캐닝된 3D 형상을 수정하거나 색상, 텍스처를 매핑하여 상업적, 개인적으로 광범위하게 사용할 수 있게 될 것이다.


## 프로젝트 구현

c++ 언어를 사용한 프로젝트이며 openCV의 rgbd, viz 모듈과 함께 main.cpp 파일이 들어있는 kinfu_example 프로젝트를 빌드하여 exe 실행파일을 만들어낸다. 만들어진 실행파일을 실행하여 ply 형식의 3D모델 파일을 얻어낼 수 있다. 얻어낸 파일은 meshlab 등의 프로그램을 사용하여 시각화할 수 있다.

 본 프로젝트에서 제안하는 알고리즘은 openCV의 rgbd 모듈 내에 있는 kinfu.cpp파일을 수정하여 구현하였다. 자세한 알고리즘의 의사 코드는 다음과 같다.

 ```python
 if (현재 depth 값의 평균)>(이전 depth값의 평균)
then value = value*0+tsdf //현재 depth값으로 대체
else
then value = value+tsdf*0 //변화 없이 유지
 ```

depth값을 평균내 물체와 카메라 간의 거리를 계산하고 계산된 depth값을 기반으로 거리가 가까우면 텍스처 값을 업데이트하고, 거리가 이전보다 멀다면 텍스처 값을 업데이트하지 않는다.

## 결론 및 기대 효과
본 연구는 비접촉 3D Scanning 방식 중 하나인 kinect camera를 활용해 Scan을 진행하고, 향상된 표면 텍스쳐를 가진 3D 모델을 도출해내는 것이다. 더욱 향상된 표면 텍스쳐를 생성하기 위해 기존 3D Scanning의 한계점인 표면 텍스쳐 평균화로 무뎌지는 현상을 개선하고 해결한다. 이러한 과정에서 kinect fusion algorithm을 참고하여 본 프로그램에서 개선된 형태로 사용된다.

본 연구의 기대효과로는 첫째, 고급 장비를 마련하기 어려운 일반인 등의 사용자들도 손쉽게 3D Scanning을 접할 수 있어 다양한 분야에서 접근성이 한 층 좋아진 상태에서 활용될 수 있다. 

둘째, 게임 개발, 제조업 등에서 좀 더 편리하고 간단하게 3D Scan을 할 수 있다. kinect 카메라로 실제 풍경을 찍어 게임의 맵을 생성할 수도 있고, 부품의 디테일한 표면을 찍어 3D 모델을 생성할 수도 있다. 추후 kinect camera의 성능이 더욱 개선된다면, 본 프로그램과 kinect camera를 이용하여 상업적으로 충분히 활용 가능한 향상된 표면 텍스쳐를 얻을 수 있을 것으로 기대된다.

## 참고 문헌
[1] 최순혁, 김영균, 류관희 (2017). 키넥트와 유니티3D를 이용한 물체 스캔 및 3D 모델 생성기법. 한국정보과학회 학술발표논문집, 1963-1965.

[2] 이병도, 김태혁 (2018). 4차 산업혁명을 위한 3D 스캐너와 BIM 데이터의 활용

[3] Michele Pirovano , Kinfu – an open source implementation of Kinect Fusion + case study: implementing a 3D scanner with PCL

[4] Shahram Izadi et al. KinectFusion: Real-time 3D reconstruction and interaction using a moving depth camera. UIST'11 - Proceedings of the 24th Annual ACM Symposium on User Interface Software and Technology. 559-568, 2011.
