# ApiDemos
Compileable ApiDemos based on android 22.

#### 【MacOS High Sierra】Android Studio 3.0.1 构建Android-22版本ApiDemos项目
	
#### 参考文档

|序号|名称|链接地址|备注|
|----|----|----|----|
|1|Android Gradle Plugin Release Notes|<https://developer.android.com/studio/releases/gradle-plugin.html#updating-gradle>|详细描述了Android Gradle Plugin的版本变更，以及每个版本对Gradle版本和Build Tools Version的依赖关系|
|2|SDK Build Tools Release Notes|<https://developer.android.com/studio/releases/build-tools.html>|记录了Build Tools 各个版本信息，包括版本号等|
|3|Support v4 library Revision archive|<https://developer.android.com/topic/libraries/support-library/rev-archive.html>|记录了Support v4包的修改进化过程，版本信息等修改升级档案|
|4|Migrate to Android Plugin for Gradle 3.0.0|<https://developer.android.com/studio/build/gradle-plugin-3-0-0-migration.html#new_configurations>|详细介绍了如何升级Android Gradle plugin到3.0.0版本，解决遇到的问题，版本冲突等|

#### 一、环境准备

> 1. 操作系统					= MacOS High Sierra 10.13.2
> 1. JDK 版本 				= <font color="red">1.8.0_40</font>    
> 2. Android Studio 		= <font color="red">3.0.1</font>    
> 3. ApiDemos源代码		   = 你的Android SDK目录下/samples/<font color="red">android-22</font>/legacy/ApiDemos    
    						 （如果没有，请使用SDKmanager下载）

#### 二、关键概念

	1. Android Studio
	2. Gradle
	3. Gradle Wrapper
	4. Gradle distributionUrl
	5. Gradle DSL method
	6. Android Gradle Plugin
	7. buildToolsVersion
	8. compileSdkVersion

#### 三、Android Studio 3.0.1中创建新项目(或者转化Eclipse项目)采用的默认配置

	1. 由于AndroidStudio3.0.1默认使用Android Gradle plugin 3.0.0+版本，而Android Gradle 
	   plugin 3.0.0+需要依赖于Gradle 4.1+版本,并且要求Build Tools 26.0.2 or higher.
	   
	2. Gradle plugin 3.0.0+中会自带一个最低可使用版本的Build Tools，只要使用Gradle 
	   plugin 3.0.0+版本就不再需要手动指定Build Tools(buildToolsVersion)了。

#### 四、Android Studio 3.0.1 导入Android-22中的ApiDemos项目

