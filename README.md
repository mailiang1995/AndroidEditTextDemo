# AndroidEditTextDemo


[CSDN博客](https://mailiang.blog.csdn.net/article/details/102043717) 


当跳转到带有EditText的界面后，App会自动弹出输入法，严重影响了用户体验。因此，我们有时候需要取消EditText的默认聚焦。

**方法一：**
在EditText的父控件中加上这两行代码：
```
android:focusable="true" 
android:focusableInTouchMode="true"
```
例如：
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".Method1Activity"
    android:orientation="vertical"
    android:focusable="true"				//
    android:focusableInTouchMode="true">	//

    <EditText
        android:layout_width="300dp"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:text="0123456789"
        android:textSize="20sp"/>
</LinearLayout>
```


**方法二：**
使用代码使外层组件获取焦点，代码如下：
```
View.setFocusable(true);
View.setFocusableInTouchMode(true);
View.requestFocus();//有时需要添加，谨慎起见建议全部都加
```

示例：
```
布局文件：
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:id="@+id/ll"		//
    tools:context=".Method2Activity"
    android:orientation="vertical">

    <EditText
        android:layout_width="300dp"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:text="0123456789"
        android:textSize="20sp"/>
</LinearLayout>

代码：
		LinearLayout ll = findViewById(R.id.ll);
        ll.setFocusable(true);
        ll.setFocusableInTouchMode(true);
        ll.requestFocus();
```

**方法三：**
将该窗口下的输入法隐藏起来，代码如下（仅隐藏输入法，需要在setContentView()前调用）：
```
this.getWindow()
	.setSoftInputMode(WindowManager.LayoutParams.SOFT_INPUT_STATE_ALWAYS_HIDDEN);
```
示例：
```
protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        this.getWindow()
                .setSoftInputMode(WindowManager.LayoutParams.SOFT_INPUT_STATE_ALWAYS_HIDDEN);
        setContentView(R.layout.activity_method3);
    }
```
**方法四：**
在AndroidManifest相应的Activity中添加如下代码（仅隐藏输入法）：
```
android:configChanges="keyboardHidden|orientation"
android:windowSoftInputMode="adjustResize|stateHidden"
```
示例：
```
<activity android:name=".Method4Activity"
            android:configChanges="keyboardHidden|orientation"
            android:windowSoftInputMode="adjustResize|stateHidden"/>
```
