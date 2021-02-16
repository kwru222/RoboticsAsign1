# RoboticsAsign1
This repository was created for the first assignment for the Spring 2021 ME699: Robotics course at the University of Kentucky.
submitted by: Keith Russell


![URDF](https://user-images.githubusercontent.com/76964531/108121024-25eeff00-7070-11eb-90b7-d4d24eea9340.png)

## Usage
### 1) Clone respoitory
```
cd home/...../parent_directory/
git clone
```

### 2) Run Main Program
```
cd project_folder/
julia
include("main.jl")
```

### 3) Program Functionality
#### There are multiple ways this program can be operated from the terminal:
#### 1. Specifying a point for the end effector
The end effector is attached to one of the two branches of this mechanism by default, and can be directed to any point within reach of the mechanism.  To do this simply enter the following into the terminal while the display window is active:

```
q = [x,y,z]
desired_tip_location = Point3D(root_frame(mechanism), q)
jacobian_transpose_ik!(state, body, point, desired_tip_location)
set_configuration!(vis, configuration(state))
```
Just replace x, y and z with your desired coordinates within the q vector.

#### 2. Adding an end effector to the other branch
To add an end effector onto the other kinematic branch, enter the following commands into the terminal:
```
effector = "link_8"
body = findbody(mechanism, effector)
point = Point3D(default_frame(body), 1.0, 0, 0)
setelement!(vis, point, 0.07)
```

Link 7 has the end effector on it by default.  There is currently no way to only select one effector from the terminal while the program is running.

#### 3. Animating the motion from the current to new state
You can also call a funtion from the terminal that will animate the movement from current end effector postion to a new desired location.

```
animator(x,y,z)
```
Where x, y and z should be replaced by the desired respective coordinates.  This feature is still quite buggy.

## Credit
I would like to aknowledge the sources that helped me create this code.  

First and foremost, Dr. Poonawala's github (specifically the spatial algebra folder) helped provide a basic understanding of URDF's and how to import them into julia code.
https://github.com/hpoonawala/rmc-s21.git

Secondly, I would like to cite julia robotics' offial tutorials for comprising a large section of the main.jl code.
https://juliarobotics.org/RigidBodyDynamics.jl/dev/generated/4.%20Jacobian%20IK%20and%20Control/4.%20Jacobian%20IK%20and%20Control/