|步骤|类型|示例|
|----|----|----|
|1|操作|Android Studio中导入eclipse项目，自动生成gradle配置文件。![import eclipse project from android studio](http://upload-images.jianshu.io/upload_images/6322932-0b338edd3844b53b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|2|操作|选择我们准备好的Android-22 ApiDemos源码目录。![select apiDemos project](http://upload-images.jianshu.io/upload_images/6322932-ba25dcbb919aeaae.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|3|操作|设置Project要导入的目标目录![select project import directory](http://upload-images.jianshu.io/upload_images/6322932-6566cd5174032957.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|4|操作|保持默认导入设置不变![keep the import settings default](http://upload-images.jianshu.io/upload_images/6322932-4622f3b345154fc8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|5|错误|项目导入之后，编译项目，开始解决编译错误。<font color="red">编译错误1：为preference_switch文件增加.xml后缀</font>![first build apiDemos and resolve first error](http://upload-images.jianshu.io/upload_images/6322932-aba5c1805fca4fc2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|6|错误&操作|<font color="red">编译错误2:缺少support v4 包，需要导入正确版本的support v4 包，默认通过module settings 导入的都是最新的版本，有可能不兼容。需要导入和buildToolsVersion 相匹配的v4 包。</font>![need support v4 package](http://upload-images.jianshu.io/upload_images/6322932-220d98de8fed9f90.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)添加V4包：项目右键-->open module settings-->选择modules中的app-->选择Dependencies-->点击左下角 "+"号-->选择support v4包-->点击OK-->OK关闭module settings界面。导入Support v4包![add support v4 package](http://upload-images.jianshu.io/upload_images/6322932-c26ed0b17c8845a1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|7|操作|添加V4包：项目右键-->open module settings-->选择modules中的app-->选择Dependencies-->点击左下角 "+"号-->选择support v4包-->点击OK-->OK关闭module settings界面。![add support v4 package](http://upload-images.jianshu.io/upload_images/6322932-c26ed0b17c8845a1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)最新support v4被放置在了google()仓库中，需要添加google()仓库支持,点击图中错误<font color="red">Add GoogleMaven repository and sync project</font>之后会添加google()仓库到项目中![最新support v4被放置在了google()仓库中，需要添加google()仓库支持](http://upload-images.jianshu.io/upload_images/6322932-5bfb4f262cd5eb53.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|8|错误|点击上图中错误Add GoogleMaven repository and sync project之后会添加google()仓库到项目中，再编译![点击上图中错误Add GoogleMaven repository and sync project之后会添加google()仓库到项目中，再编译](http://upload-images.jianshu.io/upload_images/6322932-49e782c5c683315c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|9|操作|修改minSdkVersion为14，再编译![修改minSdkVersion为14](http://upload-images.jianshu.io/upload_images/6322932-a9a01ced8b7aefad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|10|操作|[注释掉mms相关代码，因为mms编译需要内核。注释掉所有错误地方![注释掉mms相关代码，因为mms编译需要内核](http://upload-images.jianshu.io/upload_images/6322932-6948d9006168d343.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)注释代码2，注释掉所有错误地方![注释掉mms相关代码，因为mms编译需要内核2](http://upload-images.jianshu.io/upload_images/6322932-3dd68d67e0d2f94a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|11|错误&操作|查看android-22和android-23源码得知：Notification.setLatestEventInfo方法在android-23以上被删除了，所以需要修改compileSdkVersion=22![Notification.setLatestEventInfo方法在android-23以上被删除了，所以需要修改compileSdkVersion=22](http://upload-images.jianshu.io/upload_images/6322932-6a261ead95f34076.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)适合compileSdkVersion=22的BuildToolsVersion列表，从中得知22.0.0和22.0.1适合，我们选择22.0.1![适合compileSdkVersion=22的BuildToolsVersion列表](http://upload-images.jianshu.io/upload_images/6322932-de3cd64c3098fa0f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)适合buildTools 22.0.1 的Support library 版本，我们选择22.2.1![适合buildTools 22.0.1 的Support library 版本](http://upload-images.jianshu.io/upload_images/6322932-c39823ac50e4dbdb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 修改build.gradle文件：<font color="red">compileSdkVersion=22 buildToolsVersion=22.0.1 support v4 版本为 22.2.1</font>|
|12|错误|Android Gradle Plugin 版本3.0.1要求buildToolsVersion至少26.0.1，所而这里buildToolsVersion已经不能升高，所以只能奖励gradle plugin 版本来匹配buildToolsVersion = 22.0.1![gradle plugin 版本对于buildToolsVersion=22.0.1来说太高了，必须降低](http://upload-images.jianshu.io/upload_images/6322932-3a9359e0998dabaa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)修改gradle plugin版本![适合buildToolsVersion=22.0.1的gradle plugin版本](http://upload-images.jianshu.io/upload_images/6322932-9247917d1db8f3f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)修改Gradle版本来匹配gradle plugin版本![修改Gradle版本来适合Gradle plugin 版本](http://upload-images.jianshu.io/upload_images/6322932-9a602a726a0ed251.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)Gradle plugin降级之后删除不支持的google（）仓库![Gradle plugin版本降低之后，需要移除google()仓库，因为低版本不支持](http://upload-images.jianshu.io/upload_images/6322932-4400ad9ee45b4c86.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)Gradle plugin降级之后修改implementation为compile![替换implementation为旧版本complie方法](http://upload-images.jianshu.io/upload_images/6322932-547cd93119c5bbdc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|
|13|错误&操作|注释掉错误行代码,api 23 才加入的方法,方然也可以继续修改编译环境来匹配api 23.![注释掉错误行代码，api 23 加入的方法](http://upload-images.jianshu.io/upload_images/6322932-ea45a6cf84b7858b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)![api 23加入的方法](http://upload-images.jianshu.io/upload_images/6322932-424edd9cdd9a0051.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
|14|错误|可能出现的错误，如果出现，按照错误提示修改成res-auto名称空间即可。![Gradle项目中自定义View都使用res-auto名称空间](http://upload-images.jianshu.io/upload_images/6322932-9f78fd5f495ba823.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)|


<font color="red">至此，ApiDemos已经可以运行成功了。</br>
代码已经上传至Github：<https://github.com/Farubaba/ApiDemos>
</font>

