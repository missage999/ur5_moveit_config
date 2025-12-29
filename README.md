# UR5 MoveIt Configuration

这是一个为UR5机器人配置的MoveIt包，用于运动规划和控制。

## 项目概述

本项目基于MoveIt配置工具生成，用于UR5机械臂的运动规划、控制和仿真。包含了完整的MoveIt配置文件，支持路径规划、碰撞检测、运动执行等功能。

## 配置文件说明

### Launch文件
- `demo.launch.py`: 启动完整的MoveIt演示环境
- `move_group.launch.py`: 启动MoveIt的move_group节点
- `moveit_rviz.launch.py`: 启动RViz可视化界面
- `rsp.launch.py`: 启动机器人状态发布器
- `setup_assistant.launch.py`: 启动MoveIt Setup Assistant
- `spawn_controllers.launch.py`: 启动机器人控制器
- `static_virtual_joint_tfs.launch.py`: 发布静态虚拟关节TF
- `warehouse_db.launch.py`: 启动MoveIt仓库数据库

### 配置文件
- `initial_positions.yaml`: 定义机器人的初始关节位置
- `joint_limits.yaml`: 定义关节限制（位置、速度、加速度）
- `kinematics.yaml`: 定义运动学求解器参数
- `moveit.rviz`: RViz配置文件，包含MoveIt插件设置
- `moveit_controllers.yaml`: MoveIt控制器管理器配置
- `pilz_cartesian_limits.yaml`: Pilz规划器的笛卡尔空间限制
- `ros2_controllers.yaml`: ROS 2 Control控制器配置
- `ur.ros2_control.xacro`: ROS 2 Control硬件接口配置，需要更新加载参数文件的语法。
- `ur.srdf`: 机器人语义描述文件，不需要虚拟关节，因为模型文件已经有world->base_link。末端执行器也可以删掉，因为碰撞关系里面已经包含相机的碰撞信息。如果要添加末端执行器，要给摄像机分成另一个关节组，而非manipulator。
- `ur.urdf.xacro`: 机器人URDF描述文件（Xacro格式）

## 项目修改点

### 1. 初始位置配置
- 在`config/initial_positions.yaml`中定义了UR5机器人的初始关节位置
- 为所有6个关节设置了默认的初始角度值
- 需要和gazebo统一

### 2. 关节限制配置
- 在`config/joint_limits.yaml`中定义了详细的关节限制
- 包括位置、速度和加速度限制

### 3. 运动学配置
- 在`config/kinematics.yaml`中配置了运动学求解器参数
- 针对UR5机器人的特性进行了优化设置

### 4. 控制器配置
- `config/ros2_controllers.yaml`定义了ROS 2 Control控制器
- `config/moveit_controllers.yaml`定义了MoveIt控制器管理器配置，需要添加命名空间
- 配置了`manipulator_controller`用于轨迹控制
- 配置了`joint_state_broadcaster`用于状态反馈

### 5. RViz可视化
- `config/moveit.rviz`包含了预配置的RViz布局
- 集成了MoveIt Motion Planning插件

## 使用方法

### 启动演示环境
```bash
ros2 launch ur5_moveit_config demo.launch.py
```

### 启动Move Group
```bash
ros2 launch ur5_moveit_config move_group.launch.py
```

### 启动RViz可视化
```bash
ros2 launch ur5_moveit_config moveit_rviz.launch.py
```

### 启动Setup Assistant
```bash
ros2 launch ur5_moveit_config setup_assistant.launch.py
```

## 依赖项

- ROS 2 Humble Hawksbill
- MoveIt 2
- UR5机器人描述包
- ROS 2 Control

## 项目结构

```
ur5_moveit_config/
├── config/
│   ├── initial_positions.yaml
│   ├── joint_limits.yaml
│   ├── kinematics.yaml
│   ├── moveit.rviz
│   ├── moveit_controllers.yaml
│   ├── pilz_cartesian_limits.yaml
│   ├── ros2_controllers.yaml
│   ├── ur.ros2_control.xacro
│   ├── ur.srdf
│   └── ur.urdf.xacro
├── launch/
│   ├── demo.launch.py
│   ├── move_group.launch.py
│   ├── moveit_rviz.launch.py
│   ├── rsp.launch.py
│   ├── setup_assistant.launch.py
│   ├── spawn_controllers.launch.py
│   ├── static_virtual_joint_tfs.launch.py
│   └── warehouse_db.launch.py
├── CMakeLists.txt
└── package.xml
```

## 版权和许可证

此项目基于MoveIt配置工具生成，遵循相关开源许可证。