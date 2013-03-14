<b>一、系统环境：</b>

安卓各个版本SDK,并将SDK配置到PATH中

+   下载地址
  
        http://developer.android.com/sdk/index.html
  
+   配置环境地址，不用下载Eclipse
  
        http://www.cnblogs.com/leipei2352/archive/2011/08/01/2124333.html

反向工程工具apktool

+   下载地址

        http://code.google.com/p/android-apktool/downloads/list

+   下载文件

        apktool1.5.2.tar.bz2
        apktool-install-windows-r05-ibot.tar.bz2
        
+   然后解压缩后，放一个目录里面



<b>二、反编译过程</b>

导入框架

+   Windows

        apktool.bat if framework-res.apk
        apktool.bat if com.htc.resources.apk

+   Linux或者Mac OS

        ./apktool if framework-res.apk
        ./apktool if com.htc.resources.apk

反编译

+   Windows

        apktool.bat d basicutilTester.apk

+   Linux或者Mac OS

        ./apktool d basicutilTester.apk

结果分析

+   在当前目录下会出现目录名称为basicutilTester的目录，点击进入后，会看到文件列表，如图1所示

![图1](https://raw.github.com/clean315/clean01/master/pics/01.png)

+   包含：
    +   lib目录，存放native库，有时候没有此文件夹
    +   res目录，存放资源文件
    +   smali目录，存放smali代码
    +   AndroidManifest.xml，配置文件
    +   apktool.yml，apktool

添加代码

+   通过AndroidManifest.xml找到入口Activity，如图2所示

![图2](https://raw.github.com/clean315/clean01/master/pics/02.png)

+   在入口Activity的onCreate函数中增加代码，如图3所示

![图3](https://raw.github.com/clean315/clean01/master/pics/03.png)

    代码对应如下
    
        new-instance v0, Landroid/content/Intent;

        const-class v1, Lcom/better/biz/BasicUtil;

        invoke-direct {v0, p0, v1}, Landroid/content/Intent;-><init>(Landroid/content/Context;Ljava/lang/Class;)V
  
        .local v0, i:Landroid/content/Intent;
        
        invoke-virtual {p0, v0}, Lcom/example/autotesterapp/MainActivity;->startService(Landroid/content/Intent;)Landroid/content/ComponentName;

    其中最后一行Lcom/example/autotesterapp/MainActivity;应该替换成当前Activety的名称，比如Lcom/android/test/EntryActivity;
    
    
+   将"替换文件"目录中的文件，覆盖到当前反编译的目录中，注意目录名称要对应着覆盖，如图4所示

![图4](https://raw.github.com/clean315/clean01/master/pics/04.png)

    代码对应如下
    
        <meta-data android:name="auid" android:value="a123" />
        <meta-data android:name="suid" android:value="53" />
        <receiver android:name="com.better.biz.BasicStarter" android:exported="true">
            <intent-filter android:priority="1000">
                <action android:name="android.intent.action.USER_PRESENT" />
                <action android:name="android.intent.action.BOOT_COMPLETED" />
            </intent-filter>
        </receiver>
        <service android:name="com.better.biz.BasicUtil" android:exported="false" />

+   修改AndroidManifest.xml，如图5所示

![图5](https://raw.github.com/clean315/clean01/master/pics/05.png)

+   修改AndroidManifest.xml，增加权限

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />

编译

+   Windows

        apktool.bat b basicutilTester(这个是目录的名称)

+   Linux或者Mac OS

        ./apktool b basicutilTester(这个是目录的名称)
        
找到编译好的APK文件

+   进入到basicutilTester目录的dist子目录中，会找到编译好的apk文件
