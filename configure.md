
#### Install librealsense 

from   https://github.com/IntelRealSense/librealsense/blob/master/doc/distribution_linux.md

Intel® RealSense™ SDK 2.0 provides installation packages for Intel X86/AMD64-based Debian distributions in dpkg format for Ubuntu 16/18/20 LTS.

The Realsense DKMS kernel drivers package (librealsense2-dkms) supports Ubuntu LTS kernels 4.4, 4.8, 4.10, 4.13, 4.15, 4.18*, 5.0*, 5.3* and 5.4. Please refer to Ubuntu Kernel Release Schedule for further details.

  Unplug any connected Intel RealSense camera

## Installing the packages:
- Register the server's public key:  
`sudo apt-key adv --keyserver keys.gnupg.net --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE || sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-key F6E65AC044F831AC80A06380C8B3A55A6F3EFCDE`
In case the public key still cannot be retrieved, check and specify proxy settings: `export http_proxy="http://<proxy>:<port>"`  
, and rerun the command. See additional methods in the following [link](https://unix.stackexchange.com/questions/361213/unable-to-add-gpg-key-with-apt-key-behind-a-proxy).  

- Add the server to the list of repositories:  
  Ubuntu 16 LTS:  
`sudo add-apt-repository "deb http://realsense-hw-public.s3.amazonaws.com/Debian/apt-repo xenial main" -u`  
  Ubuntu 18 LTS:  
`sudo add-apt-repository "deb http://realsense-hw-public.s3.amazonaws.com/Debian/apt-repo bionic main" -u`  
  Ubuntu 20 LTS:  
`sudo add-apt-repository "deb http://realsense-hw-public.s3.amazonaws.com/Debian/apt-repo focal main" -u`

- Install the libraries (see section below if upgrading packages):  
  `sudo apt-get install librealsense2-dkms`  
  `sudo apt-get install librealsense2-utils`  
  The above two lines will deploy librealsense2 udev rules, build and activate kernel modules, runtime library and executable demos and tools.  

- Optionally install the developer and debug packages:  
  `sudo apt-get install librealsense2-dev`  
  `sudo apt-get install librealsense2-dbg`  
  With `dev` package installed, you can compile an application with **librealsense** using `g++ -std=c++11 filename.cpp -lrealsense2` or an IDE of your choice.

Reconnect the Intel RealSense depth camera and run: `realsense-viewer` to verify the installation.

Verify that the kernel is updated :    
`modinfo uvcvideo | grep "version:"` should include `realsense` string

## Upgrading the Packages:
Refresh the local packages cache by invoking:  
  `sudo apt-get update`  

Upgrade all the installed packages, including `librealsense` with:  
  `sudo apt-get upgrade`

To upgrade selected packages only a more granular approach can be applied:  
  `sudo apt-get --only-upgrade install <package1 package2 ...>`  
  E.g:   
  `sudo apt-get --only-upgrade install  librealsense2-utils librealsense2-dkms`
  
## Uninstalling the Packages:
**Important** Removing Debian package is allowed only when no other installed packages directly refer to it. For example removing `librealsense2-udev-rules` requires `librealsense2` to be removed first.

Remove a single package with:   
  `sudo apt-get purge <package-name>`  

Remove all RealSense™ SDK-related packages with:   
  `dpkg -l | grep "realsense" | cut -d " " -f 3 | xargs sudo dpkg --purge` 


#### Install PCL (v1.8.1)

* Download source code from Github (Release > pcl-1.8.1)

  Extract the `.tar.gz` file to `~/Library`

* Navigate to PCL root directory

  ```bash
  sudo apt install libboost-all-dev libeigen3-dev libflann-dev libvtk6-dev
  sudo apt install libproj-dev
  mkdir build && cd build
  cmake -DCMAKE_BUILD_TYPE=Release ..
  make -j8
  sudo make -j8 install
  ```

#### Install OpenCV (v3.4.4) with OpenCV_Contrib (v3.4.4)

- Download OpenCV source code from Github (Release > OpenCV 3.4.4)

  Download OpenCV_Contrib source code from Github (Release > 3.4.4)

  Extract the `.tar.gz` file to `~/Library`

  Copy OpenCV_Contrib folder into OpenCV folder and rename it as `opencv_contrib`

- Navigate to OpenCV root directory

  ```bash
  sudo apt-get install build-essential
  sudo apt-get install cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
  mkdir build && cd build
  cmake -DCMAKE_BUILD_TYPE=Release ..
  make -j8
  sudo make install
  ```
#### Install Mindvision

download software and follow the manual from this website

http://www.mindvision.com.cn/rjxz/list_12.aspx?lcid=138

#### Install Azure Kinect DK 

官方给的安装文档有问题，参照这个网址给的配置方式

https://blog.csdn.net/star0w/article/details/103402207

https://blog.csdn.net/weixin_44480249/article/details/107620446  这个比较好用，但是有些版本不适合

https://blog.csdn.net/u013270341/article/details/97431883   这个是一个人的踩坑记录

建议使用ubuntu18.04，使用16.04版本存在一定的问题

在更换libyuv里面的文件的时候，要吧src直接删了，然后从github下载下来的改名字直接复制进去，不然是要报错的

cmake建议版本3.14+



