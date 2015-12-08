# NDK Hello World

#### Development Environment
- windows 7
- Android Studio 1.4

#### Built Environment For Windows
- NDK�U���a
- http://developer.android.com/intl/zh-tw/ndk/downloads/index.html
- �i�Hcompiler c���ɮ�
- http://www.cygwin.com/install.html


- �}�� Android Srudio

- �إ߷s�� project �s�� ndktest


- �bProject��gradle.properties��󤤼W�[�@�� 
```properties     
        android.useDeprecatedNdk=true
```

- �bProject��local.properties��󤤼W�[�@��ndk�Ҧb�ؿ� ( �`�N':'�M'\'�n�i������ )�G
```properties
        ndk.dir=C\:\\Users\\Story\\AppData\\Local\\Android\\ndk
```

- ���}�b�u��C��Project Structure 

![](./picture/workspace_1.png)

- �ק�NDK location

![](./picture/workspace_2.png)





#### The Simplest Sample

- �bmain���U�s�W�@��jni����Ƨ� (compile�ɷ|�۰ʶi�J�W�٬�jni����Ƨ�)

![](./picture/workspace_3.png)
- �b���U�Ф@��C���H��mk��

- C��󪺼��g

```C
#include <string.h>
#include <jni.h>
/*Jstring ����^�� ,�]�i�H�� void , jint ���� ����
 C��󤤤�k���R�W�W�h
 Java_Package�W�l_Activity�W�l_��k�W
 */
jstring  Java_com_ndktest_MainActivity_stringFromJNI( JNIEnv* env, jobject thiz )
{
    return (*env)->NewStringUTF(env, "HelloWorld! ");
}
```

- mk�ɪ����g

```mk
#FileName:Android.mk
#Description:makefile of Helloworld
#Android.mk ��󭺥������w�q�nLOCAL_PATH�ܶq�Amy-dir�O�ΨӪ�^��e���|
LOCAL_PATH := $(call my-dir)

#CLEAR_VARS�ѽsĶ�t�δ��ѡA���w��GNU MAKEFILE���A�M���\�hLOCAL_XXX�ܶq
include $(CLEAR_VARS)

#�W�٥����O�ߤ@���A�ӥB���]�t����Ů�
LOCAL_MODULE    := HelloWorld

#�C�X�����ǻ���sĶ����c���
LOCAL_SRC_FILES := HelloWorld.c

#BUILD_SHARED_LIBRARY��ܽsĶ�ͦ��@�ɮw�A�O�sĶ�t�δ��Ѫ��ܶq
include $(BUILD_SHARED_LIBRARY)
```

- �}�� app Module �� build.gradle�A�b dependencies �϶��[�J�A�ҡG

```gradle
  defaultConfig {
        applicationId "com.ndktest"
        minSdkVersion 15
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
        //�ݭn��Jndk module
        ndk {
            moduleName "HelloWorld"
        }
    }
```


- MainActivity����g

```java
package com.ndktest;

import android.app.Activity;
import android.os.Bundle;
import android.widget.TextView;

public class MainActivity extends Activity {

    public void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);


        TextView tv = new TextView(this);
        tv.setText( stringFromJNI() );
        setContentView(tv);
    }

    //       �ŧi��k
    public native String  stringFromJNI();



    //  �R�A���JSo�w
    static {
        System.loadLibrary("HelloWorld");
    }
}

```
- ���}cygwin�i�J�M��main����m
- �å��W�A��ndk�̪�ndk-build

![](./picture/workspace_4.png)

- ����APP�����G

![](./picture/workspace_5.png)

#### Contributors
Lyon Lin

#### Troubleshooting
