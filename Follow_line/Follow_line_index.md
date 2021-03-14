# Follow line exercise

## Index
[Step 1: Post 13/03/2021 - Introduction](#step-1:-Introduction)
[Step 2: Post 14/03/2021 - Proportional controller implemented](#step-1:-Proportional controller implemented)

## Post 13/03/2021 - Introduction

This blog will document “the follow line” exercise from Unibotics.org web page for the master’s degree Artificial Vision. 
In this exercise the main goal is to follow a red line which is in the middle of the track and try to complete the lap in the shortest possible time. Less than 1 minute it’s a good time lap to accomplish it.

On this site there is an online editor to type our codes with two libraries to move the car and to get the different images from the simulator. The libraries provide different methods to control the car like:
* HAL.motors.sendV()
* HAL.motors.sendW()
* HAL.getImage()
* GUI.showImage()

Also it is important to know that the range of the speed is 0-5 and the range of the angular velocity is -0.5-0.5, being the negative numbers to turn right and the positive numbers to turn left. 

Knowing that the line is always red, our first approach to complete the exercise has been doing a color filter, getting a binary image where only the line is visible. The results that have been achieved are these:
<p align="center">
  <img src="images/maskLine.png" alt="Filter color image" width="55%" />
</p>

With this approach the car can know where is the line and then the different states or actions that can be implemented based on the line location. The different states depend on the difference between the red line location and the middle of the image, so in this case the error will be measure in pixels units. In the next image, the yellow part of the image is the error.

<p align="center">
  <img src="images/error.png" alt="Filter color image" width="55%" />
</p>


With all these things in mind, we can start to implement the different actions that the car has to do based on the error that the color filter tell us. 

## Post 14/03/2021 - Proportional controller implemented

In the first post was explained how the line can be located, so now we are going to implement the first steps to move the car straight forward and try to turn right or left when the car came to a curve.

The first approach is going to be to implement a proportional controller for a constant speed, which is a good one, but it’s easy to correct too much the steering wheel angle in most situations. 
The formula of the proportional controller is: u = −Kp * e, being e the error, Kp a constant, which will be adjust by us based on the experience, and u the steering wheel angle that has to be apply. In this case, the error will measure how much the car have to increase or decrease the steering wheel angle to follow the line. 

Once the controller is implemented, we can see the results on the next video:

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/VoteLytbrWY/0.jpg)](https://www.youtube.com/watch?v=VoteLytbrWY)

As we can see with the proportional controller the car can drive quite consistently, but sometimes, especially in changes of direction, the car is turning to one side bit it is not able to change the direction before crossing the line. 
For this reason, in the proportional controller the Kp constant is adjusted to 0.0015.

So based on the results, the car is already quite good but it is not driving over the line, because the proportional controller is not enough to correct the steering wheel angle completely.
