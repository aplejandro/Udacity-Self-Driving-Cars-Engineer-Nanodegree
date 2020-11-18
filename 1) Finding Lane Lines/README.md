# **Finding Lane Lines on the Road** 

## Project 1 Udacity Self-Driving Cars Nanodegree

### Iván Alejandro Ávila Gonzalez

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/SolidWhiteCurve.jpg "SolidWhiteCurveLane"

---

### Reflection

### 1. Methodology.

My pipeline consists of 7 steps. First, I converted the images to grayscale using 'cv2.cvtColor', then I applied a gaussian filter ('cv2.GaussianBlur') to this grayscale image, the next step was applying the Canny edge detector ('cv2.Canny'), after that the vertices were defined and modeled as an array, these vertices defined the region of interest (ROI) of the Canny image ('cv2.bitwise_and'), then I aplied the Hough transform in order to determine the lines ('cv2.HoughLinesP') and finally this hough space image was weighted ('cv2.addWeighted').

In order to draw a single line on the left and right lanes, I modified the 'draw_lines()' function by  first using the slope of each line segment to determine which side of the lane it represented.Evidently, lines with positive slope are classified as being on the left lane and lines with negative slope are classified as being on the right lane. Flat lines having slope below absolute value of 0.5 are discarded to avoid outliers that may impact our final averaged lane line. The selected line segment were then averaged to create what should be the most representative lane line segment. I then extended the line segment through the ordered pair to the bottom and mid-point of the graph.



![alt text][image1]


### 2. Shortcomings


One potential shortcoming would be what would happen when the curves are too open, because curves are not straight lines and Hough only consider this type of lines.


Another shortcoming could be when lines are not well defined or they have suffered wear and they could be hard to detect.


### 3. Improvements

A possible improvement would be to define the maximun line length as a very small value, so the curvture will be interpreted as a straight line, another option could be apply and algorithm that detects polynomial curves.

Another potential improvement could be to program an addaptative method, depending on how clear the lines are the program will select the case, each case with different thresholds.
