---
layout: post
title:  "Android Animation"
date:   2017-03-01 09:00:00 +0800
categories: Android
tags: Android Animation
---
# View Animation
- xml파일에 애니메이션을 정의해두고 사용하는 방식
- xml파일에 저장해서 사용하므로 코드상에서 임의로 값을 수정이 불가능하다


### View Animation 사용법
```java
private void move(){
        // view 애니메이션 실행
        // 1. 애니메이션 xml 정의
        // 2. AnimationUtil로 정의된 애니메이션을 로드
        Animation animation = AnimationUtils.loadAnimation(this, R.anim.move);
        // 3. 로드된 애니메이션을 실제 위젯에 적용
        btnObject.startAnimation(animation);
    }
```


### translate

```xml
<?xml version="1.0" encoding="utf-8"?>
<translate xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromXDelta="0"
    android:fromYDelta="0"
    android:toXDelta="100"
    android:toYDelta="300"
    android:fillAfter="true"
    android:duration="3000">
    <!--
    fillAfter = true일 경우 애니메이션의 종료위치에 고정
                false일 경우 원래위치로 복귀(default = false)

    duration  = 시간값 = 1 / 1000 초
    -->

</translate>
```


### scale

```xml
<?xml version="1.0" encoding="utf-8"?>
<scale xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromXScale="1.0"
    android:fromYScale="1.0"
    android:toXScale="0.5"
    android:toYScale="5.0"
    android:pivotX="50%"
    android:pivotY="50%"

    android:fillAfter="true"
    android:duration="3000">
    <!--
    fillAfter = true일 경우 애니메이션의 종료위치에 고정
                false일 경우 원래위치로 복귀(default = false)

    duration  = 시간값 = 1 / 1000 초
    -->

</scale>
```


### rotate

```xml
<?xml version="1.0" encoding="utf-8"?>
<rotate xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromDegrees="0"
    android:toDegrees="270"
    android:pivotX="50%"
    android:pivotY="50%"

    android:fillAfter="true"
    android:duration="3000">
    <!--
    fillAfter = true일 경우 애니메이션의 종료위치에 고정
                false일 경우 원래위치로 복귀(default = false)

    duration  = 시간값 = 1 / 1000 초
    -->

</rotate>
```


### alpha

```xml
<?xml version="1.0" encoding="utf-8"?>
<alpha xmlns:android="http://schemas.android.com/apk/res/android"
    android:fromAlpha="1.0"
    android:toAlpha="0.0"

    android:fillAfter="true"
    android:duration="3000">
    <!--
    fillAfter = true일 경우 애니메이션의 종료위치에 고정
                false일 경우 원래위치로 복귀(default = false)

    duration  = 시간값 = 1 / 1000 초
    -->

</alpha>
```


# Property Animation
- 코드로 애니메이션을 정의하여 사용
- View 애니메이션과 달리 임의의 값을 코드에 삽입하여 위젯들마다 다르게 동작이 가능함


### Property Animation 사용법

```java
private int y = 0;
private int x = 0;
public void move1(View v){
    // 1. 대상을 정의한다 - btnGo
    // 2. 애니메이터를 설정한다
    y += 10;
    ObjectAnimator ani = ObjectAnimator.ofFloat(
            btnGo,          // 움직을 대상
            "translationY", // 애니메이션 속성
            y             // 속성값
            );
    // 3. 애니메이터를 실행한다
    ani.start();
}

public void move(View v){
    // 복합애니메이션
    y += 10;
    ObjectAnimator ani = ObjectAnimator.ofFloat(
            btnGo,          // 움직을 대상
            "translationY", // 애니메이션 속성
            y             // 속성값
    );
    x += 10;
    ObjectAnimator anX = ObjectAnimator.ofFloat(
            btnGo,          // 움직을 대상
            "translationX", // 애니메이션 속성
            x             // 속성값
    );

    //애니메이션 셋에 담아서 동시에 실행 할 수 있다
    AnimatorSet aniSet = new AnimatorSet();
    aniSet.playTogether(ani,anX);
    aniSet.setDuration(3000);

    aniSet.setInterpolator(new LinearInterpolator());
    // LinearInterpolator : 일정한 속도를 유지
    // AccelerateInterpolator : 점점빠르게
    // DecelerateInterpolator : 점점느리게
    // AccelerateInterpolator : 위 둘을 동시에
    // anticipateInterpolator : 시작위치에서 조금 뒤로 당겼다 이동
    // OvershootInterpolator : 도착위치를 조금 지나쳤다가 도착위치로 이동
    // AnticipateOvershootInterpolator : 위둘을 동시에
    // BounceInterpolator : 도착위치에서 튕김
    aniSet.start();
}
```
