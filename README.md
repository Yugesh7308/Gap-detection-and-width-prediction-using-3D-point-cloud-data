The process involves five main steps: reading and analyzing the Point Cloud Data (PCD), identifying 2D Regions of Interest (ROI), cropping the point cloud data, drawing lines along the y-axis for different y-values, and projecting those lines on the xz-plane to calculate gap widths. Below, we detail each of these steps:

STEP 1 - Reading and Analyzing PCD Data
•	Objective: The primary goal of this step is to understand the structure and components of the Point Cloud Data (PCD).
•	Action: Read the PCD file. This involves loading the PCD into the processing environment and performing an initial analysis to understand its structure, including the distribution and density of points.


STEP 2 - Identifying 2D Regions of Interest (ROI)
•	Objective: To locate specific areas within the PCD that are critical for gap analysis.
•	Action: Train a Yolov8 model to predict the gap regions. This step involves using the Yolov8 object detection algorithm to identify and mark regions of interest within the PCD that are likely to contain gaps between vehicle parts.


STEP 3 - Cropping Point Cloud Data
•	Objective: To select the required point cloud data for detailed gap analysis.
•	Action: Crop the PCD using the coordinates min_x, max_x, min_y, and max_y. By isolating the regions of interest identified in Step 2, we refine the dataset to focus only on the relevant areas, reducing computational load and enhancing analysis precision.


STEP 4- Drawing Lines along the y-axis for Different y-values
•	Objective: To find uneven gap widths along different sections of the vehicle part.
•	Action: The gap is calculated using the average of gaps along all the defined lines. This involves:
o	Declaring the interval at which the lines should be drawn. In this case, lines are drawn at every 10% interval.
o	Defining min_y as the starting line and max_y as the ending line.
o	The difference between y_max and y_min is multiplied by increments of 0.1, 0.2, ..., 0.9, and added to y_min to get the points at which lines need to be drawn.
o	A tolerance of 0.03 is used to ensure that points are available at the given y-values.
o	Drawing these lines along the y-axis helps in identifying variations in gap widths across different segments.


STEP 5 - Projecting Those Lines on the xz-plane
•	Objective: To calculate the gap width, defined as the difference between the start point of the next segment and the end point of the current segment.
•	Action: Calculate the Euclidean distance between consecutive segments and name this distance as the gap. Projecting the lines on the xz-plane allows for a straightforward calculation of distances between points, facilitating accurate gap measurement.
