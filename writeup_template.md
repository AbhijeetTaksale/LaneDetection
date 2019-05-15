# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. 

First, I converted the images to grayscale, then I applyed gaussian smoothing with gaussion factor of 3 (after tunning). 

Second, I used gaussion image as input to the canny API to detect edges in the image giving min threshold and max threshold as 85 and 125 respectively. 

Third, I created a polygon to select the area of intrest in image/ video using numpy.array and cv2fillpoly functions. Then performed bitwise AND operation with masked image with region selection image. 

Fourth, I applied hough transforamtion on masked edge detected image with 150 and 200 as minLinLength and minLinGap resp. 

Fifth, finally I combined raw image with hough transformed image using add weigthed.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first calculating the slope of lines coming as input to this function from hough transform. Based on the sign of slope and position of line in image w.r.t center , we are drawing seperate line on image.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]

[CarND-LaneLines-P1/test_videos_output/solidWhiteRight.mp4]

[CarND-LaneLines-P1/test_videos_output/solidYellowLeft.mp4]

[CarND-LaneLines-P1/test_videos_output/challange.mp4]

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when camera is not mounted proberly or it was mounted properly but due to some reason it got 
misalligned.

Another shortcoming could be what about night time. Normal cameras won't capture much light at night time and due to which current pipeline wont work.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to crop the image area some what where the car bumper is comming, as it could effect the algorithum. 

Another potential improvement could be to to make region selection dynamic insteaded of stationary. 
for examples, below line should have dynamic values
# Create a four sided polygon to mask
    vertices = np.array([[(130,imshape[0]),(425, 335), (540, 335), (890,imshape[0])]], dtype=np.int32)

The decision should have made based on road condition.	
