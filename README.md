# HRI-20069: Introduction to S/W developmental tools & perception technologies 

Linux Laptop required!!!

## Week 2: Git (Version Control)

### Install git & sign up for github.com
In Ubuntu 16.04, git is already included, but for the other OS please refer to https://git-scm.com

  * References:
    * https://git-scm.com/book/en/v2
    * https://opentutorials.org/course/2708

### First-Time Git Setup
  * Configure the git
    ** Your Identity
    ```
    $ git config --global user.email "you@example.com”  
    $ git config --global user.name "Your Name"
    ```   
    ** Your Editor
    ```
    $ git config --global push.default simple
    $ git config --global core.editor vi           # Using vi editor for git
    ``` 
    ** Checking Your Settings
    ```
    $ git config -l
    user.name=John Doe
    user.email=johndoe@example.com
    color.status=auto
    color.branch=auto
    color.interactive=auto
    color.diff=auto
    ...
    ```

#### [1] '01_docker_ros' branch: build a ros-tutorial Dockerfile and do 'docker run'
If you've already cloned this repository, then you can just checkout the 01_docker_ros branch as
  ```
  $ git checkout 01_docker_ros
  ```
  or make a branch called 01_docker_ros and checkout as well like
  ```
  $ git checkout -b "01_docker_ros"
  ```
  
Make a Dockerfile like
  ```
  $ vi Dockerfile
  
  # This is a Dockerfile for ros:ros-tutorials
  FROM ros:indigo-ros-base

  ENV ROS_DISTRO indigo

  # install ros tutorials packages
  RUN apt-get update && apt-get install -y \
      ros-indigo-ros-tutorials \
      ros-indigo-common-tutorials \
      && rm -rf /var/lib/apt/lists/*
  ```
Also, prepare ros_entrypoint.sh file like
  ```
  $ vi ros_entrypoint.sh
  #!/bin/bash
  set -e

  # setup ros environment
  source "/opt/ros/$ROS_DISTRO/setup.bash"
  exec "$@"
  ```
Build a docker image as
  ```
  $ docker build -t hri/ros:ros-tutorials .
  ```
Check that your image has been built by
  ```
  $ docker images 
  REPOSITORY            TAG                    IMAGE ID            CREATED             SIZE
  hri/ros               ros-tutorials          616da3279f76        5 days ago          1.06GB
  ```
Make the following three files: start_master.sh, start_talker.sh, and start_listener.sh
Make a start_master.sh 
  ```
  docker run -it --rm \
    --net foo \
    --name master \
    hri/ros:ros-tutorials \
    roscore
  ```
And make it executable by
  ```
  chmod 755 start_master.sh
  ```
Make a start_talker.sh 
  ```
  docker run -it --rm \
    --net foo \
    --name talker \
    hri/ros:ros-tutorials \
    rosrun roscpp_tutorials talker
  ```
And make it executable by
  ```
  chmod 755 start_talker.sh
  ```
Make a start_listener.sh 
  ```
  docker run -it --rm \
    --net foo \
    --name listener \
    hri/ros:ros-tutorials \
    rosrun roscpp_tutorials listener
  ```
And make it executable by
  ```
  chmod 755 start_listener.sh
  ```

Create a bridge network called foo if you haven't done before.
  ```
  $ docker network create foo
  ```

Now, see what happens by typing the following commands in different command windows.
  ```
  $ ./start_master.sh
  ```
  ```
  $ ./start_talker.sh
  ```
  ```
  $ ./start_listener.sh
  ```
  
#### [2] '02_docker_ros_compose' branch: build & run a ros-tutorial Dockerfile using 'docker-compose'

