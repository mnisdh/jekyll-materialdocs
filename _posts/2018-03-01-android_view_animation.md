---
layout: post
title:  "Android View Animation"
date:   2017-03-01 09:00:00 +0800
categories: Android
tags: Android View Animation
---
**View Animation**  
- xml파일에 애니메이션을 정의해두고 사용하는 방식
- xml파일에 저장해서 사용하므로 코드상에서 임의로 값을 수정이 불가능하다

code :
{% highlight java linenos %}
private void move(){
    // view 애니메이션 실행
    // 1. 애니메이션 xml 정의
    // 2. AnimationUtil로 정의된 애니메이션을 로드
    Animation animation = AnimationUtils.loadAnimation(this, R.anim.move);
    // 3. 로드된 애니메이션을 실제 위젯에 적용
    btnObject.startAnimation(animation);
}
{% endhighlight %}


translate :
{% highlight xml linenos %}
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
{% endhighlight %}


scale :
{% highlight xml linenos %}
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
{% endhighlight %}


rotate :
{% highlight xml linenos %}
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
{% endhighlight %}


alpha :
{% highlight xml linenos %}
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
{% endhighlight %}