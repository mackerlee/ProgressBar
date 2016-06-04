# ProgressBar

android 61 lesson
1.ProgressBar进度条:可以分为对话框进度条/标题进度条/自定义进度条,它也是继承类View类,也可分为确定进度和不确定进度.一般用于耗时比较                     长，需要用户等待的进程中.
    --a.两种展示方式：表盘形式（普通/小/大）和条形填充形式,通过layout中定义ProgressBar组件的style属性类设置其展示方式;
    --b.ProgressBar的XML中重要属性：
      --android:max:进度条长度最大值，配合条形填充方式使用;
      --android:progress:设置进度条当前进度值;
      --android:secondaryProgress:第二进度条进度值;
      --android:progressBarStyle:设置进度条样式,表盘或条形;
      --android:progressBarStyleHorizontal:设置水平样式
    --c.ProgressBar的重要方法:
      --getMax():返回这个进度条的范围的上限;
      --getProgress():返回当前进度值;
      --getSecondaryProgress():返回次要当前进度值;
      --incrementProgressBy(int diff):指定增加的进度即步长;
      --isIndeterminate():指示当前进度条是否在不确定模式下;
      --setIndeterminate(boolean indeterminate):设置为不确定模式;
      --setVisibility(int v):设置该进度条是否可视.

2.ProgressBar实例：在res->layout->activity_main.xml中：
  <?xml version="1.0" encoding="utf-8"?>
  <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent"
      android:paddingBottom="@dimen/activity_vertical_margin"
      android:paddingLeft="@dimen/activity_horizontal_margin"
      android:paddingRight="@dimen/activity_horizontal_margin"
      android:paddingTop="@dimen/activity_vertical_margin"
      tools:context="com.example.mackerlee.android_61.MainActivity">
  
      //--默认进度是表盘型
      <ProgressBar
          android:id="@+id/progressbar01"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          />
  
      <ProgressBar
          //--通过该属性设置表盘样式
          style="?android:attr/progressBarStyleSmall"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:id="@+id/progressBar02"
          android:layout_below="@+id/progressbar01" />
  
      <ProgressBar
          //--设置为条形
          style="?android:attr/progressBarStyleHorizontal"
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
          android:id="@+id/progressBar03"
          android:layout_below="@id/progressBar02"
          //--设置当前进度值
          android:progress="50"
          //--设置第二进度值，类似视频播放中的缓存进度
          android:secondaryProgress="60"
          //--设置最大进度值
          android:max="100" />
  
      //--设置两个按钮来控制条形进度条，表盘型的不需要
      <Button
          android:id="@+id/button01"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_below="@id/progressBar03"
          android:text="增加"/>
  
      <Button
          android:id="@+id/button02"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_toRightOf="@id/button01"
          android:text="减少"/>
  
  </RelativeLayout>

      
