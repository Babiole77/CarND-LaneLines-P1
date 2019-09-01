# **Finding Lane Lines on the Road** 
<img src="https://github.com/Babiole77/CarND-LaneLines-P1/blob/master/media/solidYellowLeft.gif" width="700" height="400" />

The pipeline consists 5 steps:
	- an original image is converted to a grayscale image
	- gaussian filter is applied
	- canny edge detector is used
	- trapezoid region of interest is combined with the resulted image from canny edge detector
	- hough transformation is used in order to find lines

The function for drawing lines has been modified in the following way:
	- slope for the lines is calculated
	- lines with positive and negative slopes are separated
	- median value for positive and negative slopes are calculated
	- some lines are filtered out based on their slopes relative to median slope
	- least squares esimation(LSE) is used to draw line through remaining points: one line for points on the lines with positive slope and another line for points on the lines with negative slope
	- the lines from LSE are drawn starting from bottom of image

Lane finding algorithm's performance depends on hyperparameters that have to properly tuned. Therefore, currently used
parameters have been tuned based on given images and it could have problem when applied to other images containing different range of colors. In this case an automatic or adaptive tuning of hyperparameters(e.g. gridsearch) on many images could help to find optimal parameters. 
Another problem could appear if position of the lane on the image changes. This can happen on roads big curvatures or on crossroads. 
   