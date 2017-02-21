#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report




---

### Reflection

###1. Pipeline for lane detection.

My pipeline consisted of the following steps.  First the image was converted grayscale as shown bellow
[//]: # (Image References)


[image1]: ./docu_images/gray.jpg "Grayscale"

-
and smoothen with a Gaussian Filter to remove noise. To detect edges in the image, the Canny Detector was used. The result is shown in the following figure

[image1]: ./docu_images/edges.png “Edges”

A region o interests was defined  and the region outside interest is masked as shown below :

[image2]: ./docu_images/masked_edges.png “Masked edges”

Further, lines are extracted from the detected edges with the Hough transformation and the left and right lanes are detected. 

[image3]: ./docu_images/solidWhiteCurve_detect.jpg “Lane detect” 
 
In order to draw a single line on the left and right lanes, I modified the draw_lines() function. The detected segments on the line are filtered into left and right segments based on their slope value.
Only the segments with the slope above a certain threshold are considered to filter out the lines that are at odd angles
The points for the left and right segments are then fitted with a first order polynomial and the parameters for the left and right lane are detected.
For the left and the right lane, lines are then draw between the minimum and maximum points as in the following example

[image4]: ./docu_images/solidWhiteCurve_detect_all.jpg “Lane detect all” 


###2. Potential shortcomings with your current pipeline


One potential shortcoming is the fixed region of interest. If an object would appear in our region of interest, its edges would be detected and can further be interpreted as a line.

Another shortcoming could be the intensity of the light and how the light is reflect by the road surfaces. There is a chance that shadows are on the lane and detected as object. Another problem can be the lack of contrast between the lane markup and the road surface and so no edges are detected.

Another shortcoming for this method is that is working only for a straight road and has difficulties approximating curves. 


###3. Possible improvements to your pipeline

A possible improvement would be to normalise the color space to reduce the effects of light. Another possibility is to improve edge detection by using adaptive thresholds based on the image's characteristics. 

Another potential improvement could be to have a variable region of interest.

