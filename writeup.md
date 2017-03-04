# **Finding Lane Lines on the Road** 

## Writeup



### Reflection

### 1. Pipeline description
My pipeline consisted of 5 steps:

#### 1. Color extraction
At this step I've tried a greyscale transformation but I realized that using a combination of red and green channels seems to work better. So, I've extracted red and green color channels from the image.

#### 2. Canny
Apply border detection to green and red channels obtaining two binarized images. Threshold levels were left wide open (0-255) since the pipeline worked pretty well with this levels.
These new binary images are combined with a logical OR function.

#### 3. Region of interest masking
Apply a mask to remove all the non usable parts of the image.

#### 4. Hough
Apply the lines detection function to the binary image obtaining a bunch of lines.

#### 5. Lines separation
Lines are separated using their slope, a positive slope means a right line and viceversa.

#### 6. Linear regression
Perform a linear regression to each set of lines obtaining two master lines. These lines are extended to cover all the range of interest. If linear regression worked ok the obtained lines are then stored into a class to be used in the next frames.

#### 7. Lines drawing
Draw the lines onto the original frame.

#### 8. Smoothing
If linear regression doesn't return valid lines, the previous frame line is drawn instead. This way we get a much mode stable lines.


### 2. Identify potential shortcomings with your current pipeline
The pipeline works pretty well with straight lines, the main shortcoming I think is the curved lines. Maybe a second order linear regression could be used to identify lines.

Another shortcoming could be when image presents heavy color/contrast changes that could means much noise coming into the lines detector. This could cause much noisy lines to merge and maybe the linear regressor could not manage with good results.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be using a second order polynomial regression to manage curved roads/lanes.

Another potential improvement could be include a measurement of the off-center deviation of the car, it could help to maintain the car between the lines. :)

