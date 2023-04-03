

## Xcode 14.3 兼容iOS 8

#### Xcode 14.3版本运行项目报错

ld: file not found: /Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/lib/arc/libarclite_iphoneos.a

clang: error: linker command failed with exit code 1 (use -v to see invocation)

因为系统已经内置有`ARC`相关的库，所以没必要再额外链接，至少Xcode 14支持的最低部署目标iOS 11及以上版本的系统肯定是没问题的。如果应用部署目标不低于iOS 11还出现问题，那么应该是第三方库的部署目标有问题。

arc

```
/Applications/Xcode.app/Contents/Developer/Toolchains/XcodeDefault.xctoolchain/usr/lib/arc/
```

参考链接 https://blog.csdn.net/crasowas/article/details/129901398



#### 在Xcode升级到Xcode14以后，大家都发现系统的支持版本升级到了11.0，那么想要调试11.0之前的系统该怎么办呢？

下边给大家介绍Xcode14调试11.0之前的系统的方法：

![截屏2022-09-15 09.55.56](https://github.com/wang-junxing/DeviceSupport/blob/master/document/%E6%88%AA%E5%B1%8F2022-09-15%2009.55.56.png?raw=true)

1.首先在Xcode14之前的版本下，应用程序-xcode 显示包内容 /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport ，把程序中的低于11.0的文件夹拷贝到Xcode14的相应目录下。



2.在Xcode14下，应用程序-xcode 显示包内容 修改以下文件,记得修改前备份,防止改错无法还原.

/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/SDKSettings.json

/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS.sdk/SDKSettings.plist

添加 8.0-10.3 的版本 到以下节点中

SupportedTargets - iphoneos - ValidDeploymentTargets

DefaultProperties - DEPLOYMENT_TARGET_SUGGESTED_VALUES

如果没有包含，请把这个plist文件拷贝到桌面手动添加。添加完成后再粘贴到原来的位置。重启Xcode即可。

3.MinimumDeploymentTarget 改为8.0



#### DeviceSupport下载地址:

https://github.com/wang-junxing/DeviceSupport




链接：https://www.jianshu.com/p/1fab8881f08a