# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

Setup
---

**Step 1:** Set up the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) if you haven't already. Follow the instuctions for setup.

**Step 2:** Open the code in a Jupyter Notebook. Use this command to start a new notebook in your browser.

`> jupyter notebook`

A browser window will appear showing the contents of the current directory.  Click on the file called "P1.ipynb". A more detailed description of the pipline and steps are decribed in this file along with the code. The notebook allows you to run steps individually to visually understand the process for filtering.


Reflection
---
Pipeline as shown above:
    1. Grayscale - to simplify image processing
    2. Gaussian Blur - to remove noise
    3. Canny edges - to get lane line markings
    4. ROI - to remove excess noise and focus on lanes
    5. Hough Lines - fit lines with correct slopes to average 2 lane markings
    
draw_lines function:
    A draw lines function was created for the hough lines step in order to create straight line markings for the video. I used a for loop to process each line that was returned by the canny function. This returned a set of points for each line which could be converted into slopes using the slope formula. I used a slope_threshold to divide them into either a left lane or a right lane. The lines were then averaged and extrapolated using the polyfit and poly1d functions which created a fitted line. The function then returns these two fitted lines, one for the left lane and one for the right lane.

Potential shortcomings and possible approaches:

One potential shortcoming would be if we introduce curving lane lines or the image gets distorted to make it appear so. My functions are tuned for straight lines at the moment. In order to account for more curvy lines I would have to modify my draw lines function in order to fit lines to a higher degree or to possibly break the canny lines into shorter line segments to account for curves.

