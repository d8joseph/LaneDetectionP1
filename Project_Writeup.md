#**Finding Lane Lines on the Road** 

##Daniel Joseph

---

**Finding Lane Lines on the Road**

[//]: # (Image References)

[Original]: ./Process/orig.png "Original Image"
[Gray]: ./Process/gray.png "Grayscale"
[BlurGray]: ./Process/blur_gray.png "Gaussian blur"
[Canny]: ./Process/canny.png "Canny Transform"
[Mask]: ./Process/mask.png "Region of Interest"
[Hough]: ./Process/hough.png "Lines found using Hough Transform"
[Final]: ./Process/final.png "Detected Lane Lines"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of the following steps:
![alt text][Original]
* Convert the given image to grayscale
![alt text][Gray]
* Apply gaussian blur on grayed image to suppress noise and smooth out gradients by averaging
![alt text][BlurGray]
* Run canny edge detection on image from previous step to find the strong edges
![alt text][Canny]
* Apply a mask on the canny edge detected image to filter out the region of interest - the field of vision within 
which lanes lines are expected to be
![alt text][Mask]
* Apply Hough transform on the image from the previous step to find lines in our image
![alt text][Hough]
* Finally we superimpose our lines onto the original image. 
![alt text][Final]

Modifications done to draw_lines:
I modified the draw lines function to filter out the left and right lane lines based on their slope. The right lane line will have positive slope, and the left lane line will have negative slope. Then I found:
 *the highest and rightmost point (X1,Y1), and the lowest and leftmost point (X2,Y2) for the left lane line
 *the highest and leftmost point (X1,Y1), and the lowest and rightmost point (X2,Y2) for the right lane line
Then using the slope of the lane lines, I extrapolated them to the bottom of the image. I also increased thickness of the line to make it more visually appealing.




###2. Identify potential shortcomings with your current pipeline

One of the shortcomings that I noticed was with the challenge video. The polygon used to filter out the region of interest needs to be modified according to the curvature of the road.

Another shortcoming is that with canny edge detection, the pipeline currently also picks out the edges between silver rims and black body of a car in the adjacent lane


###3. Suggest possible improvements to your pipeline

An improvement would be to continually change the shape of the region we're filtering out based on steering input.

Another improvement would be to average out the lines over short intervals so we have smooth lane detection/