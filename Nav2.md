
# Generate a Map with slam_toolbox

1. 安装 Cyclone DDS 
    ```shell
    $ sudo apt install ros-foxy-rmw-cyclonedds-cpp
    ```
2. 设置
   ```shell
   $ echo "export RWM_IMPLEMENTATION=rwm_cyclonedds_cpp" >> ~/.bashrc
   ```
3. 安装导航相关包
   ```shell
   $ sudo apt install ros-foxy-navigation2 ros-foxy-nav2-bringup ros-foxy-turtlebot3*
   ```
4. 安装 slam-toolbox
   ```shell
   $ sudo apt install ros-foxy-slam-toolbox
   ```
5. 设置turtlebot3的机器人模型
   ```shell
   $ echo "export TURTLEBOT3_MODEL=waffle" >> ~/.bashrc
   ```

1. 启动仿真环境
   ```shell
   $ ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
   ```
2. ff
   ```shell
   $ ros2 launch nav2_bringup navigation_launch.py use_sim_time:=True

   $ ros2 launch slam_toolbox online_async_launch.py use_sim_time:=True
   $ ros2 run rviz2 rviz2 -d /opt/ros/foxy/share/nav2_bringup/rviz/nav2_default_view.rviz 
   $ ros2 run turtlebot3_teleop teleop_keyboard 

   ```
3. 保存地图
   方式一：
   ```shell
   $ ros2 run nav2_map_server map_saver_cli -f my_map
   ```
   如果保存失败 Timeout，可增加超时时间，如下：
   ```shell
   $ ros2 run nav2_map_server map_saver_cli -f my_map --ros-args -p save_map_timeout:=20000
   ```
   方式二：
   在rviz界面，选择 Panels->Add new panel，选择 SlamToolBoxPlugin，填写Save Map和 Serialize Map，再点击对应按钮即可。
   ![SlamToolBoxPlugin](figures/SlamToolBoxPlugin.png)
   在home下会生成四个文件
   ![my_map_save](figures/my_map_save.png)
   地图文件
   ![my_map](figures/my_map.pgm)
   Gazebo
   ![Gazebo](/figures/Gazebo.png)
