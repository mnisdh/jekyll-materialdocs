---
layout: post
title:  "Android Property Animation"
date:   2017-03-01 09:00:00 +0800
categories: Android
tags: Android Property Animation
comments: 1
---
**Property Animation**  
- 코드로 애니메이션을 정의하여 사용  
- View 애니메이션과 달리 임의의 값을 코드에 삽입하여 위젯들마다 다르게 동작이 가능함  

code :
{% highlight java linenos %}
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
{% endhighlight %}