﻿# 医学图像算法unet/unet++的darknet实现开源代码
乐山五通朱伟(lswtzw)的远程开源代码库,主要是医学图像算法方面的开源代码(总计不到8MB)


运行环境和运行条件:
win8/win10 -----(最好是有4GB显存以上的独立显卡,并安装好了CUDA开发环境,未安装只能用CPU版本);
本项目需要先安装opencv320-----(最好是opencv320,与开发机保持一致,其它版本估计也行);
最后:请把opencv320下的opencv_world320.dll复制到可执行文件目录下(darknet/build/darknet/x64/);
     首次使用建议先跑通darknet_no_gpu.exe这个版本(CPU版本,配置要求低).


发行版本说明:
本开源项目是基础于AlexeyAB大神的Windows版的darknet框架加改的,所以如果你的电脑已配置好了AlexeyAB大神的版本,只要替换掉:
darknet.h,darknet.c,data.h,data.c,parser.c,并增加unet.h,unet.c这几个文件就可以了.用户可按需修改主文件unet.c,
darknet框架的windows版本安装方法请百度查CSDN网文:"win10下配置yolov3","window下安装配置darknet"等.
另外,本开源项目也参考了网友:阳光玻璃杯 的"图片语义分割"的博文,并在他的git关键代码和配置的基础上改出了本开源代码,他用的是segnet网络模型.


使用说明:
因为darknet.exe是在我的电脑上编译出的gpu版本,可能在你的电脑上启不动.需要重新编译源码.
如果你想先快速上手试试,可以先用:darknet_no_gpu.exe这个可执行文件.
把下载好的darknet和unet_data两个目复制到你的电脑c:根目录下,可以少些路径配置.
测试的话可以先执行unet_data目录下的几个批处理文件.

一.文件和目录配置：
    1.darknet目录是项目源码,用vs2015或以上打开它的.sln工程文件,在build子目录下.
    2.unet_data目录是调用批处理/配置文件/图像集/权重模型文件的存放主目录,核心是data.txt:
      这个文件是各种路径的配置文件,注意修改对应的盘符!默认初始值是在C盘根目录下.
      上面这个和darknet框架上的传统data配置文件差不多,用法略有改动.
    3.color目录下放的是彩色训练图像和对应配置文件.
    4.backup目录一般用于存放训练出的模型文件.

二.网络模型配置：
    unet_cfg.txt/unet_cfg++.txt这两个文本文件就是网络模型配置文件
    (完全同于darknet格式的cfg),注意:不要另存为UTF-8编码(有时改了会出错),
    就用windows记事本默认的ANSI编码来保存.(windows回车换行模式)
    配置文件可以自由使用各种网络模型,如segnet也是可以的.这个我放在了darknet的cfg目录下.

三.关于数据增广:
    因为label(蒙版二值图像)和image是按文件名称,进行的一一对应关系,如果产生平移或挤压等变化时,
    两者要同步进行,所以须要另外想办法用其它工具软件或程序实现,结果图直接加到训练模板中.

四.结束训练的时机:
    根据笔者的经验,avg_loss的值,训练到100以下,就差不多了可以停了.
    总之我的GT750显卡4GB显存,10张模板用了4个小时以上,训练unet++时间比unet要长得多.
    如果训练24小时都不行,一般是模板图像有问题,存在矛盾模板.
    根据笔者的经验,GPU识别的速度一般在2秒以内.视图像大小和网络复杂度而定.    
    启动训练后,可以用nvidia-smi查看显存占用,如果余得多,可以增大cfg的[net]的batch的值或图像宽高.

五.调用接口:
    为方便C#和JAVA等的弱耦合调用,提供了一次性载入模型和多次性按需识别的调用接口,请参见项目中包含的说明文档.


