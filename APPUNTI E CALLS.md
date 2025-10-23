Giorno 07/10/2025 -> primo meeting con Nunzio dove ho definito gli obiettivi relativi al progetto di Mobile Robotics e Tirocinio/Tesi. 

# OBIETTIVO FINALE 
Implementare su IsaacLAb un robot UGV con Zed-Camera integrata da controllare da joystick e supportato da teleoperazione (deve essere un robot intelligente capace di riconoscere l'ambiente e assistere l'utente quindi utilizzare Collision Avoidance ecc) e con possibilità di implementare ciò che è ottenuto su un robot del laboratorio.

# Suddivisione del progetto
## Mobile Robotics :

Creare una simulazione con il Robot UGV con Zed camera integrata e funzionante tramite ROS2Bridge quindi implementare guida assistita per un DifferentialDrive robot con Central Body function o Artificial potental field e ricavare il tutto su RViz

## Tirocinio e Tesi : 
Implementare il controllo del robot da un visore, quindi controllo il robot come se fossi lontano da lui e non all'interno (sono io a prendere le decisioni per il robot, è come un joystick in cui però sei teleassistito) poi usi l'imitation learning per addestrare il robot a muoversi da solo ma sulla base del tuo processo decisionale.

## Link utili

### IsaacSim

[Link IsaacLab](https://developer.nvidia.com/isaac/lab)

[Link IsaacSim per inizio](https://learn.nvidia.com/courses/course-detail?course_id=course-v1:DLI+S-OV-27+V1)

[Link IsaacLab per ZedCamera](https://www.stereolabs.com/docs/isaac-sim)

[Link IsaacLab per installazione di ROS](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/install_ros.html)

[Core api tutorial: codici python per usare IsaacSim](https://docs.isaacsim.omniverse.nvidia.com/latest/core_api_tutorials/index.html)

[Isaac Documentation](https://docs.isaacsim.omniverse.nvidia.com/latest/core_api_tutorials/index.html)


### Rviz
[link per launch file Rviz](https://docs.ros.org/en/foxy/Tutorials/Intermediate/URDF/Using-URDF-with-Robot-State-Publisher.html#create-a-launch-file)

# Informazioni su IsaacSim 

**Indirizzo IP** : 10.73.0.159

**Cartella dove sono salvati i file del mio Pc** : /workspace/isaaclab/Assets


from pxr import UsdPhysics, PhysxSchema, Gf, PhysicsSchemaTools, UsdGeom

import omni stage = omni.usd.get_context().get_stage()  
 # Setting up Physics Scenegravity = 9.8  
scene = UsdPhysics.Scene.Define(stage, "/World/physics")  
scene.CreateGravityDirectionAttr().Set(Gf.Vec3f(0.0, 0.0, -1.0))  
scene.CreateGravityMagnitudeAttr().Set(gravity) PhysxSchema.PhysxSceneAPI.Apply(stage.GetPrimAtPath("/World/physics"))  
physxSceneAPI = PhysxSchema.PhysxSceneAPI.Get(stage, "/World/physics")  
physxSceneAPI.CreateEnableCCDAttr(True)  
physxSceneAPI.CreateEnableStabilizationAttr(True)  
physxSceneAPI.CreateEnableGPUDynamicsAttr(False)  
physxSceneAPI.CreateBroadphaseTypeAttr("MBP")  
physxSceneAPI.CreateSolverTypeAttr("TGS")

PhysicsSchemaTools.addGroundPlane(stage, "/World/groundPlane", "Z", 15, Gf.Vec3f(0,0,0), Gf.Vec3f(0.7))

path = "/World/Cube"  
cubeGeom = UsdGeom.Cube.Define(stage, path)  
cubePrim = stage.GetPrimAtPath(path)  
size = 0.5  
offset = Gf.Vec3f(0.5,0.2,1.0)  
cubeGeom.CreateSizeAttr(size)  
cubeGeom.AddTranslateOp().Set(offset) 
rigid_api = UsdPhysics.RigidBodyAPI.Apply(cubePrim)  
rigid_api.CreateRigidBodyEnabledAttr(True)  
UsdPhysics.CollisionAPI.Apply(cubePrim)





 



