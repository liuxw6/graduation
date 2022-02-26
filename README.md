# graduation

根据教程完成了大部分的步骤，以下是一些重要的问题解决方法：

1、无法下载labelImg进行标注：

开始使用了Ubuntu专用的指令下载，配置过程相当繁琐且最终也没有解决，在帮助下使用了以下方法在虚拟环境下安装成功了。

![img](file:///C:\Users\86186\AppData\Roaming\Tencent\Users\2016993189\QQ\WinTemp\RichOle\VE3C}[(3{051NWI]563E7)A.png)

2、GPU无法配置/开启：

对于markfile文件中LDFLAGS+= -L/usr/local/cuda-11.3/lib64 -lcuda -lcudart -lcublas -lcarand

报了——找不到lcuda的错，最后直接在markfile中将 -lcuda删除竟然解决了问题



cuda过高的版本淘汰了一部分ARCH版本，注释掉了一部分版本，选取了86版本，使用的是11.3的cuda版本。本人了解到的是超过cuda10.0，ARCH30的版本就不再使用。



训练模式下默认batch=64，本人电脑性能不足以支持这么高的batch_size，调试后最高支持batch=2，不过弊端很大，在少量样本下，很难训练出好的权重，权重的应用范围很有限。

使用了dataenhance软件对图片进行数据增强，可以近似达到提高batch的效果。



训练图片过大，调小分辨率即可



3、yolov3预训练模型下载慢

直接从官方外网下载需至少8小时，因此寻找了百度网盘资源进行下载。



4、训练完后测试出现默认类别名字

原本使用以下代码：



![img](file:///C:\Users\86186\AppData\Roaming\Tencent\Users\2016993189\QQ\WinTemp\RichOle\HT6YD54@}GHU}OI1CN7TC_4.png)

修改成以下格式

![img](file:///C:\Users\86186\Documents\Tencent Files\2016993189\Image\C2C\D51228A9E8A18ED1D63CB4CB637081D9.jpg)

尤其注意要将存放自己设置的类别名字的路径加入



5、训练图片格式受限

默认只能用jpg格式图片训练。

如果是.jpeg格式可以批量修改后缀名，使用以下方式

![img](file:///C:\Users\86186\AppData\Roaming\Tencent\Users\2016993189\QQ\WinTemp\RichOle\_%IVYGDE`DR~NGF5VRGYQT4.png)



如果是其他格式，则需要更改my_lables.py文件，查找出jpg修改成你想要训练的图片格式





6、迭代1000次后，权重每10000次保存一次

可以进行修改保存频率寻找最合适的权重，在如下位置修改

![img](file:///C:\Users\86186\Documents\Tencent Files\2016993189\Image\C2C\B384118729D09F00C55C50CA236E42E0.jpg)



最终选择了训练4000次得到的权重，但是由于权重太大，就不上传到github了。