This project is a part of:  
 [![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

# **Finding Lane Lines on the Road** 

This is simple lane finding algorithm.   
P1.ipynb is provided to demonstrate the method.

[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteRight.jpg "Sample output"

![alt text][image1]

### 1.  Pipeline description 

Pipeline consisted of 5 steps. 
 - **Gaussian Blur**  
  This method was used to remove compression artifacts and very detailed parts of image

 - **Canny edge detection on R,G,B channes separately**  
   Canny edge detection is performed on 3 channels separately and then merged. Doing that instead of grayscale is to contain more edges referring do color details (on grayscale image yellow lane can dissappear in some ighting contions)

 - **Two regions of interests (ROIs)**  
   To apply specific lines slopes range spearate processing is done for left and right side of video

 - **Detect Hough lines for ROIs**  
   Hough lines are searching for lines after canny edge detection. The found lines are filtered by allowed slope range.
   hough_lines was equipped with new parameter (method to filter the lines is passed)

 - **Average and extrapolate hough lines**  
   All lines on left and right are separately averaged and exrapolated to fit corresponding ROI

 - **Merge ROI branhces, draw lines, produce output**  


The sample output of lane detection looks like below:


### 2. Identify potential shortcomings with your current pipeline

One potential shortcoming would be what would happen when the lanes are chnaged in rapid manner: the allowed line slope range could cause lanes not to be recognized.

Another shortcoming could be that different lighting conditions (like night, rain etc.) could cause simmilar isuses to dissappearing left lane in challenge video. 

Using windscreen wipers could also introduce some false lines for edge detecion in slope range and cause averaged lane line to be less accurate.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to address lane consistency. Remembering some number of last results could fill any single missing frmaes. Also moving average could cause line to be more stable. 

Another potential improvement could be to inroduce neural network to be sure what is lane line and what is not to focus only on proper edges.