# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer. Edit test

--

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)


[image1]: ./examples/failcase_1.jpg "Fail case 1"
[image2]: ./examples/failcase_2.png "Fail case 2"
---

### Reflection

### 1. Method Description

My lane detection algorithm consists of six steps. First of all, the image extracted from the video is converted into a gray scale image, after that, gaussian smoothing is applied to process the image. Then, the smoothed image is fed in to the canny edge detection function wile a mask (region of interest of the image) is layered on with edges output from canny edge detection function to filter the noise (lines) out of the region of the interest out. Then, the masked image is fed into the Hough transform function, which outputs the coordinates of the lines detected. Finally, the initial detected lines are fed into the draw_line function. 

In the  draw_line function, the line segments ([(x1,x2),[y1,y2]]) are classified into right lines and left lines based on the slop. Note that a minimal slop value is set to filter the horizontal lines out. For each line segment in the right lines group and left lines group, the slop (k) and the intersection point (b) of that line (y = k*x + b) in the image reference frame are calculated and stored in lists. After looping all the lines, the average slop and average intersection are obtained, then the fitted lines can be drawn.    


### 2. Potential Shortcomings
The lane detection works very well on the first two videos compared with the challenge video. The program can detect most of the lines in the video but failed in some frames, as the following figures shown:
![alt text][image1]
![alt text][image2]

The reason for the first case is the little dot white line out side the yellow line  interference the calculated slop and intersection for the yellow line. The reason for the second case is that the road surface experienced color change, which generates an edge that makes the program thinks it’s a lane.    




### 3. Suggestions
To solve the first failed case, the length fed into the draw_line function could be constrained to eliminate the segments with short length. Also, the slopes (k) and intersections (b) calculated by the classified lines (left, right) could be further selected to filter the out layers out. 

To solve the second failed case, the image could be per-processed to eliminate the potential road colors and only keep the white and yellow colors. 

The parameters of the Hough transform could bu further improved.    


