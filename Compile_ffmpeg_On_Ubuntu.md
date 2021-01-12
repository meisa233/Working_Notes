# 在Ubuntu从源编译ffmpeg
## 官方编译文档：http://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu

### 1.安装依赖
```
sudo apt-get update -qq && sudo apt-get -y install \
  autoconf \
  automake \
  build-essential \
  cmake \
  git-core \
  libass-dev \
  libfreetype6-dev \
  libgnutls28-dev \
  libsdl2-dev \
  libtool \
  libva-dev \
  libvdpau-dev \
  libvorbis-dev \
  libxcb1-dev \
  libxcb-shm0-dev \
  libxcb-xfixes0-dev \
  pkg-config \
  texinfo \
  wget \
  yasm \
  zlib1g-dev
```
### 2.创建临时文件夹ffmpeg_sources和bin
ffmpeg_sources:存放所有的源码
bin：存放所有的二进制文件（可执行文件）
```
mkdir -p ~/ffmpeg_sources ~/bin
```
### 3.编译和安装
请注意：这份指导假定我们只想安装**大部分**第三方库。<br />
该节下的每一小节包含了在编译过程中的安装第三方库的指令所需要的的依赖包的安装过程。<br />
<br />
如果你不需要其中的某些功能，可以选择略过，移除./configure后面的相关选项。<br />
举例来说，如果不需要**libvpx**的话，需要移除**--enable-libvpx**<br />
<br />
小贴士：可以在**make**命令后面加上-j8来加速
#### (1) 安装nasm
```
sudo apt-get install nasm
```
或者
```
cd ~/ffmpeg_sources && \
wget https://www.nasm.us/pub/nasm/releasebuilds/2.14.02/nasm-2.14.02.tar.bz2 && \
tar xjvf nasm-2.14.02.tar.bz2 && \
cd nasm-2.14.02 && \
./autogen.sh && \
PATH="$HOME/bin:$PATH" ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" && \
make && \
make install
```
#### (2) 安装libx264
配置时的选项
```
--enable-gpl --enable-libx264
```
安装
```
sudo apt-get install libx264-dev
```
或者
```
cd ~/ffmpeg_sources && \
git -C x264 pull 2> /dev/null || git clone --depth 1 https://code.videolan.org/videolan/x264.git && \
cd x264 && \
PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" --enable-static --enable-pic && \
PATH="$HOME/bin:$PATH" make && \
make install
```
#### (2) libx265
配置时的选项
```
--enable-gpl --enable-libx265
```
安装
```
sudo apt-get install libx265-dev libnuma-dev
```
或者
```
sudo apt-get install libnuma-dev && \
cd ~/ffmpeg_sources && \
git -C x265_git pull 2> /dev/null || git clone https://bitbucket.org/multicoreware/x265_git && \
cd x265_git/build/linux && \
PATH="$HOME/bin:$PATH" cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX="$HOME/ffmpeg_build" -DENABLE_SHARED=off ../../source && \
PATH="$HOME/bin:$PATH" make && \
make install
```

