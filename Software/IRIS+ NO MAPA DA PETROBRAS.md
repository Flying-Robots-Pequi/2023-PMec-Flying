# Tutorial drone IRIS+ no mapa da competição da Petrobras ᕕ( ᐛ )ᕗ
O procedimento a seguir ensina como utilizar o repositório do PX4-Autopilot para spawnar o drone IRIS+ no mundo da competição da Petrobras (o que foi feito até agora ) e para continuarmos com o procedimento é necessário termos feito todo o processo descrito no arquivo Download PX4-Autopilot,se feito continue   (　＾∇＾).
### Dê git clone no mapa da competição:
    git clone https://github.com/LASER-Robotics/Petrobras_Competition.git

#### Agora acesse o workspace que foi utilizado para a instalação do MAVROS para instalar o plugin gazebo (o meu workspacese chama catkin_ws, modifique-o para o nome dado por você):

    cd catkin_ws/src
    git clone https://github.com/ros-simulation/gazebo_ros_pkgs.git -b noetic-devel
    rosdep update
    rosdep check --from-paths . --ignore-src --rosdistro noetic
    cd ..
    catkin build
    source devel/setup.bash

#### Ainda em catkin_ws/src iremos criar um package para adicionarmos o mundo da competição:
    catkin_create_pkg petrobras_challenge
 
#### Arraste os arquivos launch,models,start,worlds,cmakelists e package contidos na pasta Petrobras_Competition para dentro da pasta petrobras_challenge (esse processo eu fiz manualmente nos arquivos,mas faça do jeito que lhe convém °˖✧◝(⁰▿⁰)◜✧˖°)
    cd ..
    catkin build

#### Novamente em catkin_ws/src,clone:
    git clone https://github.com/ctu-mrs/mrs_simulation.git

#### Feito o procedimento todo,tente abrir seguindo os seguintes comandos em terminais diferentes:
1-Terminal 1 (abrirá o px4):

     roslaunch px4 px4.launch
2-Terminal 2 (abrirá o mapa da competição):

    roslaunch petrobras_challenge simulation.launch world_name:=fase1 gui:=true
    
O termo -fase1- pode ser mudado de 1 a 4, alterando o mapa para dada fase da competição.  

3-Terminal 3 (inserção do drone):

    rosrun gazebo_ros spawn_model -sdf -file $(pwd)/PX4-Autopilot/Tools/simulation/gazebo-classic/sitl_gazebo-classic/models/iris_opt_flow/iris_opt_flow.sdf -model iris -x 0 -y 0 -z 0 -R 0 -P 0 -Y 0

#### Caso queira, dê ./QGroundControl.AppImage em outro terminal para controlar o drone via qgroundcontrol.
