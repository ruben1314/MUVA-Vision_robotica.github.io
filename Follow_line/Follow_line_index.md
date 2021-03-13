# Follow line exercise

## Index
[Step 1: Post 13/03/2021 - Introduction](#step-1:-Introduction)

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
