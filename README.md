# YzyFFmpeg
Ubuntu下编译ffmpeg  
首先在此像雷神致敬，感谢这种无私奉献的人，永远活在我们的心中  
## 编译步骤： ##  
1、下载FFmpeg源码 www.ffmpeg.org  
2、配置ndk环境  
3、在下载好的ffmpeg的源码中创建一个shell脚本yzy_build_android.sh  
4、修改configure脚本，不然编译出来的so库中so在文件名中间，Android无法识别，如：“libavcodec.so.5.100.1”  
找到下面的代码  
    
    SLIBNAME_WITH_MAJOR='$(SLIBNAME).$(LIBMAJOR)'  
    LIB_INSTALL_EXTRA_CMD='$$(RANLIB)"$(LIBDIR)/$(LIBNAME)"'  
    SLIB_INSTALL_NAME='$(SLIBNAME_WITH_VERSION)'  
    SLIB_INSTALL_LINKS='$(SLIBNAME_WITH_MAJOR)$(SLIBNAME)'  
修改为：  

    SLIBNAME_WITH_MAJOR='$(SLIBPREF)$(FULLNAME)-$(LIBMAJOR)$(SLIBSUF)'  
    LIB_INSTALL_EXTRA_CMD='$$(RANLIB)"$(LIBDIR)/$(LIBNAME)"'  
    SLIB_INSTALL_NAME='$(SLIBNAME_WITH_MAJOR)'  
    SLIB_INSTALL_LINKS='$(SLIBNAME)'  
5、为源码赋予777权限：sudo chmod 777 -R YzyFFmpeg  
6、执行yzy_build_android.sh脚本进行怼源码编译  
7、编译好的so库放在yzy_android文件夹下对应的cpu文件夹下  
8、注意yzy_build_android.sh脚本中的几个环境的版本好要配置正确，不然无法编译通过  

    export NDK=/home/yzy/DevTools/android-ndk-r13
    export SYSROOT=$NDK/platforms/android-9/arch-arm/
    export TOOLCHAIN=$NDK/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64

邮箱：yzytmac@163.com  

