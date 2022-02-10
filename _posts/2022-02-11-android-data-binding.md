---
layout: post
title: "안드로이드에서 Data Binding 사용하기"
categories: android
---

자바 코드에서 레이아웃에 있는 View를 가져오기 위해 보통 쓰는 `findViewById`보다 편리한
Data Binding을 사용하기 위한 방법이다.

## build.gradle 설정

app내의 build.gradle에 다음과 같이 dataBinding 블럭을 추가한다.

```groovy
android {
    ...
    dataBinding {
        enabled = true
    }
    ...
}
```

## layout xml 설정
최상위 Layout바깥에 layout태그를 만들어주고,
원래 Layout태그 속성의 xmlns태그들을 아래와 같이 layout태그로 빼준다.
```xml
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">
    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">

        <TextView
            android:id="@+id/textview_test"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Hello World!"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintLeft_toLeftOf="parent"
            app:layout_constraintRight_toRightOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

    </androidx.constraintlayout.widget.ConstraintLayout>
</layout>
```

## Data Binding 사용
아래는 Kotlin에서 Data Binding을 사용한 예이다.

```kotlin
...

class MainActivity : AppCompatActivity() {
    private lateinit var binding: ActivityMainBinding
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        binding = DataBindingUtil.setContentView(this, R.layout.activity_main)

        binding.textviewTest.text = "modified text"
    }
}```

`DataBindingUtil.setContextView`메소드는 기존의 `setContextView`를 실행하고 DataBinding을 반환한다.
