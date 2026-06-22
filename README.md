# ECE-148---Autonomous-Vehicle
This repo host deliverables for the autonomous vehicle I co-developed in a team of 4 for UCSD SP26 ECE/MAE 148

<img width="432" height="324" alt="ece148_car" src="https://github.com/user-attachments/assets/f32db245-236c-4bf2-826c-a6b7ebff456a" />

## Designs
The vehicle is being built on top of a standrad RC car skeleton, where as the frame, suspensions, and motor are provided to us. We begin to assemble the electronic parts by soldering and wiring, designing and 3D printing mounts, and making architectural decisions for the vehicle.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/3af3e08d-fc7f-4ccc-ad11-608f28bdeea2" />
<img width="600" alt="image" src="https://github.com/user-attachments/assets/4d39cf46-210a-450c-a1a9-d55de141c7af" />




## Simulation
Like every real life projects, starting with a simulation is always the best idea to put our product in an ideal working environment and test out it's feature and core functionality. 

Here, individually, we have to train a model for 20 + laps on a VM by collecting image data of 20 Hz and user's input (including steering angle, throttle responses). Then we feed the training data into a Convulution Neural Network to train our first ever SIM model, so that it can learn our driving behaviour. 
**Finally, I enabled the trained model to run on an external server, that can be viewed on the class' Twitch account, and it successfully ran 3 laps, avoiding cones, and stays on the tracks.**

Video Demo here: https://youtu.be/3qjLKubMgZI
[<img width="1382" height="635" alt="image" src="https://github.com/user-attachments/assets/fe8bad37-a444-409a-a1ca-ed183d8e2779" />
](https://youtu.be/3qjLKubMgZI)

## Sim-to-Real
Now that we've learned how the simulation is, it's time to put it to the real test. As usual, real life never happens as expectation.

The biggest difference between Sim and Real are external factors on the lighting changes throughout the day, the people moving in and out during training and testing, the cones located differently. Furthermore, software compatibility issues that may or may not because of hardwares malfunctioning (motor blown, VESC did not work), loose electrical soldering, 3D-print products does not fit or broken on impact, etc. 

We spent lots of time collecting hundreds of thousands of data, before train the model and test it out on the same track in a random time of the day. **Here is the result**: https://drive.google.com/file/d/1RZqxMx_XRgKJ_EpIpjLJyVNuLOrXb9V5/view

## ROS2 Lap
The purpose of this laps is we want the car to move autonomously on the right hand side of the yellow lane only, so we uses ROS2 with some color filter and fine-tuning driving behaviors.



