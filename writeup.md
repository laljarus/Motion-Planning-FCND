## Project: 3D Motion Planning
In this project the backward_flyer is extended to find an optimal path to an arbitary location in a given map. 

# Steps taken to complete the Project:
1. 2.5D map is loaded from the colliders.csv file describing the environment.
2. The environment is discretized into grid and graphs.
3. The current location of quadcopter is set a starting point and an arbitary point in the map is chosen as goal.
4. A* algorithm is used to perform the search an optimal path.
5. A combination of collinearity test and bresenham algorithm is used to remove unwanted points in the identified path.
6. Waypoints are calculated in the local ECEF coordinates from the 2D path found using A*(format for `self.all_waypoints` is [N, E, altitude, heading]).


## [Rubric](https://review.udacity.com/#!/rubrics/1534/view) Points
### All the rubic points are considered in the project and it is discussed here how each rubic point is implemented.
---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

Project report is done.

### Explain the Starter Code

#### 1. Explain the functionality of what's provided in `motion_planning.py` and `planning_utils.py`

The motion planning project is an extension of backyard flying project. Both the project use the event driven programming paradigm. The major difference between *'backyard_flyer_solution.py'* and *'motion_planning.py'* is that in *'motion_planning.py'* there is an additional state called **PLANNING** where the drone path is calculated using A* algirithm. Whereas in *'backyard_flyer_solution.py'* the waypoints are hard coded.

The starter code of the motion planning project contains some utility funcitons in the *'planning_utils.py'* and there some more funcitons are added, which are used in the path planning algorithm. The following table shows the list functions and their description in the *'planning_utils.py'* 

Name in the function | Description|
|:-|:-|
create_grid| This function creats a 2D grid of the environment based on the data from the **'colliders.csv'** file. This function takes into account the drone altitude and the safe distance that the drone can fly near an obstacles when creating the grid.
Action(enum)| This enum defines the possible movements of the drone which can be used by the path planning algorithm. The following direction are defined in the enum North,East,South,West,North-East,North-West,South-East,South-East,South-West.
valid_actions| This functions checks if all the drone actions(movements) are possible without hitting obstacles for a given location in the grid. 
a_star| This function implements the A* algorithm it calculates the optimal path for a given start and goal location in the grid using the defined drone actions and heuristic function.
heuristic| This function defines the heuristic i.e. it calculates an a cost between the current position and the goal without considering the grid. In this project 2nd order vector norm is used as heuristic
collinearity_check| This function takes in three points and checks if the three points lie in straight line by calculating the area of triangle formed by the three points. This function takes in epislon as parameter which is compared with the area and decided if the points lie in a straight line.


These scripts contain a basic planning implementation that includes...

And here's a lovely image of my results (ok this image has nothing to do with it, but it's a nice example of how to include images in your writeup!)
![Top Down View](./misc/high_up.png)

Here's | A | Snappy | Table
--- | --- | --- | ---
1 | `highlight` | **bold** | 7.41
2 | a | b | c
3 | *italic* | text | 403
4 | 2 | 3 | abcd

### Implementing Your Path Planning Algorithm

#### 1. Set your global home position
Here students should read the first line of the csv file, extract lat0 and lon0 as floating point values and use the self.set_home_position() method to set global home. Explain briefly how you accomplished this in your code.


And here is a lovely picture of our downtown San Francisco environment from above!
![Map of SF](./misc/map.png)

#### 2. Set your current local position
Here as long as you successfully determine your local position relative to global home you'll be all set. Explain briefly how you accomplished this in your code.


Meanwhile, here's a picture of me flying through the trees!
![Forest Flying](./misc/in_the_trees.png)

#### 3. Set grid start position from local position
This is another step in adding flexibility to the start location. As long as it works you're good to go!

#### 4. Set grid goal position from geodetic coords
This step is to add flexibility to the desired goal location. Should be able to choose any (lat, lon) within the map and have it rendered to a goal location on the grid.

#### 5. Modify A* to include diagonal motion (or replace A* altogether)
Minimal requirement here is to modify the code in planning_utils() to update the A* implementation to include diagonal motions on the grid that have a cost of sqrt(2), but more creative solutions are welcome. Explain the code you used to accomplish this step.

#### 6. Cull waypoints 
For this step you can use a collinearity test or ray tracing method like Bresenham. The idea is simply to prune your path of unnecessary waypoints. Explain the code you used to accomplish this step.



### Execute the flight
#### 1. Does it work?
It works!

### Double check that you've met specifications for each of the [rubric](https://review.udacity.com/#!/rubrics/1534/view) points.
  
# Extra Challenges: Real World Planning

For an extra challenge, consider implementing some of the techniques described in the "Real World Planning" lesson. You could try implementing a vehicle model to take dynamic constraints into account, or implement a replanning method to invoke if you get off course or encounter unexpected obstacles.


