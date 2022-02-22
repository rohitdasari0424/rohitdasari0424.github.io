# Get Started

<p style = "font-weight : 300; font-size : 24px;">
This section will go over the step-by-step process on how the path follower works
</p>

---

> [!ATTENTION]
> This page is for both Tank and Mecanum Drivetrains.

> The first step of the algorithm is making the path
> The path-follower algorithm works with 5 steps that run in a loop till the robot reaches the end of the path:
>- Get the robot location
>- Extend a circle about the robot's center (x , y) with radius (lookahead distance)
>- Calculate intersections between this circle and each segment of the path
>- Calculate which intersection is closest to the end of the path and set this as lookahead point
>- GoToPoint(lookaheadPoint)


### Creating the path

The first step before starting the path follower algorithm is to create the [path](/path-term) for the robot to follow. Each point of the path will have it's own characteristics such as:

- `x`: x coordinate of the point on the field
- `y`: y coordinate of the point on the field
- `movementSpeed`: speed the robot should go at while on that line segment
- `lookaheadDistance`: lookahead distance for that line segment
- `faceTowardsAngle`: determines if the robot should point towards the target point

<figure align="center">
    <video id="sampleMovie" src="Images/create_path.mov" height = "100%" width = "100%" style="border-radius: 1.5%" controls></video>
    <figcaption class="mt-2 text-sm text-center text-gray-600">A robot path using a set of points</figcaption>
</figure>

---

### Get Robot Location

The first step of the Path-Follower is getting the location of the robot. The location of the robot can be denoted by: (`x , y , heading`) where
`x` is the x position of the robot, `y` is the y position of the robot, and `heading` is the angle at which the robot is facing. The robot locations
is used to calculate the lookahead point and the motor powers.

<figure align="center">
    <video id="sampleMovie" src="Images/robot_location.mov" height = "100%" width = "100%" style="border-radius: 1.5%" controls></video>
    <figcaption class="mt-2 text-sm text-center text-gray-600">The robot location on the field</figcaption>
</figure>

---

### Line Circle Intersection

Using the robot's (x , y) position as the center of the circle and the lookahead distance as the radius, a circle is intersected
with each line segment of the path.

<figure align="center">
    <video id="sampleMovie" src="Images/lookahead_circle.mov" height = "100%" width = "100%" style="border-radius: 1.5%" controls></video>
    <figcaption class="mt-2 text-sm text-center text-gray-600">Intersect the circle with the path</figcaption>
</figure>

---

### Find lookahead

The next step is to find the distance between each of the intersections and the end of the path. The intersection closest to the end of the path is the lookahead point.
When the next loop runs and the robot is at a new (x , y) position, the lookahead point would be different since the center of the circle would've changed. This essentially makes the lookahead point constantly change allowing the robot to progress along the path. When the robot gets within a distance from the end of the path, the lookahead point is set to the last point of the path.

<figure align="center">
    <video id="sampleMovie" src="Images/check_distance.mov" height = "100%" width = "100%" style="border-radius: 1.5%" controls></video>
    <figcaption class="mt-2 text-sm text-center text-gray-600">Check the distance between each intersection and the end of the path</figcaption>
</figure>

---

### Go To Position

The next step is to get the robot to move towards the direction of the lookahead point. We do this using the GoToPosition() method which runs one time
and uses three Controllers:
- `TURN_CONTROLLER`: PID Controller for error between the target heading and current robot heading
- `STRAFE_CONTROLLER`: PID Controller for the x error between the lookahead.x and robot.x
- `DRIVE_CONTROLLER`: PID Controller for the y error between the lookahead.y and robot.y

It then uses the mecanum kinematic equations to calculate power for the individual motors using these three movement variables and sets it.

---

### Running the loop again

Now that the robot has moved towards the direction of the lookahead point, the robot's location (x, y, heading) would've changed. This would cause
the lookahead point to change as well. The loop constantly runs until the robot reaches the last point of the path.

---

<figure align="center">
    <video id="sampleMovie" src="Images/follow_path.mov" height = "100%" width = "100%" style="border-radius: 1.5%" controls></video>
    <figcaption class="mt-2 text-sm text-center text-gray-600">Robot follows path using the path follower while keeping a target heading of 0.</figcaption>
</figure>

---

<figure align="center">
    <img src="Images/field-centric-pure-pursuit-implementation.gif" class="rounded-lg" alt="Example of field-centric pure pursuit" style="border-radius:1.5%;">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Path follower in action</figcaption>
</figure>

---

To make the robot follow the path faster, the `movementSpeed` of each point in the path could be adjusted. Likewise, to make the robot face towards the lookahead point while following the path, the `faceTowardsAngle` of each point in the path can be adjusted.

--- 

<p style = "font-weight : 300; font-size : 24px;">
This concludes the step-by-step process of the path follower.
</p>