#### (3) libvpx
配置时的选项
```
--enable-libvpx
```
安装
```
sudo apt-get install libvpx-dev
```
或者
```
cd ~/ffmpeg_sources && \
git -C libvpx pull 2> /dev/null || git clone --depth 1 https://chromium.googlesource.com/webm/libvpx.git && \
cd libvpx && \
PATH="$HOME/bin:$PATH" ./configure --prefix="$HOME/ffmpeg_build" --disable-examples --disable-unit-tests --enable-vp9-highbitdepth --as=yasm && \
PATH="$HOME/bin:$PATH" make && \
make install
```
#### (4) libfdk-aac
配置时的选项
```
--enable-libfdk-aac 
```
安装
```
sudo apt-get install libfdk-aac-dev
```
或者
```
cd ~/ffmpeg_sources && \
git -C fdk-aac pull 2> /dev/null || git clone --depth 1 https://github.com/mstorsjo/fdk-aac && \
cd fdk-aac && \
autoreconf -fiv && \
./configure --prefix="$HOME/ffmpeg_build" --disable-shared && \
make && \
make install
```
#### (5) libmp3lame
配置时的选项
```
--enable-libmp3lame
```
安装
```
sudo apt-get install libmp3lame-dev
```
或者
```
cd ~/ffmpeg_sources && \
wget -O lame-3.100.tar.gz https://downloads.sourceforge.net/project/lame/lame/3.100/lame-3.100.tar.gz && \
tar xzvf lame-3.100.tar.gz && \
cd lame-3.100 && \
PATH="$HOME/bin:$PATH" ./configure --prefix="$HOME/ffmpeg_build" --bindir="$HOME/bin" --disable-shared --enable-nasm && \
PATH="$HOME/bin:$PATH" make && \
make install
```
#### (6) libopus
配置时的选项
```
--enable-libopus
```
安装
```
sudo apt-get install libopus-dev
```
或者
```
cd ~/ffmpeg_sources && \
git -C opus pull 2> /dev/null || git clone --depth 1 https://github.com/xiph/opus.git && \
cd opus && \
./autogen.sh && \
./configure --prefix="$HOME/ffmpeg_build" --disable-shared && \
make && \
make install
```
#### (7) libaom
```
cd ~/ffmpeg_sources && \
git -C aom pull 2> /dev/null || git clone --depth 1 https://aomedia.googlesource.com/aom && \
mkdir -p aom_build && \
cd aom_build && \
PATH="$HOME/bin:$PATH" cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX="$HOME/ffmpeg_build" -DENABLE_SHARED=off -DENABLE_NASM=on ../aom && \
PATH="$HOME/bin:$PATH" make && \
make install
```
注意：<br />
由于aom在墙外，在国内git clone的话是很容易出现以下错误的：<br />
```
fatal: unable to access 'https://aomedia.googlesource.com/aom/': Failed to connect to aomedia.googlesource.com port 443: Timed out
```
解决方法来源：https://blog.csdn.net/listener51/article/details/79505812
<br />
git config --global http.proxy http://127.0.0.1:梯子的端口号
<br />
要查看端口号，请查看梯子的设置<br />

#### (8) libsvtav1
```
--enable-libsvtav1
```
```
cd ~/ffmpeg_sources && \
git -C SVT-AV1 pull 2> /dev/null || git clone https://github.com/AOMediaCodec/SVT-AV1.git && \
mkdir -p SVT-AV1/build && \
cd SVT-AV1/build && \
PATH="$HOME/bin:$PATH" cmake -G "Unix Makefiles" -DCMAKE_INSTALL_PREFIX="$HOME/ffmpeg_build" -DCMAKE_BUILD_TYPE=Release -DBUILD_DEC=OFF -DBUILD_SHARED_LIBS=OFF .. && \
PATH="$HOME/bin:$PATH" make && \
make install
```
#### (9) ffmpeg
```
cd ~/ffmpeg_sources && \
wget -O ffmpeg-snapshot.tar.bz2 https://ffmpeg.org/releases/ffmpeg-snapshot.tar.bz2 && \
tar xjvf ffmpeg-snapshot.tar.bz2 && \
cd ffmpeg && \
PATH="$HOME/bin:$PATH" PKG_CONFIG_PATH="$HOME/ffmpeg_build/lib/pkgconfig" ./configure \
  --prefix="$HOME/ffmpeg_build" \
  --pkg-config-flags="--static" \
  --extra-cflags="-I$HOME/ffmpeg_build/include" \
  --extra-ldflags="-L$HOME/ffmpeg_build/lib" \
  --extra-libs="-lpthread -lm" \
  --bindir="$HOME/bin" \
  --enable-gpl \
  --enable-gnutls \
  --enable-libaom \
  --enable-libass \
  --enable-libfdk-aac \
  --enable-libfreetype \
  --enable-libmp3lame \
  --enable-libopus \
  --enable-libsvtav1 \
  --enable-libvorbis \
  --enable-libvpx \
  --enable-libx264 \
  --enable-libx265 \
  --enable-nonfree && \
PATH="$HOME/bin:$PATH" make && \
make install && \
hash -r
```
```
source ~/.profile
```
```
ffmpeg (also ffplay, ffprobe, lame, x264, & x265) 这些都可以使用了
```
ffmpeg的二进制文件地址：~/bin <br />
如果需要其他用户也可以使用ffmpeg，请将~/bin/下的文件复制到/usr/local/bin
