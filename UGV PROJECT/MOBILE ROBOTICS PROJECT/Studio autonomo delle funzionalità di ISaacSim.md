NVIDIA che è l'azienda creatrice del software mette a disposizione tutorial e materiale utile all'apprendimento della robotica e del software stesso. Ho iniziato uno studio autonomo proprio di questo materiale da [Corso IsaacSim su tutto ciò che serve](https://www.nvidia.com/en-us/learn/learning-path/robotics/)

## INFORMAZIONI UTILI SULL'IMPORTAZIONE DI FILE URDF

1. Start by navigating to the top menu bar in Isaac Sim.
2. Click on **Isaac Utils > Workflows > URDF Importer.**

- This opens the URDF Importer interface, which is specifically designed to convert URDF files (used in ROS) into USD files (used in Omniverse Isaac Sim).

#### **Understand the Purpose of the Importer**

At the top of the interface, you’ll see an overview that explains that this utility is used to import URDF representations of robots into Isaac Sim. 

#### **Explore Import Options**

The importer provides several settings to customize how your robot is imported. These settings may vary depending on your robot type.

Note

If you’re unsure about any parameter, hover over it with your mouse to display a helpful tooltip.

#### **Configure the Fix Base Link Option**

One key setting is **Fix Base Link**, which determines whether the base of your robot is fixed in world coordinates.

For manipulator-style robots (e.g., robotic arms), this option is typically checked because their base doesn’t move.

1. Since we're using a mobile robot for this course, make sure the **Fix Base Link** setting is **unchecked**.

#### **Locate and Select the URDF File**

1. Scroll down to the **Input File** section and click on the **file browser**.
2. Find and select **carter.urdf**, then click **Select URDF**.
    - Once selected, you’ll notice a new sub-menu appears in the interface showing additional details about your robot’s joints and properties.

#### **Review and Adjust Joint Properties**

In this sub-menu, you can see all of Carter’s joints listed along with their default properties.

Let’s break down Carter’s design: 

- - Carter is a two-wheeled mobile robot with a third passive wheel at the back.
    - By default, joint target types are set to **Position** which works well for manipulators where precise positioning is required (e.g., gripping objects).
    - However, for Carter, we need to control wheel **Velocity** instead of position.

#### **Modify Joint Target Types**

Update these joint settings as follows: 

1. Change **left_wheel** and **right_wheel** target types to **Velocity**. 
    - This allows us to control the wheels to spin forward or backward.
2. Set **rear_axle** and **rear_pivot** target types to **None** because these are passive components that don’t require motor control. They will rotate naturally as Carter moves.

#### **Leave Other Settings as Default**

Unless specified otherwise, leave all remaining settings at their default values. These defaults are generally suitable for most use cases.

#### **Import the Robot**

1. Click on **Import** to begin converting and importing Carter’s URDF file into Isaac Sim.
2. When prompted, confirm the import path by selecting **Yes**.

- The importer will process the file and add Carter as a USD asset in your simulation environment.

---

**Why These Steps Are Important:**

- The URDF Importer simplifies bringing robots from ROS-based workflows into Isaac Sim, saving time and effort.
- Configuring options like joint target types ensures that your robot behaves correctly during simulation.
- Understanding these settings prepares you to import and customize other robots in future projects.

# PREPARING THE ENVIROMENT

#### **Adding a Simple Environment**

Right now, our simulation doesn’t have any ground or environment for Carter to interact with—it’s just floating in an empty space.

Isaac Sim 4.2Isaac Sim 4.5

1. To fix this, navigate to **Create > Isaac > Environments > Flat Grid**.
    - This will add a flat grid to your scene, which acts as a basic ground plane for Carter to move on.
    - Adding this environment is important because without it, physics simulations (like gravity) won't allow Carter to act correctly.

#### **Improving Visibility**

To make things easier to see, let’s turn off the default **Environment Light**:

2. In the _Stage_ window, locate the **Environment Light** object and toggle it off by clicking the small "**eye**" icon next to it.

#### **Adjusting Carter’s Position**

After adding the flat grid, you’ll notice that Carter might be intersecting with or sitting below the grid.

3. To fix this, select **Carter** in the _Stage_ window and move it slightly upward so it’s positioned above the ground. You can do this by dragging it up in the viewport or adjusting its `Z-axis` position in the _Transform_ settings.

#### **Activating Physics**

Now let’s test if physics is working correctly:

4. Press the **Play** button to start the simulation. This is located at the bottom of the left-hand toolbar. 
    - This step confirms that physics is active because we observed the Carter falling due to gravity in the simulation. That Carter’s colliders (the invisible boundaries that define its physical shape) are interacting with the environment.

#### **Hiding and Visualizing Colliders**

Isaac Sim can display green boxes around objects to represent their colliders. These are helpful for debugging but can get in the way visually.

To toggle them:

5. Go to **Show By Type** (the "eye" icon at the top of the viewport).
6. Navigate to **Physics > Colliders** and select **None**.

Now you can see Carter clearly without any visual obstructions.

# ADD A CAMERA

### Adding the Sensors

In this section, we’ll add an RGB camera and a lidar sensor to the Carter robot. Sensors are critical for enabling robots to perceive their environment, whether it’s for navigation, object detection, or other tasks. By the end of this section, you’ll know how to attach sensors to the robot, configure their placement, and visualize their outputs during simulation.

#### **Understanding Sensor Setup**

- The URDF file we imported earlier doesn’t include any sensors. This is common because URDF files typically focus on the robot’s physical structure and joints.
- Sensors like **cameras** and **Lidar** need to be added manually in Isaac Sim.
- Carter has designated spots for these sensors:

- At the front, there’s a rounded rectangle designed for a stereo camera.
- On the top, there’s a cylinder meant for a 2D lidar.

- Let’s add these sensors and configure them so Carter can perceive its environment.

#### **Adding an RGB Camera**

#### **Create the Camera**

1. Move your camera view close to Carter so you can easily position the sensor.
2. Navigate to **Create > Camera** in the menu. This adds a new camera to your scene.

#### **Attach the Camera to Carter**

3. In the _**Stage**_ window, drag and drop the camera under **Carter > Chassis_link**.

- This ensures that the camera moves with the robot during simulation.

5. Double-click the **camera** in the _stage_ to rename it to **RGB_Sensor** so it’s clear what this object represents.

#### **Position and Rotate the Camera**

5. Move the camera to the front top of Carter, aligning it with the rounded rectangle where a stereo camera would typically be placed.
    - We used **0.1, 0.0, 0.33** for translation parameters and **90, -90, 0.0** for our rotation parameters. You can see where these parameters are located in the video above.
    - Typically, in a URDF file, the locations of the sensors are identified. Here, we are estimating their location on the robot to accomplish the goals of this course.
6. If the movement of the camera feels “snappy” when trying to adjust its position, **disable** snapping by clicking on the **magnet icon** in the left toolbar. This allows for smooth, precise adjustments.
7. Rotate the camera so it faces forward relative to Carter’s orientation.

#### **Preview the Camera’s View**

Note

Hold right click when in the camera view and move the mouse to set rotation, use WASD to set the position

To check if your positioning is correct:

8. Change your viewport from **Perspective** to **RGB_Sensor**. You can do this by selecting the **camera** dropdown in the top of your _Viewport_, then selecting **Cameras > RGB_Sensor**.
    - This switches your view to what the camera sees. Adjust its position or rotation if needed.
9. Once satisfied, switch back to **Perspective**. 

#### **Validate Camera Movement**

10. Start the simulation by pressing **Play**.
11. Use your keyboard **W, A, S, D** to drive Carter around while observing whether the camera moves with it**.**
12. If everything looks good, **stop** the simulation.

#### **Adding a Lidar Sensor**

#### **Create and Attach Lidar**

13. Navigate to **Create > Isaac > Sensors > PhysX Lidar > Rotating**.
14. Just like with the camera, drag and drop this lidar sensor under **Carter > Chassis_link** in the _Stage_ window.

#### **Position the Lidar**

15. Move the lidar sensor to Carter’s top, aligning it with the cylindrical mesh.
    - We used **-0.05, 0.0, 0.42** for our translation parameters to position this sensor correctly. 

#### **Enable Visualization for Lidar Beams**

16. Select the **Lidar** sensor in the _`Stage`_ window.
17. Scroll down to its **Raw USD Properties** in the _Property_ panel.
18. Enable **Draw Lines**. This will allow you to see lidar beams during simulation:

- Gray beams indicate areas where no objects are detected.
- Red beams indicate that an object has been hit by a beam (e.g., walls or obstacles).

#### **Simulate and Test Lidar**

19. Press **Play** again to start simulating.

Observe gray beams radiating from the lidar sensor as it rotates. These beams represent how lidar scans its environment.

---

#### **Why These Steps Are Important**

- Adding sensors like cameras and lidar is essential for making robots “aware” of their surroundings. Without sensors, robots can’t interact intelligently with their environment.
- Properly positioning sensors ensures they capture relevant data—for example, placing an RGB camera at eye level or a lidar sensor on top for 360-degree scanning.
- Visualizing sensor outputs (like camera POV or lidar beams) helps you debug and verify that they’re working as intended.


# ADD OBSTACLES

### Adding Obstacles to the Environment

In this section, we’ll add obstacles to the environment so Carter’s sensors—specifically the lidar—can detect and interact with them. Obstacles are essential for testing how sensors perceive the robot’s surroundings, which is a key step in building navigation and obstacle avoidance systems. By the end of this section, you’ll know how to create obstacles, configure them as physics objects, and test their interaction with Carter’s sensors.

#### **Why Add Obstacles?**

- Lidar sensors work by emitting beams and detecting objects in their path. Without obstacles in the environment, the beams will remain gray, indicating that nothing is being hit.
- Adding obstacles gives Carter something to "see" with its **Lidar** and **RGB camera**, making the simulation more realistic and useful for testing.

#### **Add Primitives as Obstacles**

1. Navigate to **Create > Mesh > Cube** (or another primitive like a sphere or cylinder) to add a basic shape to your stage.
    - Place these meshes around the flat grid so they act as obstacles for Carter to detect.
    - Feel free to add as many obstacles as you like or even import a custom USD file if you have a pre-designed stage.

Tip

Spread the obstacles out at different distances and angles from Carter so you can test how well it detects objects in various positions.

#### **Simulate and Observe**

2. Press **Play** to start the simulation.
3. Look at the lidar beams:

- You’ll notice that they’re still gray, even though the obstacles are visible in the stage.
- This happens because the obstacles haven’t been configured as **physics objects** yet, so they don’t interact with the Lidar sensor.

5. **Stop** the simulation.

#### **Make Obstacles Physics Objects**

5. Select all the **obstacles** you’ve added in the _Stage_ window; **hold Shift** or **Ctrl** to select multiple objects.
6. Right-click on your selection and choose **Add > Physics > Rigid Body with Colliders Preset**.

- Adding a rigid body makes each obstacle a physics object, meaning it can interact with other objects (like Carter) and sensors (like lidar).
- The colliders define the physical boundaries of each object, which are used by lidar beams to detect collisions. 

#### **Test Lidar Detection**

7. Press **Play** again to restart the simulation.
8. Observe how the lidar beams now turn red when they hit an obstacle.

- Gray beams indicate empty space.
- Red beams show where an object has been detected.

**Test RGB Camera View**

9. Switch your viewport from **Perspective** to ****RGB_Sensor**** to see what Carter’s camera is detecting.
10. Drive Carter around using your keyboard **W, A, S, D** and observe how obstacles appear from its point of view.

This step helps you understand how both sensors work together:

- - The **RGB camera** provides a visual feed of what’s in front of Carter.
    - The **Lidar** gives precise distance measurements for objects around it.

#### **Stop Simulation and Reset View**

Once you’re done testing:

11. Stop the simulation by clicking **Pause** or **Stop**.
12. Switch your viewport back to **Perspective**.

Important

If you forget to switch back, any movement in your viewport will move the RGB camera instead of your perspective view.


# INSTALL ISAACSIM AND LINK IT TO ROS2

1. If not already installed, follow the installation guide for Isaac Sim provided in the [Isaac Sim Installation Documentation](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/index.html).
2. For this course, we assume you are using the **Workstation Installation** method.
    - Instructions can be found [here](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/install_workstation.html).
3. Alternatively, if you prefer to install Isaac Sim using PIP in a virtual environment, refer to the [PIP Installation Guide](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/install_python.html).
4. #### **Install ROS 2 Humble**

5. Install ROS 2 Humble on **Ubuntu 22.04** following the steps outlined in the [ROS and ROS 2 Installation Documentation](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/install_ros.html).
6. For this course, we recommend using the **Running Native ROS** method. Follow the instructions under:

- Running Native **ROS > ROS 2 > Ubuntu 22.04 > Humble**

#### **Launch Isaac Sim with ROS 2 Enabled**

6. To enable communication between Isaac Sim and ROS 2, **launch** Isaac Sim with the ROS 2 bridge **enabled**.

- If you are using ROS 2 Humble, Isaac Sim loads the Humble bridge by default, so no additional steps are required.
- If you are using ROS Noetic or another version of ROS, follow the instructions under **Enabling the ROS Bridge Extension** in the [documentation](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/install_ros.html#enabling-the-ros-bridge-extension).

8. Ensure that your ROS installation is sourced before launching Isaac Sim to avoid fallback to pre-packaged libraries.
9. Verify that the ROS2 Bridge is enabled:

- In Isaac Sim, go to **Window > Extensions**.
- Search for **ROS** in the search bar.
- Confirm that the **ROS2 Bridge** extension is toggled **on**

#### **Open the Simple Room Environment**

Note

Follow the video to guide you through the next steps.

Isaac Sim 4.2Isaac Sim 4.5

9. In Isaac Sim, navigate to

**Content > NVIDIA/Assets/Isaac/4.2/Isaac/Environments/Simple_Room/**

10. Drag and drop the **simple_room.usd** file into the main window.

- Wait a few seconds for it to load completely.
- Place it at the origin by **zeroing out** all Translate components in the Transform Property on the right-hand pane.
- Zoom into the scene until you can clearly see the table within the room.

# LAUNCHING ISAACSIM WITH ROS2

To begin, we need to set up the Isaac Sim environment to publish robot and environment data to your ROS nodes.

1. Open a new terminal by pressing **Ctrl+Alt+T**.
2. Run the following commands in the terminal:

```shell
source /opt/ros/humble/setup.bash
```

This ensures that your terminal is sourced for ROS 2 (Humble).

---

#### **Understanding the Integration**

Isaac Sim acts as a simulation platform that can interact with ROS 2 through its built-in tools and extensions. In this step, we will ensure that the simulation environment is configured correctly to publish data such as sensor readings, odometry, and robot states to ROS topics.

---

#### Review: Verifying ROS Sourcing

Before proceeding, confirm that your terminal is properly sourced for ROS 2:

1. Run the following command:

```shell
echo $ROS_DISTRO
```

2. If the output does not display humble, re-run the sourcing command:

```shell
source /opt/ros/humble/setup.bash
```

---

#### **Launch Isaac Sim**

From the terminal we were just working in, run the following commands.

1. Navigate to the Isaac Sim directory:

```shell
cd ~/isaacsim
```

2. Run this command to launch Isaac Sim:

```shell
./isaac-sim.sh
```

**Wait for Isaac Sim to fully load.**

- Ensure that no errors appear in the terminal before proceeding.

# PUBLISH A LIDAR GRAPH
We will start by publishing the synthetic lidar pointcloud generated by Isaac Sim to ROS

1. In Isaac Sim, go to **File > Open**
2. Open the Nova Carter robot from `~/Desktop/DLI_SIL/Starting_point/nova_carter/nova_carter.usd`
3. In the Stage Tree, right-click the default prim and select **Create > Scope**.
4. Rename the new scope to **Graph**
    - A Scope acts as a container for organizing graphs and related components.
5. Navigate to **Tools > Robotics > ROS 2 OmniGraphs > RTX Lidar**.
    - This shortcut simplifies the process of adding a Lidar graph.

![](https://learn.learn.nvidia.com/assets/courseware/v1/aaa2c4d566f108493005580f18b0b546/asset-v1:DLI+S-OV-39+V1+type@asset+block/image3.png)

6. In the window that appears, set the Graph Path to: **/nova_carter_sensors/Graph/ROS_LidarRTX**
7. For the lidar prim, click the Add button and select the following path: **/nova_carter_sensor/chassis_link/XT_32/PandarXT_32_10hz**
    - Press Select to confirm.

It should look like this:

![](https://learn.learn.nvidia.com/assets/courseware/v1/5496a1677d80593bc5bde4b5632bc483/asset-v1:DLI+S-OV-39+V1+type@asset+block/image4.png)

8. Set the Frame ID to: **front_3d_lidar**.
9. Uncheck the box for **Laser Scan**, as it is not needed for this configuration.
10. Check the box for **Point Cloud** to enable publishing point cloud data.

![](https://learn.learn.nvidia.com/assets/courseware/v1/794dfae95ad92454bdd4da2527cd62c2/asset-v1:DLI+S-OV-39+V1+type@asset+block/image29.png)

11. Press **OK** to complete the setup.

You have successfully integrated a Lidar sensor into your simulation environment, preparing it for real-time interaction with ROS nodes in subsequent modules.

# ULTERIORI INFORMAZIONI SU COME COLLEGARE ISAACSIM A ROS2 

Vedi questo link per accedere a tutto il tutorial [tutorial ros2](https://learn.nvidia.com/courses/course?course_id=course-v1:DLI+S-OV-39+V1&unit=block-v1:DLI+S-OV-39+V1+type@vertical+block@5d8db66dad2846aebe517df9e323f41a)