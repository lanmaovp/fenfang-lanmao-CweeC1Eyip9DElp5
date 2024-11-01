
* 首先下载OpenCV的SDK
推荐在官网下载。
官网地址：[https://opencv.org/releases/](https://github.com)
也可以在OpenCV的GitHub上现在
GitHUb链接：[https://github.com/opencv/opencv/releases](https://github.com):[slower加速器](https://jisuanqi.org)


官网下载：
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031202935851-1442293729.png)
GitHub下载
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031202958451-1175803101.png)
* 下载完成后，解压压缩包，会得到以下目录
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031203130343-1474851195.png)
其中SDK文件夹是我们要导入的目标。
* 在进行导入前，有些准备工作。
你需要配置NDK环境和CMake，将它们勾选下载下来。
下载过程很简单，勾选要配置的环境，然后同意协议，然后下一步下一步，ok就行。
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031203338507-1633346972.png)
* 接下来就是导入OpenCV了
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031203655737-253851898.png)
然后你会进入到这个页面
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031203834559-1699970579.png)
点击文件夹，选择你解压后的文件夹下的sdk文件夹。
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031203806593-2005529325.png)
如果你导入后发生了错误：A problem occurred evaluating project ‘:opencv’. Plugin with id ‘kotlin\-android’ not found.
简单处理一下即可。


	1. 选择Poject查看模式
	![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031204021448-122863864.png)
	2. 进入opencv下的build.gradle文件中。
	![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031204133429-141940761.png)
	3. 然后将开头的一行apply plugin: 'kotlin\-android'注释掉
	![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031204222454-2090422866.png)
	最后直接sync now
	![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031204323536-1773700794.png)
* 检查一下，setting.grandle
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031204527388-1842183443.png)
查看是否自动包含了opencv
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031204553908-1354333464.png)
然后检查opencv下的build.gradle
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031204709053-1841493430.png)
检查一下minSdkVersion和targetSdkVersion是否与你项目的相同。
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031204740383-1824065187.png)
APP下的build.gradle为本项目的配置，
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031204841118-1640876804.png)
查看defaultConfig下的参数，如果不同，将opencv的参数改成和项目一致。
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031204928470-952663037.png)
* 最后一步，在app下的build.gradle，翻到最下边，在dependencies中添加依赖。
![image](https://img2024.cnblogs.com/blog/2240909/202410/2240909-20241031205151942-261824512.png)
如果你的配置文件不是build.gradle.kts，那么依赖添加为这两句：



```

implementation fileTree(dir: 'libs', include: ['*.jar'])
implementation project(':opencv')


```

* 最后，验证一下OpenCV是否正常加载。



```
@Override
    protected void onResume() {
        super.onResume();
        if (!OpenCVLoader.initDebug()) {
            Log.d("openCv", "OpenCv加载失败...");
        } else {
            Log.d("openCv", "OpenCv加载成功...");
        }
    }

```

