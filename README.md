# Intel RealSense Gazebo ROS plugin

This package is a Gazebo ROS plugin for the Intel D435 realsense camera.
 
## Acknowledgement

This is a continuation of work done by [SyrianSpock](https://github.com/SyrianSpock) for a Gazebo ROS plugin with RS200 camera.

This package also includes the work developed by Intel Corporation with the ROS model for the [D435](https://github.com/intel-ros/realsense) camera.

## Example usage with a custom robot

Note that this was tested for the ROS2 branch with ROS Fosy distro. A turtlebot3 like custom robot model was used. 
In custom robot's model.sdf, we should attach the link and sensors as; 

```xml
    <link name="realsense_link">
      <pose>0.4 0 0.25 0 0 0</pose>
      <visual name="realsense_link_visual">
        <pose>0 0 0 -1.57 0 -1.57</pose>
        <geometry>
          <mesh>
            <uri>model://chiconybot/meshes/d435.dae</uri>
          </mesh>
        </geometry>
      </visual>
      <collision name="realsense_link_collision">
        <pose>0 0 0 -1.57 0 -1.57</pose>
        <geometry>
          <box>
            <size>0.02505 0.090 0.025</size>
          </box>
        </geometry>
      </collision>
      <inertial>
        <pose>0 0 0 0 0 0</pose>
        <inertia>
          <ixx>0.001</ixx>
          <ixy>0.000</ixy>
          <ixz>0.000</ixz>
          <iyy>0.001</iyy>
          <iyz>0.000</iyz>
          <izz>0.001</izz>
        </inertia>
        <mass>0.564</mass>
      </inertial>

      <sensor name="cameradepth" type="depth">
        <camera name="camera">
          <horizontal_fov>1.57</horizontal_fov>
          <image>
            <width>1280</width>
            <height>720</height>
          </image>
          <clip>
            <near>0.1</near>
            <far>100</far>
          </clip>
          <noise>
            <type>gaussian</type>
            <mean>0.0</mean>
            <stddev>0.100</stddev>
          </noise>
        </camera>
        <always_on>1</always_on>
        <update_rate>30</update_rate>
        <visualize>0</visualize>
      </sensor>
      <sensor name="cameracolor" type="camera">
        <camera name="camera">
          <horizontal_fov>1.57</horizontal_fov>
          <image>
            <width>1280</width>
            <height>720</height>
            <format>RGB_INT8</format>
          </image>
          <clip>
            <near>0.1</near>
            <far>100</far>
          </clip>
          <noise>
            <type>gaussian</type>
            <mean>0.0</mean>
            <stddev>0.007</stddev>
          </noise>
        </camera>
        <always_on>1</always_on>
        <update_rate>30</update_rate>
        <visualize>1</visualize>
      </sensor>
      <sensor name="cameraired1" type="camera">
        <camera name="camera">
          <horizontal_fov>1.57</horizontal_fov>
          <image>
            <width>1280</width>
            <height>720</height>
            <format>L_INT8</format>
          </image>
          <clip>
            <near>0.1</near>
            <far>100</far>
          </clip>
          <noise>
            <type>gaussian</type>
            <mean>0.0</mean>
            <stddev>0.05</stddev>
          </noise>
        </camera>
        <always_on>1</always_on>
        <update_rate>1</update_rate>
        <visualize>0</visualize>
      </sensor>
      <sensor name="cameraired2" type="camera">
        <camera name="camera">
          <horizontal_fov>1.57</horizontal_fov>
          <image>
            <width>1280</width>
            <height>720</height>
            <format>L_INT8</format>
          </image>
          <clip>
            <near>0.1</near>
            <far>100</far>
          </clip>
          <noise>
            <type>gaussian</type>
            <mean>0.0</mean>
            <stddev>0.05</stddev>
          </noise>
        </camera>
        <always_on>1</always_on>
        <update_rate>1</update_rate>
        <visualize>0</visualize>
      </sensor>
    </link>

    <joint name="realsense_joint" type="fixed">
      <parent>base_link</parent>
      <child>realsense_link</child>
      <pose>0.4 0 0.4 0 0 0</pose>
    </joint>
```
