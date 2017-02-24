#**Finding Lane Lines on the Road**

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipe line consisted of following steps:

First converted image to gray scale
Added gausian blur to grayscale image
Detected edges using canny edge detection. I used auto canny function which selects the best params based on image. Used this resource as reference
http://www.pyimagesearch.com/2015/04/06/zero-parameter-automatic-canny-edge-detection-with-python-and-opencv/
Then I found hough lines and extrapolated them and drew it on the final image.


Draw lines modification:

First I got all co ordinates from HoughLinesP function and calculated the slope of the points.
All points having positive slope belong to right lane and negative slope belong to left lane.
I segregated points into right lane and left lane and fitted a y=mx+c equation using the linalg.lstsq function of numpy.
This gave me the m and c of the line and I drew line using the calculated slope and intercept.

For the challenge video. I kept a running average of mean and intercepts for last 20 frames.
This approach is not giving good results yet. have to debug and see wheres the issue.
Will fix this in my next submission


Problems I am facing with the project:

My Lane lines are extending beyond the road. I reduced the region of interest but it gives not so good results.
Lane detection for challenge video is not that good even with running average of slope and intercepts.




###2. Identify potential shortcomings with your current pipeline

The region of interest is hardcoded . have to find an automated way of finding region of interest.
I tested my pipeline on some videos recorded by me and the performance was really poor as the videos were shot in low light conditions
and during rainy weather. So this pipeline performs badly when visibility is low.



###3. Suggest possible improvements to your pipeline

Find region of interest automatically.
Does not work good for conditions with low visibility. May be can use a deep learning approach to solve this.

