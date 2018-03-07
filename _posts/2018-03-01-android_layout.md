---
layout: post
title:  "Android Layout"
date:   2017-03-01 09:00:00 +0800
categories: Android
tags: Android Layout
---
**Constraint Layout**  
- 레이아웃이나 위젯에 연결하여 위치값을 설정하는 레이아웃
- Frame Layout 다음으로 속도가 빠름

<img width="250" height="450" src="https://github.com/mnisdh/Android/blob/master/android/BasicLayout/capture/ConstraintLayout.png?raw=true"/>


**Frame Layout**  
- 위젯들이 중첩되는 레이아웃
- 게임 같은 어플을 개발할때 사용되며
- Layout들 중 가장 빠름

<img width="250" height="450" src="https://github.com/mnisdh/Android/blob/master/android/BasicLayout/capture/FrameLayout.png?raw=true"/>


**Linear Layout**  
- 가로 또는 세로의 단일 방향으로 위젯들을 표시하는 레이아웃
- 위젯들간의 겹침을 허용하지 않으며
- layout_weight 속성으로 레이아웃에 가중치를 둬서 디바이스 크기에 맞게 크기를 자동 조절할수 있다

<img width="250" height="450" src="https://github.com/mnisdh/Android/blob/master/android/BasicLayout/capture/LinearLayout.png?raw=true"/>


**Grid Layout**  
- 표와 같은 형태로 제공되는 레이아웃
- 컬럼이나 로우등의 속성으로 위젯의 범위를 설정할수 있으나
- 높이나 너비를 균일하게 설정하기 힘들어 사용빈도가 적음

<img width="250" height="450" src="https://github.com/mnisdh/Android/blob/master/android/BasicLayout/capture/TableLayout.png?raw=true"/>


**Relative Layout**  
- Constraint Layout 과 비슷하게 위젯에 연결하여 위치값을 설정하는 레이아웃

<img width="250" height="450" src="https://github.com/mnisdh/Android/blob/master/android/BasicLayout/capture/RelativeLayout.png?raw=true"/>
