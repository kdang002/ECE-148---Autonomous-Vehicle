# ECE-148---Autonomous-Vehicle
This repo host deliverables for the autonomous vehicle I, Vy Kiet Dang, co-developed in a team of 4 for UCSD SP26 ECE/MAE 148 in less than 8 weeks.

<img width="432" height="324" alt="ece148_car" src="https://github.com/user-attachments/assets/f32db245-236c-4bf2-826c-a6b7ebff456a" />

*Image 1: The final product (as seen above) has been through multiple trials-and-errors, broken on impact, architectural changes, etc.*

## Designs
The vehicle is being built on top of a standrad RC car skeleton, where as the frame, suspensions, and motor are provided to us. We begin to assemble the electronic parts by soldering and wiring, designing and 3D printing mounts, and making architectural decisions for the vehicle.

This was one of the most time consuming, but yet most rewardable step of our time working with this RC car. The foundation of the vehicle needs to be well built, prepare for impacts, rigidity, wiring and soldering must be intact, organized and pleasant on the eye. Our cases and mounts are mostly designed by our "German engineering" teammate, as we handled the printing process, and as we expected, there are many times where the case does not fit, or more parts being added on later that we have to change our architectural layout, which results in many reprints.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/3af3e08d-fc7f-4ccc-ad11-608f28bdeea2" />

*Image 2: Mounting plate and camera holder.*

<img width="600" alt="image" src="https://github.com/user-attachments/assets/4d39cf46-210a-450c-a1a9-d55de141c7af" />

*Image 3: The wiring schematic of all electrical components.*

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
The purpose of this laps is we want the car to move autonomously on the right hand side of the yellow lane only, so we filtered out that the camera can focus on the yellow line and fine-tuning it's driving behaviors to stick to the yellow line.

The biggest challenege about this lap are trials-and-error and lighting shifts, sometimes we have to "hack-the-environment" to reduct background noises. 
There are 6 different variables we have to adjust: 
- HSV color values: For seeing only yellow values
- `error_threshold`: Indicated as redlines on left and right on how wide is the error value such that if the yellow lines fall within, the model makes no steering changes.
- `camera_centerline`: Indicated in green, the center of line recognition, where we placed it left-bias so the car and stay on the right side of the yellow line
- PID steering values: These are 3 values that will control the how it steers in straight, and especially curves and cornering: how sensitive will it react to the changes on the camera, how much steering will it react, and how often will it steer.
- `no_lines`: How many valid line segments to include in the centroid calculation. More lines = more stable on straights, harder to tune on tight curves

**Here is the results**: https://drive.google.com/file/d/1jC_GaAxvshBArW9rVcWhAXsf1CvzBfpQ/view?usp=sharing
<img width="500" alt="image" src="https://github.com/user-attachments/assets/3b955257-fa42-4684-b153-cbd45405748e" />

*Image 4: A look into the RViz for fine-tuning filters and PID steering values.*

## YOLO Detection model:
Using the camera for object recognition, where we will make a "unique" object recognizable, such that the YOLO model has not seen it before. 

We imported the basic Computer Vision object recognition code, then we simply add hundreds of different photos of a black rubber duck and labelled it, and trained the model on that dataset. 

**Here is the result**: https://drive.google.com/file/d/1vYtVr6WZ0WP4KD-TaJ6TGIUskoXzxGa-/view

**This is the foundation for our future final project on building a JeepBot with object recognition.**
<img width="400" alt="image" src="https://github.com/user-attachments/assets/e82e36c1-fa91-4cdc-ab1e-bdc68f438bd1" />

*Image 5: Custom YOLO detection model*

## What we learned
The RC Car is definitely an interesting and fun project that we've done as it is a branch of robotic. There were multiple instances of that showed how "interdisciplined" this field is, such that: 
- Wiring, soldering, connecting electrical components is our Electrical Engineering main strength, but there were so many parts needs to be soldered in time, so we have to learn soldering as well.
- 3D designing is our Mechanical Engineering strength, but there are so many parts need to be designed and printed in time, so we all have to learn how to designs or print
- Fixing software and firmware compatibility is my main strength... but since they are so niche I handled most of it myself as I am the most comfortable in doing it.
- We all required to be on the field to observed, assert, and communicate all the time. So we cannot asssume other people understand each other technical's term, so learning how to explain to a non-technical person is required in our team.

## Conclusion
This course was definitely very time-consuming and grind-intensive. There were many nights we stayed on the field together to collect data, trained on Convulution Neural Network correctly, and run robustly. Just for the next day's lighting kills our model behaviour, and we have to collect even more throughout different daylight time, train again, and finally have it ran. It was a crazy run, but it taught and pushed us out of our comfort zone, learning new materials of other field, communication, scheduling, etc. It was worth it.
 


