# Dummy Control 包使用指南

欢迎使用 `dummy_control` 包！这个包提供了对 Dummy 机械臂的仿真和控制功能。

## 1. 编译和初始化工作空间

每次修改了代码或第一次使用时，需要编译工作空间并 source 环境变量。
打开终端（Terminal），依次输入以下命令：

```bash
# 进入你的工作空间目录
cd ~/dummy_control_ws

# 编译代码包
colcon build

# 加载环境变量（这一步非常重要，否则系统找不到你的包）
source install/setup.bash
```

> **提示**：每次新开一个终端窗口，都需要执行一次 `source install/setup.bash`，如果你嫌麻烦，可以把它加到 `~/.bashrc` 文件中。

---

## 2. 启动仿真环境

我们提供了一个非常方便的启动文件(`launch file`)，可以一键启动模型显示(RViz2)以及控制器。

如果你**只需要在 RViz2 中查看模型**，运行：
```bash
ros2 launch dummy_control dummy_control_launch.py
```

如果你**想要同时启动完整的物理仿真(Gazebo)**，请加上 `use_gazebo:=true` 参数：
```bash
ros2 launch dummy_control dummy_control_launch.py use_gazebo:=true
```

---

## 3. 控制机械臂（重点）

在启动仿真环境的同时，你可以通过指定 `control_file` 参数来选择你要使用的控制脚本。

### 🕹️ 键盘控制

这会弹出一个新的终端窗口，让你通过按键盘来控制机械臂的各个关节运动。

```bash
# 启动 RViz 并使用键盘控制
ros2 launch dummy_control dummy_control_launch.py control_file:=test_dummy_keyboard.py

# 启动 Gazebo+RViz 并使用键盘控制
ros2 launch dummy_control dummy_control_launch.py use_gazebo:=true control_file:=test_dummy_keyboard.py
```

**键盘操作按键说明：**
- `q` / `a` : 控制关节1 (Joint1) 的正/负方向旋转
- `w` / `s` : 控制关节2 (Joint2) 的正/负方向旋转
- `e` / `d` : 控制关节3 (Joint3) 的正/负方向旋转
- `r` / `f` : 控制关节4 (Joint4) 的正/负方向旋转
- `t` / `g` : 控制关节5 (Joint5) 的正/负方向旋转
- `y` / `h` : 控制关节6 (Joint6) 的正/负方向旋转
- `z` : 让所有关节一键回到零位（初始状态）
- `x` : 退出键盘控制程序


## 问题排查
1. **找不到包或文件**：检查是否执行了 `source install/setup.bash`。
2. **键盘按了没反应**：确保选中了包含“键盘控制说明”的**那个新弹出的终端窗口**再按键。对于 Gazebo 控制，如果一开始模型坍塌或者不响应，请尝试重置或稍微等待物理引擎加载。
