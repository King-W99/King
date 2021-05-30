# 约束布局ConstraintLayout

#### 1 添加依赖

首先我们需要在app/build.gradle文件中添加ConstraintLayout的依赖，如下所示。

```bash
 implementation 'com.android.support.constraint:constraint-layout:1.1.3'
```

下面来看看相对定位的常用属性：



~~~apl
layout_constraintLeft_toLeftOf     控件左边对齐某控件的左边
layout_constraintLeft_toRightOf    控件左边对齐view2的右边
layout_constraintRight_toLeftOf    控件右边对齐view2的左边
layout_constraintRight_toRightOf   控件右边对齐view2的右边
layout_constraintTop_toTopOf        控件顶部对齐view2的顶部
layout_constraintTop_toBottomOf     控件顶部对齐view2的底部
layout_constraintBottom_toTopOf     控件底部对齐view2的顶部
layout_constraintBottom_toBottomOf   控件底部对齐view2的底部
layout_constraintBaseline_toBaselineOf  控件基准线对齐view2的基准线
layout_constraintStart_toEndOf      控件起始位置对齐view2的结束位置
layout_constraintStart_toStartOf    控件起始位置view2的起始位置
layout_constraintEnd_toStartOf     控件结束位置对齐view2的起始位置
layout_constraintEnd_toEndOf       控件结束位置对齐view2的结束位置


~~~

实操

<img src="/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-30 上午3.44.07.png" alt="截屏2021-05-30 上午3.44.07" style="zoom:50%;" />

~~~kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="button1"
          app:layout_constraintTop_toTopOf="parent"
          app:layout_constraintLeft_toLeftOf="parent"/>
    <Button
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="button2"
        android:layout_marginLeft="10dp"
         app:layout_constraintLeft_toRightOf="@+id/button1"
         app:layout_constraintTop_toTopOf="parent"/>
    <Button
        android:id="@+id/button3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="button3"
        app:layout_constraintTop_toBottomOf="@+id/button1"
        app:layout_constraintLeft_toLeftOf="parent"/>
     <Button
         android:layout_width="wrap_content"
         android:layout_height="wrap_content" 
         android:text="button4"
         app:layout_constraintTop_toBottomOf="@+id/button2"
         app:layout_constraintLeft_toRightOf="@id/button3"
         android:layout_marginLeft="10dp"/>
       
</androidx.constraintlayout.widget.ConstraintLayout>
~~~

### 偏心定位

 偏心定位由水平偏移app:layout_constraintHorizontal_bia和垂直偏移app:layout_constraintVertical_bias来设置，默认为0.5即50%（左偏移50%右偏移50%），0.3(左偏移30%右偏移70%)

~~~kotlin
<Button
        android:id="@+id/button"
        android:layout_width="100dp"
        android:layout_height="50dp"
        android:text="按钮"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent"/>
~~~

### 循环定位

官方解释：您可以以一定角度和距离约束相对于另一个窗口小部件中心的窗口小部件中心。这允许您将一个小部件放置在一个圆上

相关属性：

- `layout_constraintCircle` ：引用另一个小部件ID

- `layout_constraintCircleRadius` ：到其他小部件中心的距离

- `layout_constraintCircleAngle` ：小部件应处于哪个角度（度数，从0到360）

  

  ~~~kotlin
  <?xml version="1.0" encoding="utf-8"?>
  <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      tools:context=".MainActivity">
  
      <Button
          android:id="@+id/button1"
          android:layout_width="100dp"
          android:layout_height="100dp"
          android:gravity="center"
          android:text="buuton"
          app:layout_constraintTop_toTopOf="parent"
          app:layout_constraintLeft_toLeftOf="parent"
          app:layout_constraintRight_toRightOf="parent"
          app:layout_constraintBottom_toBottomOf="parent"/>
  <Button
      android:layout_width="100dp"
      android:layout_height="50dp"
      android:text="nihao"
      app:layout_constraintCircle="@id/button1"
      app:layout_constraintCircleRadius="100dp"
      app:layout_constraintTop_toTopOf="parent"
      app:layout_constraintLeft_toLeftOf="parent"
      app:layout_constraintBottom_toTopOf="@id/button1"
       android:gravity="center"
        app:layout_constraintCircleAngle="45"/>
  </androidx.constraintlayout.widget.ConstraintLayout>
  ~~~

  <img src="/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-30 上午4.21.40.png" alt="截屏2021-05-30 上午4.21.40" style="zoom:50%;" />

## 文本对齐

~~~apl
layout_constraintBaseline_toBaselineOf
~~~

### xml和手动结合 约束线

~~~kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline5"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_percent="0.75" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline4"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_percent="0.5" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_constraintGuide_percent="0.3" />

    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        app:layout_constraintGuide_percent="0.3" />

    <TextView
        android:id="@+id/textView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="用户名"
        app:layout_constraintBottom_toTopOf="@+id/guideline3"
        app:layout_constraintEnd_toStartOf="@+id/guideline2"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.7"/>

    <TextView
        android:id="@+id/textView3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="密码"
        app:layout_constraintBottom_toTopOf="@+id/guideline4"
        app:layout_constraintEnd_toStartOf="@+id/guideline2"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="@+id/guideline3" />

    <EditText
        android:id="@+id/editTextTextPersonName"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="请输入用户名"
        android:inputType="textPersonName"
        app:layout_constraintBottom_toTopOf="@+id/guideline3"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="@+id/guideline2"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.7" />

    <EditText
        android:id="@+id/editTextTextPassword"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:ems="10"
        android:hint="请输入密码"
        android:inputType="textPassword"
        app:layout_constraintBottom_toBottomOf="@+id/textView3"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="@+id/guideline2"
        app:layout_constraintTop_toTopOf="@+id/textView3" />

    <Button
        android:id="@+id/button2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="登录"
        app:layout_constraintBottom_toTopOf="@+id/guideline5"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="@+id/guideline4" />
</androidx.constraintlayout.widget.ConstraintLayout>
~~~

<img src="/Users/wking/Library/Application Support/typora-user-images/截屏2021-05-30 上午5.03.02.png" alt="截屏2021-05-30 上午5.03.02" style="zoom:50%;" />

