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

The new OutPut Images are stored in the same directory with DCP begining.

[image1]: ./test_images/DCP_solidWhiteCurve.jpg
[image2]: ./test_images/DCP_solidWhiteRight.jpg
[image3]: ./test_images/DCP_solidYellowCurve.jpg
[image4]: ./test_images/DCP_solidYellowCurve2.jpg
[image5]: ./test_images/DCP_solidYellowLeft.jpg
[image6]: ./test_images/DCP_whiteCarLaneSwitch.jpg

The Video's are stored in the CarND-LaneLines-P1 directory.
[video1]: ./white_FirstTry.mp4 "Initial try with output as grayscale video"
[video1]: ./white_secondTry.mp4 "Second try with output as color video"
[video1]: ./white.mp4 "First Video for output for this project"
[video1]: ./yellow.mp4 "Second Video for output for this project"
Did not worked on the futher Challenge.
---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps as follows: 

Step 1: Create the GrayScale Image by calling the grayscale(image) function and passing the impage to it.

Step 2: Now that we have the grayscale image Define a kernel size for Gaussian smoothing / blurring. Call the function gaussian_blur(grayscaled_image,kernel_size) to get the image modifed.

Step 3: Apply the Canny transform by calling the canny function with smoothen image and threasholds canny(blur_gray_image, low_threshold, high_threshold)

Step 4: Define the Hough transform parameters and call the function hough_lines(masked_edges, rho, theta, threshold, min_line_length, max_line_gap) this function returns an image with hough lines drawn.

In order to draw a single line on the left and right lanes the draw_lines(img, lines, color=[255, 0, 0], thickness=10) function is called from the hough_lines function

After reading the instructions to modify the Draw line function, decided to use the for loop iteration for the line object

first iteration is for the Minimum & Maximum Y values initialization, the next iteration is to determine the slope ((y2-y1)/(x2-x1)) that helps to decide which segments are part of the left line vs. the right line. Once the left & right segments are sorted out the average of the position of each of the lines is calculated and used to extrapolate the top and bottom of the lane.


###2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when there is significant curve on the road the starting of the line do not adjust closer to the lane. 

Another shortcoming could be if there are marker or spots in the middel of lane can cause the lane line to fork.


###3. Suggest possible improvements to your pipeline

A possible improvement would be to better use of lenear regression to speedup and elimiate the loops in the draw_line function 

Another potential improvement could be to finetune the parameter to smoothen the flickering