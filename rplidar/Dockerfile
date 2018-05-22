FROM kinetic-desktop-full-rpi

RUN echo "source /opt/ros/kinetic/setup.bash" >> /root/.bashrc

RUN mkdir -p /root/catkin_ws/src

WORKDIR /root/catkin_ws/src

RUN /bin/bash -c "source /opt/ros/kinetic/setup.bash; catkin_init_workspace" 

WORKDIR /root/catkin_ws

RUN /bin/bash -c "source /opt/ros/kinetic/setup.bash; catkin_make" 

RUN echo "source /root/catkin_ws/devel/setup.bash" >> /root/.bashrc

WORKDIR /root/catkin_ws/src

RUN git clone https://github.com/robopeak/rplidar_ros

RUN sed -i -e 's/ttyUSB0/ttyUSB_lidar/g' rplidar_ros/launch/rplidar.launch

WORKDIR /root/catkin_ws

RUN /bin/bash -c "source /opt/ros/kinetic/setup.bash; catkin_make" 

RUN /bin/bash -c "source /opt/ros/kinetic/setup.bash; catkin_make install"

RUN usermod -a -G dialout root

RUN apt-get update && apt-get install -y net-tools dnsutils iputils-ping && rm -rf /var/lib/apt/lists/*
