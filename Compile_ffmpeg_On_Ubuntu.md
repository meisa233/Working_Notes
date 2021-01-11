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
### 3.编译和安装
请注意：这份指导假定我们只想安装**大部分**第三方库。<br />
该节下的每一小节包含了在编译过程中的安装第三方库的指令所需要的的依赖包的安装过程。<br />
<br />
如果你不需要其中的某些功能，可以选择略过，移除./configure后面的相关选项。<br />
举例来说，如果不需要**libvpx**的话，需要移除**--enable-libvpx**<br />
<br />
小贴士：可以在**make**命令后面加上-j8来加速
