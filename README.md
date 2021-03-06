# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## The Model
1. General assertion <br>
The coordinates of the car provided by the simulator are in global coordinates. For more simplicity, I transformed theses coordinates with respect to the car (and not to the map). <br>
The state vector of the vehicle is given as follow: 
* x - Vehicle position in forward direction
* y - Vehicle position in lateral direction
* psi - Angle of the vehicle (yaw angle)
* v - Vehicle's speed

And the actuators are:
* delta - Steering angle (radians)
* a - acceleration

2. Update step <br>
The update step can be found [here](https://github.com/Mornor/CarND-MPC-Project/blob/master/src/MPC.cpp#L112) in my code. 
This update step is used to compute the next state of the car, regarding the current state. `Lf` is the distance between the front of vehicle and its center of gravity. This constant was kindly given by Udacity. 

## Polynomial Fitting and MPC Preprocessing
I used a third degree Polynomial to compute the trajectory od the car. A second degree polynomial would have led to underfitting, whereas more than a third degree polynomial would not have allow me to generalize the data enough (overfitting). 

## Timestep Length and Elapsed Duration (N & dt)
Timestep Length and Frequency were chosen by trial and error method.
After some trials, I found that 10 timesteps (`N`) at a frequency of 15 (`dt`) provided the best results, for a speed of 30 mph. 
However, the more speed we would like to achieve, the more we want to "see further", hence it becomes necessary to increase `N`. 

## Model Predictive Control with Latency
The Model Predictive Control handles a 100 millisecond latency which simulate latency between sensors and processing.

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets) == 0.14, but the master branch will probably work just fine
  * Follow the instructions in the [uWebSockets README](https://github.com/uWebSockets/uWebSockets/blob/master/README.md) to get setup for your platform. You can download the zip of the appropriate version from the [releases page](https://github.com/uWebSockets/uWebSockets/releases). Here's a link to the [v0.14 zip](https://github.com/uWebSockets/uWebSockets/archive/v0.14.0.zip).
  * If you have MacOS and have [Homebrew](https://brew.sh/) installed you can just run the ./install-mac.sh script to install this.
* [Ipopt](https://projects.coin-or.org/Ipopt)
  * Mac: `brew install ipopt --with-openblas`
  * Linux
    * You will need a version of Ipopt 3.12.1 or higher. The version available through `apt-get` is 3.11.x. If you can get that version to work great but if not there's a script `install_ipopt.sh` that will install Ipopt. You just need to download the source from [here](https://github.com/coin-or/Ipopt/releases).
    * Then call `install_ipopt.sh` with the source directory as the first argument, ex: `bash install_ipopt.sh Ipopt-3.12.1`. 
  * Windows: TODO. If you can use the Linux subsystem and follow the Linux instructions.
* [CppAD](https://www.coin-or.org/CppAD/)
  * Mac: `brew install cppad`
  * Linux `sudo apt-get install cppad` or equivalent.
  * Windows: TODO. If you can use the Linux subsystem and follow the Linux instructions.
* [Eigen](http://eigen.tuxfamily.org/index.php?title=Main_Page). This is already part of the repo so you shouldn't have to worry about it.
* Simulator. You can download these from the [releases tab](https://github.com/udacity/CarND-MPC-Project/releases).



## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./mpc`.
