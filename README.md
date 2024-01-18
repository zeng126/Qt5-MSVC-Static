# **Qt5-MSVC-Static**

Set of tools to build Qt5 static libs on Windows.  
There are some binaries available [here](https://ci.appveyor.com/project/fpoussin/qt5-msvc-static/build/artifacts)

## Dependencies

 - MSVC 2013-2017 with WDK 8.1/10+ (Community edition works fine)
 - Qt 5.8.0+ sources (Works with previous version with minor edits)
 - Python 2.7 (https://www.python.org/downloads/windows/) (for Qt)
 - Perl (http://strawberryperl.com/) (for OpenSSL)
 - OpenSSL 1.0.x/1.1.x

Make sure *Python*, *Perl* are all in the *PATH* or add them to *PATH* in options.bat  

**NTFS** case sensitivity needs to be turned **OFF** in the parent folder before cloning.  
You can check with this command:  
```
fsutil file queryCaseSensitiveInfo .
```
If you need to disable it:
```
fsutil file setCaseSensitiveInfo . disable
```

You can check the official documentation here:  
http://doc.qt.io/qt-5/windows-requirements.html  
http://doc.qt.io/qt-5/windows-building.html  

## Usage

First, we need to check the folder names are correct in *tools/options.bat*  

Open a VS command prompt in the repo's root.  
The links for the prompts are "*VS2017_Win32/64*"

You will need to run *qt.bat* from the VS command prompt.

Run these commands in the following order to build Qt:
 - qt download
 - qt openssl
 - qt setup
 - qt build

## Additional Qt modules

Those can be downloaded and installed by the script.  
If you want to install extra Qt modules like qtscript or webkit:
- Run this command: *qt extra [module-name]*
- You need to run it once per module

You obviously have to do that after installing Qt.
Modules can be found here: http://download.qt.io/official_releases/qt/5.12/5.12.1/submodules/

## Configuration

Only release libs are enabled by default. 
You can add the debug libs or use the official sdk libs for debugging.
You can add extra build options for Qt by editing the *EXTRABUILDOPTIONS* var in options.bat


You can check the official configuration guide here:
http://doc.qt.io/qt-5/configure-options.html


Qt一共有几百个版本，关于如何选择Qt版本的问题，一般保留四个版本.

为了兼容Qt4用4.8.7，最后的支持XP的版本5.7.0，最新的长期支持版本比如5.15，最高的新版本比如5.15.2。

强烈不建议使用4.7以前和5.0到5.3之间的版本（Qt6.0到Qt6.2之间、不含6.2的版本也不建议，很多模块还没有集成），太多bug和坑，稳定性和兼容性相比于之后的版本相当差，能换就换，不能换睡服领导也要换。

如果没有历史包袱建议用5.15.2，目前新推出的6.0版本也强烈不建议使用，官方还在整合当中，好多类和模块暂时没有整合，需要等到6.2.2版本再用。

Qt4.8.7是Qt4的终结版本，是Qt4系列版本中最稳定最经典的（很多嵌入式板子还是用Qt4.8），其实该版本是和Qt5.5差不多时间发布的。参考链接 https://www.qt.io/blog/2015/05/26/qt-4-8-7-releasedhttps://blog.qt.io/blog/2015/07/01/qt-5-5-released/

Qt5.6.3最最后支持xp系统的长期支持版本，Qt5.7.0是最后支持xp系统的非长期支持版本（有可能有极少数函数不支持，个人没遇到过）。

Qt5.12.3是最后提供mysql数据库插件的版本，往后的版本需要自行编译对应的mysql数据库插件，官方安装包不再提供。

Qt5.12.5是最后样式表性能最高的版本，经过酷码大佬查阅代码发现此后版本的样式表源码中为了修复一个bug做了循环嵌套设置，导致性能急剧下降，界面越多性能暴降10倍以上。

Qt5.14.2是最后提供二进制安装包的版本，后面的版本都需要在线安装。

Qt5.15系列是最后支持win7的版本，后面的Qt6系列版本需要更改源码编译才能支持win7，这对于小白来说难于上青天。

Qt6.0/6.1版本其实也是支持win7的，但是因为缺失太多模块，而且BUG成山，大佬说了狗都不用，所以使用此版本没意义。

Qt6不支持win7，是说开发阶段和运行阶段都不支持，无论开发阶段还是运行阶段你都需要Qt的库，只要是Qt的库不支持，到哪里也不支持。

新版的qtc7由于采用Qt6编译，所以也只能在win10及以上运行，意味着你要用新的qtc7+Qt5做开发也必须用win10及以上。

欢迎各位补充，比如哪个版本以后商用需要收费之类的，貌似用Qt4，在不更改Qt本身源码，动态库发布程序，法律风险小一些？

Qt官方除了Qt库一直在升级外，对应的集成开发环境也在更新升级，一般会选用最新的Qt库编译新版本，要注意的是，有些人安装的旧版本的qtc，加载比较高版本的Qt库，很容易出现报错提示 Project ERROR: Cannot run compiler ‘g++’. Maybe you forgot to setup the environment? 之类的，一般是版本跨度过大，比如用Qt5.5附带的qtc加载Qt5.9的库，导致有些环境识别不到，可能是qtc在新版本中对某些识别处理规则有变动。所以一般建议可以用新的qtc加载旧的Qt库，不建议旧的qtc加载新的Qt库。
