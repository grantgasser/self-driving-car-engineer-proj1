# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: extrapolate.png "Extrapolate"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied Gaussian blur to reduce noise. Next, I used Canny Edge Detector to detect edges in the image. Then, I applied a mask to the image such that only the part where lane lines appear was considered. Lastly, I used Hough to find lines in that region of the image drew them on the original image. 

In order to draw a single line on the left and right lanes, I modified the `draw_lines()` function by first deciding whether a line from the output of `hough_lines()` was part of the left lane or right lane, depending on which half of the image it was. Then, I kept track of the most extreme points of all the lines (separately for each side) and then drew a single line on each side. For example, I found the left and bottommost point and the right and topmost point for the left lane and drew the line between those points.

Result after extrapolation:

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


The main shortcoming of this pipeline is the assumption that the lane lines are straight. For one, the code assumes the lane lines are straight, rather than curved. The challenge.mp4 video reveals this. This assumption is seen in the extrapolation code as well as the region of interest being centered in the image. Obviously, if the lane is curving, the lane will be outside the centered region of interest.

Another scenario that would provide a challenge to this model is hills or changing of the horizon. Again, the region of interest is hard-coded so the lane going up or downhill may cause problems. Even is the camera is fixed on the car, the lanes will not always appear in the region of interest. 


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to sequentially connect lines until there is only one line left. One can think of this as a curved line being many combinations of straight lines. 

Another potential improvement could be to re-calculate the region of interest either for each frame or periodically (every few frames maybe). We have a general idea of where the region of interest is and might be able to derive the proper region of interest for each frame (I'm not exactly sure how to do this.)

I hope dealing with curved lane lines appears later in the course as I would like to learn how to do this.
