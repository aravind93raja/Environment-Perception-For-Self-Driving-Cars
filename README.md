# Environment-Perception-For-Self-Driving-Cars

This code was written as a Project for the "Visual Perception for Self-Driving Car" Course provided online by University of Toronto.

The python file with the code and the Jupyter Notebook with Outputs and results are provided.

For perception we are provided with the 

1)RGB Image from the camera

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/1.png"> 

2)Depth map of the same

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/depth2.png">

3)Semantic Segmentation of the same

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/segmentation4.png"> <img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/segmentation_table.png">

Perception (A) - Drivable Space Estimation Using Semantic Segmentation Output

Step1 : Estimate x,y,z coordinates 

The equations to get the required 3D coordinates are:

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/xyz_coordinates_formula.png">

Step2 : RANSAC algorithm is used to estimate the ground plane in the 3D camera coordinate frame from the x,y, and z coordinates estimated above

My results of the estimated ground plane:

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/drivable space0.png">

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/drivable_space.png" width="400"> <img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/drivable_space2.png" width="400">

Perception (B) - Lane Estimation Using The Semantic Segmentation Output

Step1 : Estimating Lane Boundary Proposals

a)Create an image containing the semantic segmentation pixels belonging to categories relevant to the lane boundaries, similar to what we have done previously for the road plane. For this assessment, these pixels have the value of 6 and 8 in the neural network segmentation output.

b)Perform edge detection on the derived lane boundary image.

c)Perform line estimation on the output of edge detection.

My Output:

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/b1.png" width="400">

Step2 : Merging and Filtering Lane Lines

a)Get every line's slope and intercept using the function provided.

b)Determine lines with slope less than horizontal slope threshold. Filtering can be performed later if needed.

c)Cluster lines based on slope and intercept.

d)Merge all lines in clusters using mean averaging.

My Output:

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/b2.png" width="400">

Step3 : To extrapolate the lanes to start at the beginning of the road, and end at the end of the road, and to determine the lane markings belonging to the current lane

My Output:

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/b3.png" width="400">

Perception (C) - Computing Minimum Distance To Impact Using The Output of 2D Object Detection

The Output of 2D Object Detection

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/c1.png" width="400">

Step1 : Filtering Out Unreliable Detections

a)For each detection, compute how many pixels in the bounding box belong to the category predicted by the neural network.

b)Divide the computed number of pixels by the area of the bounding box (total number of pixels).

c)If the ratio is greater than a threshold keep the detection. Else, remove the detection from the list of detections.

My Output:

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/c2.png" width="400">

 Step2 : Estimating Minimum Distance To Impact
 
a)Compute the distance to the camera center using the x,y,z arrays from part I. This can be done according to the equation:  𝑑𝑖𝑠𝑡𝑎𝑛𝑐𝑒=Squareroot(𝑥2+𝑦2+𝑧2).

b)Find the value of the minimum distance of all pixels inside the bounding box.

My Output:

<img src="Environment Perception For Self-Driving Cars-Project/photos_for_readme/c3.png" width="400">
