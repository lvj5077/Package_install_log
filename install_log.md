# Ubuntu14.04.5

## sudo install
	sudo passwd
	sudo apt-get update
	sudo apt-get remove libreoffice-common
	sudo apt-get remove unity-webapps-common
	sudo apt-get remove thunderbird totem rhythmbox empathy brasero simple-scan gnome-mahjongg aisleriot 
	sudo apt-get remove gnome-mines cheese transmission-common gnome-orca webbrowser-app gnome-sudoku  landscape-client-ui-install  
	sudo apt-get remove onboard deja-dup 

	sudo apt-get install unity-tweak-tool 
	sudo apt-get install unity-webapps-service

	sudo add-apt-repository ppa:noobslab/themes
	sudo apt-get update
	sudo apt-get install flatabulous-theme

	sudo add-apt-repository ppa:noobslab/icons
	sudo apt-get update
	sudo apt-get install ultra-flat-icons

	sudo apt install openssh-server
	sudo apt-get install espeak
	sudo gpasswd --add ${USER} dialout
	sudo apt-get install libncurses5-dev

	sudo apt-get install cmake
	sudo apt-get update && sudo apt-get install build-essential
	sudo apt-get install libeigen3-dev libsuitesparse-dev libqt4-dev qt4-qmake libqglviewer-dev


# 04/28/2017
## Pangolin
	sudo apt-get install libglew-dev
	git clone https://github.com/stevenlovegrove/Pangolin.git
	cd Pangolin
	mkdir build
	cd build
	cmake ..
	make -j

## OpenCV3.2
	sudo apt-get install build-essential libgtk2.0-dev libvtk5-dev libjpeg-dev libtiff-dev libjasper-dev libopenexr-dev libtbb-dev
	
	mkdir build
	cd build
	cmake ..
	make -j4
	Usage:
	SET("OpenCV_DIR" "/home/jin/Packages/opencv-3.2.0/build")
	find_package(OpenCV 3.2 REQUIRED)
## OpenCV2.4.13
	mkdir build
	cd build
	cmake ..
	make -j4
	Usage:
	SET("OpenCV_DIR" "/home/jin/Packages/opencv-2.4.13/build")
	find_package(OpenCV 2.4 REQUIRED)

## Eigen3.3.3
	mkdir build
	cd build
	cmake ..
	make
	include_directories("/usr/include/eigen-3.3.3")

## ROS-indigo
	sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'

	sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116

	sudo apt-get update

	sudo apt-get install ros-indigo-desktop-full

	sudo rosdep init
	rosdep update

	echo "source /opt/ros/indigo/setup.bash" >> ~/.bashrc
	source ~/.bashrc
## ROS-indigo-rviz
	sudo apt-get install ros-indigo-rviz

## LSD-ROS (rosmake)
	sudo apt-get install ros-indigo-libg2o ros-indigo-cv-bridge liblapack-dev libblas-dev freeglut3-dev libqglviewer-dev libsuitesparse-dev libx11-dev

	sudo apt-get install python-rosinstall
	mkdir ~/rosbuild_ws
	cd ~/rosbuild_ws
	rosws init . /opt/ros/indigo
	mkdir package_dir
	rosws set ~/rosbuild_ws/package_dir -t .
	echo "source ~/rosbuild_ws/setup.bash" >> ~/.bashrc
	bash
	cd package_dir
	git clone https://github.com/tum-vision/lsd_slam.git lsd_slam
	rosmake lsd_slam

## librealsense
	sudo apt-get install ros-indigo-rgbd-launch
	sudo apt-get install libusb-1.0-0-dev pkg-config
	./scripts/install_glfw3.sh
	mkdir build && cd build
	cmake ../ -DBUILD_EXAMPLES=true
	make
	cd ..
	sudo cp config/99-realsense-libusb.rules /etc/udev/rules.d/
	sudo udevadm control --reload-rules && udevadm trigger
	sudo apt-get install libssl-dev
	./scripts/patch-realsense-ubuntu-xenial.sh
	press m, if no m, then press y

# 05/08/2017
## realsense-indigo-devel
	#Creating a workspace for catkin
	cd ~
	mkdir -p ~/catkin_ws/src
	cd ~/catkin_ws/src
	cd ..
	catkin_make
	source devel/setup.bash
	mkdir -p ~/catkin_ws/devel/lib
	
	cp /home/jin/Packages/librealsense/build/devel/lib/librealsense.so* ~/catkin_ws/devel/lib

	edit ~/catkin_ws/src/realsense/realsense_camera/CMakeLists.txt
	set(librealsense_DIR "/home/jin/Packages/librealsense/build/catkin_generated/installspace/")
	if(USE_SYSTEM_LIBREALSENSE)
	  find_package(realsense REQUIRED 
		PATH "/home/jin/Packages/librealsense/build/catkin_generated/installspace/")
	else()
	  list(APPEND REALSENSE_CATKIN_BASED_DEPS librealsense)
	endif()

	cd ~/catkin_ws/
	catkin_make
	source devel/setup.bash
## LSD-ROS (catkin)
	cd ~/catkin_ws/
	catkin_make
		
# 05/12/2017
## install libserial
	enable port permission: sudo gpasswd --add ${USER} dialout
	install:	./configure 
				make
				make install

# 07/26/2017
## install pcl
	sudo add-apt-repository ppa:v-launchpad-jochen-sprickerhof-de/pcl
	sudo apt-get update
	sudo apt-get install libpcl-all

## install Ceres
	sudo apt-get install liblapack-dev libsuitesparse-dev libcxsparse3.1.2 libgflags-dev libgoogle-glog-dev libgtest-dev
	mkdir build
	cd build
	cmake ..

## install g2o
	sudo apt-get install libqt4-dev qt4-qmake libqglviewer-dev libsuitesparse-dev libcxsparse3.1.2
	mkdir build
	cd build
	cmake ..