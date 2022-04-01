# LG_OpenSSL_Android



## 编译环境

```
Ubuntu
ubuntu-21.10-desktop-amd64.iso

NDK
android-ndk-r21e-linux-x86_64.zip

OpenSSL
openssl-1.1.1n.tar.gz
```



## NDK 下载

较新版本

https://developer.android.google.cn/ndk/downloads

较旧版本

https://github.com/android/ndk/wiki/Unsupported-Downloads 

r21e 版本 ndkVersion "21.4.7075529"

https://dl.google.com/android/repository/android-ndk-r21e-linux-x86_64.zip



```
mkdir AndroidDev
cd AndroidDev
wget https://dl.google.com/android/repository/android-ndk-r21e-linux-x86_64.zip
unzip android-ndk-r21e-linux-x86_64.zip
```



## OpenSSL 下载

https://www.openssl.org/source/

官网 Downloads 页面展示以下版本

| KBytes | Date                 | File                                                         |
| ------ | -------------------- | ------------------------------------------------------------ |
| 9619   | 2022-Mar-15 15:24:36 | [openssl-1.1.1n.tar.gz](https://www.openssl.org/source/openssl-1.1.1n.tar.gz) ([SHA256](https://www.openssl.org/source/openssl-1.1.1n.tar.gz.sha256)) ([PGP sign](https://www.openssl.org/source/openssl-1.1.1n.tar.gz.asc)) ([SHA1](https://www.openssl.org/source/openssl-1.1.1n.tar.gz.sha1)) |
| 14685  | 2022-Mar-15 15:24:36 | [openssl-3.0.2.tar.gz](https://www.openssl.org/source/openssl-3.0.2.tar.gz) ([SHA256](https://www.openssl.org/source/openssl-3.0.2.tar.gz.sha256)) ([PGP sign](https://www.openssl.org/source/openssl-3.0.2.tar.gz.asc)) ([SHA1](https://www.openssl.org/source/openssl-3.0.2.tar.gz.sha1)) |



```
wget https://www.openssl.org/source/openssl-1.1.1n.tar.gz
tar -zxvf openssl-1.1.1n.tar.gz
```



## 编译

Android 官方编译说明

```
https://github.com/openssl/openssl/blob/master/NOTES-ANDROID.md
```



命令示例

```
export ANDROID_NDK_ROOT=/home/whoever/Android/android-sdk/ndk/20.0.5594570
PATH=$ANDROID_NDK_ROOT/toolchains/llvm/prebuilt/linux-x86_64/bin:$ANDROID_NDK_ROOT/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64/bin:$PATH
./Configure android-arm64 -D__ANDROID_API__=29
make
```



调整命令编译 arm64-v8a

```
cd openssl-1.1.1n
export ANDROID_NDK_HOME=/home/louis/Desktop/AndroidDev/android-ndk-r21e
PATH=$ANDROID_NDK_HOME/toolchains/llvm/prebuilt/linux-x86_64/bin:$ANDROID_NDK_HOME/toolchains/arm-linux-androideabi-4.9/prebuilt/linux-x86_64/bin:$PATH
./Configure android-arm64 -D__ANDROID_API__=23 --prefix=/home/louis/Desktop/AndroidDev/openssl-1.1.1n_so/arm64-v8a
make
make install
```



继续编译 armeabi-v7a

```
make clean
./Configure android-arm -D__ANDROID_API__=23 --prefix=/home/louis/Desktop/AndroidDev/openssl-1.1.1n_so/armeabi-v7a
make
make install
```







附：

```
//1.1.1 分支
https://github.com/openssl/openssl/tree/OpenSSL_1_1_1-stable
//镜像
https://gitcode.net/mirrors/openssl/openssl
```

