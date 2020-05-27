# how to compile opencv 3.4.10 on jetson nano

## apt
```bash
sudo apt-get purge '*opencv*'
sudo apt-get -y install cmake
sudo apt-get -y install libeigen3-dev
sudo apt-get -y install libgtk-3-dev qt5-default freeglut3-dev libvtk6-qt-dev
sudo apt-get -y install libtbb-dev
sudo apt-get -y install libhdf5-dev
sudo apt-get -y install libjpeg-dev libjasper-dev libpng++-dev libtiff-dev libopenexr-dev libwebp-dev
sudo apt-get -y install libpython2.7-dev libpython3.5-dev
sudo apt-get -y install python-numpy python-scipy python-matplotlib
sudo apt-get -y install python3-numpy python3-scipy python3-matplotlib
sudo apt-get -y install libopenblas-dev liblapacke-dev
sudo apt-get -y install libatlas-base-dev liblapacke-dev
```

## make swap file
```bash
sudo dd if=/dev/zero of=/swapfile bs=1M count=6144
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

## download
```bash
cd /opt
wget https://github.com/opencv/opencv/archive/3.4.10.zip
unzip 3.4.10.zip
mv opencv-3.4.10 opencv-3.4.10_src
cd opencv-3.4.10
mkdir -p build && cd build
```

## cmake
```bash
cmake -D BUILD_opencv_python2=ON -D BUILD_opencv_python3=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D BUILD_CUDA_STUBS=OFF -D BUILD_DOCS=OFF -D BUILD_EXAMPLES=OFF -D BUILD_JASPER=OFF -D BUILD_JPEG=OFF -D BUILD_OPENEXR=OFF -D BUILD_PACKAGE=ON -D BUILD_PERF_TESTS=OFF -D BUILD_PNG=OFF -D BUILD_SHARED_LIBS=ON -D BUILD_TBB=OFF -D BUILD_TESTS=OFF -D BUILD_TIFF=OFF -D BUILD_WITH_DEBUG_INFO=ON -D BUILD_ZLIB=OFF -D BUILD_WEBP=OFF -D BUILD_opencv_apps=ON -D BUILD_opencv_calib3d=ON -D BUILD_opencv_core=ON -D BUILD_opencv_cudaarithm=ON -D BUILD_opencv_cudabgsegm=ON -D BUILD_opencv_cudacodec=ON -D BUILD_opencv_cudafeatures2d=ON -D BUILD_opencv_cudafilters=ON -D BUILD_opencv_cudaimgproc=ON -D BUILD_opencv_cudalegacy=ON -D BUILD_opencv_cudaobjdetect=ON -D BUILD_opencv_cudaoptflow=ON -D BUILD_opencv_cudastereo=ON -D BUILD_opencv_cudawarping=ON -D BUILD_opencv_cudev=ON -D BUILD_opencv_dnn=ON -D BUILD_opencv_features2d=ON -D BUILD_opencv_flann=ON -D BUILD_opencv_highgui=ON -D BUILD_opencv_imgcodecs=ON -D BUILD_opencv_imgproc=ON -D BUILD_opencv_java=OFF -D BUILD_opencv_ml=ON -D BUILD_opencv_objdetect=ON -D BUILD_opencv_photo=ON -D BUILD_opencv_python2=OFF -D BUILD_opencv_python3=ON -D BUILD_opencv_shape=ON -D BUILD_opencv_stitching=ON -D BUILD_opencv_superres=ON -D BUILD_opencv_ts=ON -D BUILD_opencv_video=ON -D BUILD_opencv_videoio=ON -D BUILD_opencv_videostab=ON -D BUILD_opencv_viz=ON -D BUILD_opencv_world=OFF -D CMAKE_BUILD_TYPE=RELEASE -D CUDA_ARCH_BIN="5.3" -D CUDA_ARCH_PTX="5.3" -D CV_TRACE=OFF -D ENABLE_CXX11=ON -D WITH_1394=ON -D WITH_CAROTENE=ON -D WITH_CUBLAS=ON -D WITH_CUDA=ON -D WITH_CUFFT=ON -D WITH_EIGEN=ON -D WITH_FFMPEG=ON -D WITH_GDAL=OFF -D WITH_GPHOTO2=OFF -D WITH_GIGEAPI=ON -D WITH_GSTREAMER=ON -D WITH_GTK=ON -D WITH_INTELPERC=OFF -D WITH_IPP=OFF -D WITH_IPP_A=OFF -D WITH_ITT=OFF -D WITH_JASPER=ON -D WITH_JPEG=ON -D WITH_LIBV4L=ON -D WITH_OPENCL=OFF -D WITH_OPENCLAMDBLAS=OFF -D WITH_OPENCLAMDFFT=OFF -D WITH_OPENCL_SVM=OFF -D WITH_OPENEXR=ON -D WITH_OPENGL=OFF -D WITH_OPENNI=OFF -D WITH_PNG=ON -D WITH_PTHREADS_PF=ON -D WITH_PVAPI=ON -D WITH_QT=OFF -D WITH_TBB=OFF -D WITH_TIFF=ON -D WITH_UNICAP=OFF -D WITH_V4L=OFF -D WITH_VTK=ON -D WITH_WEBP=ON -D WITH_XIMEA=OFF -D WITH_XINE=OFF -D WITH_LAPACK=ON -D CMAKE_INSTALL_PREFIX=/opt/opencv-3.4.10 -D ENABLE_NEON=ON -D ENABLE_VFPV3=ON ..
```

## make
```bash
make -j `nproc`
make install
/bin/bash -c 'echo "/opt/opencv-3.4.10" > /etc/ld.so.conf.d/opencv.conf'
sudo ldconfig
```
