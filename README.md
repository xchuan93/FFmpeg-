# FFmpeg-ios
# Mac配置FFmpeg环境
# 1 安装homebrew
  打开终端输入以下命令行：
  ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  
# 2 安装FFmpeg
  brew install ffmpeg

# 3 iOS集成FFmpeg
  1 下载脚本FFmpeg脚本地址
    https://github.com/kewlbear/FFmpeg-iOS-build-script
	
  2 编译FFmpeg-iOS-build-script，获得FFmpeg静态库文件
    ./build-ffmpeg.sh
  
  3 这时只需执行以下命令即可，问题链接：https://github.com/kewlbear/FFmpeg-iOS-build-script/issues/119
  
  4 sudo xcode-select --switch /Applications/Xcode.app
  
# 4 iOS项目集成FFmpeg
  1）上步操作执行成功后，会生成FFmpeg-iOS文件，将该文件直接拖到项目中

  2）配置头文件搜索路径：在工程文件->Bulid Setting->Search Paths->Header Search Paths添加$(SRCROOT)/$(PRODUCT_NAME)/FFmpeg- iOS/include,(请根据自己实际路径更改)

 3）在工程中新建ffmpeg文件夹，并从ffmpeg-3.0的文件中添加如下文件：
  
     cmdutils_common_opts.h
     cmdutils.h及cmdutils.c
     config.h在scratch目录下取个对应平台的
     ffmpeg_filter.c
     ffmpeg_opt.c
     ffmpeg_videotoolbox.c
     ffmpeg.h及ffmpeg.c
     除了config.h文件外,别的文件均在ffmpeg-3.0源码目录中
	 
  4）编译后会报错，然后根据提示挨个修复，还需要导入相应的依赖库。
  
 # 五 使用FFmpeg转码
   1、FFmpeg使用命令行调用

   1） 如ffmpeg -i /temp.mp3 -y /test.aac 这条指令就是调用ffmpeg,输入源(-i)是/temp.mp3文件,输出到/test.aac,其中-y参数是若存在则直接覆盖

   2）ffmpeg -i /temp.mp4 -f flv -y /temp.flv 这条指令是输入一个视频文件,将文件转码为h264编码格式的flv文件,-f参数是指定目标格式

   3）具体FFmpeg能使用哪些指令可以参考官方文档或如下博客:http://www.cnblogs.com/wainiwann/p/4128154.html
 
 # demo主要介绍使用命令行做音视频解码操作，和m3u8文件下载
