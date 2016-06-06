# ProgressBar

android 61-63 lesson
1.ProgressBar进度条:可以分为对话框进度条/标题进度条/自定义进度条,它也是继承类View类,也可分为确定进度和不确定进度.一般用于耗时                     比较长，需要用户等待的进程中.
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
    --d.标题进度条：设置标题进度条必须在setContentView方法之前,即MainActivity.java中setContentView(R.layout.activity_main)之前
                    requestWindowFeature(Window.FEATURE_INDETERMINATE_PROGRESS);
                    设置显示标题进度条是否可见
                    setProgressBarIndeterminateVisibility(true);

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
          android:text="增加"
          //--设置按钮响应事件
          android:onClick="onClick"/>
  
      <Button
          android:id="@+id/button02"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:layout_toRightOf="@id/button01"
          android:layout_below="@id/progressBar03"
          android:text="减少"
          //--设置按钮响应事件，与上面是同一个函数，通过判断id值进行不同操作
          android:onClick="onClick"/>
  
    //--设置一个按钮用于弹出显示进度条对话框,默认是表盘形式，如果要用水平样式要在代码中设置
    <Button
        android:id="@+id/button03"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="显示对话框进度条"
        android:layout_below="@id/button01"
        android:onClick="onClick"/>
    
    //--设置一个按钮用于用静态方法方式弹出显示进度条
    <Button
        android:id="@+id/button04"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="用静态方法实现对话框进度条"
        android:layout_below="@id/button03"
        android:onClick="onClick"/>
        
    //--创建一个自定义的进度条
    <ProgressBar
        android:id="@+id/progressBar04"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        //--将该进度条与res->drawable中定义的自定义进度条的pdzdy.xml关联起来
        android:indeterminateDrawable="@drawable/pdzdy"/>
  </RelativeLayout>
  
  在app->java->包名->MainActivity.java中：
  package com.example.mackerlee.android_61;

    import android.app.ProgressDialog;
    import android.support.v7.app.AppCompatActivity;
    import android.os.Bundle;
    import android.view.View;
    import android.widget.Button;
    import android.widget.ProgressBar;
    
    public class MainActivity extends AppCompatActivity {
    
        private Button btnIncrement,btnDecrement;
        private ProgressBar pb;
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            //--设置标题栏进度条：不确定进度条，必须在setContentView方法之前设置调用
            requestWindowFeature(Window.FEATURE_INDETERMINATE_PROGRESS);
            setContentView(R.layout.activity_main);
            setProgressBarIndeterminateVisibility(true);    //设置该标题进度条可见,放在setContentView之下
            btnIncrement = (Button)findViewById(R.id.button01);
            btnDecrement = (Button)findViewById(R.id.button02);
            pb = (ProgressBar)findViewById(R.id.progressBar03);
        }
    
        public void onClick(View view){
            switch (view.getId()){
                case R.id.button01:
                        //--每点击一次增加按钮，进度值加5
                        pb.incrementProgressBy(5);
                        //--第二进度值每点一次加5
                        pb.incrementSecondaryProgressBy(5);
                    break;
                case R.id.button02:
                        //--每点击一次减少按钮进度值减5，同一个函数，但用负数值
                        pb.incrementProgressBy(-5);
                        pb.incrementSecondaryProgressBy(-5);
                    break;
                case R.id.button03:
                    //--创建一个进度条对话框组件方法一：new一个ProgressDialog
                    ProgressDialog pd = new ProgressDialog(this);
                    pd.setTitle("下载进度");        //对话框标题
                    pd.setMessage("下载中...");     //对话框显示文字
                    //--设置为水平样式进度条
                    pd.setProgressStyle(ProgressDialog.STYLE_HORIZONTAL);
                    pd.setMax(100);                  //设置进度条最大值为100
                    pd.setProgress(20);              //设置进度条当前值为20，以上两个只有在水平形式下才有意义
                    pd.show();                       //对话框显示，默认是表盘模式 
                    break;
                case R.id.button04:
                    //--创建一个进度条对话框组件方式二：静态方法实现
                    ProgressDialog.show(this,"下载进度--静态方式","下载中...",true); //true参数表示是不确定的
                    break;
                default:
                    break;
            }
        }
    }

3.自定义进度条：通过一个图片来自定义进度条，首先自己找到一副进度条图片如jdt.jpg：
    --a.在res/drawable/下创建一个layer-list的xml文件，在该文件中定义jdt.jpg图片的旋转方式,如角度/方向等等
    --b.设置ProgressBar的android:indeterminateDrawable属性来指定该文件
    --c.在res->drawable中定义自定义进度条的pdzdy.xml,如下：
    <?xml version="1.0" encoding="utf-8"?>
    //--设置一个图层列表xml文件
    <layer-list xmlns:android="http://schemas.android.com/apk/res/android">
        <item>
            //--与自定义图片jdt.jpg关联作为进度条的图片
            <rotate android:drawable="@drawable/jdt"
                    android:fromDegrees="0"  //从0度开始旋转
                    android:toDegrees="360"  //一直旋转到360度
                    android:pivotX="50%"     //旋转的中心轴的x坐标，50%即表示中间位置
                    android:pivotY="50%"/>   //旋转的中心轴的y坐标
        </item>
    </layer-list>
    剩余部分代码在上面
