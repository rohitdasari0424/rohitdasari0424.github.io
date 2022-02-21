
# Follow Path

<p style = "font-weight : 300; font-size : 24px;">
This page will implement the followPath() method.
</p>

---

The <b>followPath()</b> will take an ArrayList of path points and follow it by:
- Calculating the lookahead point
- Calculating the heading point
- Calling the goToPosition() method to get to these target points

The method will run a while loop in which all of this takes place.  In this loop, the updateTracker() , lookaheadPoint() , and goToPoisiton() method are constantly called to
get the robot to progress along the path. Each loop takes the robot's new location and brings it to its new target position since lookahead point changes as you move along the path.

## Condition

The condition for the while loop will be called `stopState`. It will store how long we have we been a certain range of error within the destination (last point of the path).
Once you are within a range of error from the destination, the stopState starts, otherwise it is 0.

To implement the stopState, we also need another time variable called startTime which would store the time at which the stopState started so we can keep track of how much time has passed.


## Code Implementation

```java 
    public followPath(ArrayList<Point> path){
        
    }

```

### Stop State

In this section , we will implement the stopState condition and update the position tracker.

```java 
    public followPath(ArrayList<Point> path){
        double stopState = 0;
        double startTime = 0;
        
        // Get the new extended path to use for calculating heading point
        // Extend the path 20 inches above the lookahead distance just to be safe
        ArrayList<Point> extendedPath = lookaheadMath.extendedPath(path , lastPointOfPath.lookaheadDistance + 20);
    
        while(stopState < 500){
            // Update the tracker whenever we deal with movements
            odometry.updateTracker();
            Point robotLocation = new Point(odometry.getX() , odometry.getY());
            
            Point lastPointOfPath = path.get(path.size() - 1);
            
            // 4 inches is the range in which to start stopState
            // The range of error to start stop State can be tuned to make it more accurate
            if(Math.sqrt(Math.pow(lastPointOfPath.x - robotLocation.x , 2) + Math.pow(lastPointOfPath.y - robotLocation.y , 2) < 4){
                stopState = System.currentTimeMillis() - startTime;
            }else{
                startTime = System.currentTimeMillis();
            }
        }
    }

```

### Current index in path

In this section, we will use the clipToPath() method to get the index of the end point of the line segment we are on. This will allow us to have control over things like faceTowardsAngle , movementSpeed , and lookaheadDistance for each individual line segment of the path.

```java 
    // Get the current index we are on the path
    Point currIndexInPath = clipToPath(path , robotLocation);
    
    // The end point of the line segment we are currently on in the path
    Point currPointInPath = path.get(currIndexInPath.pointIndex);
```


### Lookahead Point

In this section , we will calculate the lookahead point using the path passed into the followPath() method and the robot location point.

```java 
    Point lookahead = lookaheadMath.getLookaheadPoint(path , robotLocation , currIndexInPath);
```

### Heading Point

In this section, we will calculate the heading point.

```java 
    Point headingLookahead = lookaheadMath.getLookaheadPoint(extendedPath , robotLocation , currIndexInPath);
```

### Target Heading

In this section, we will calculate the target heading for the robot to face.

To fully understand the math, let's take a robot with position (x , y) and target (xt , yt):
<figure align="center">
    <img src="../../assets/images/robot-target-heading-example.png" class="rounded-lg" alt="quadratic formula">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Robot at position (x , y) with target (xt , yt)</figcaption>
</figure>

The target heading is the angle denoted by theta in this picture. We can calculate this angle by using the arc tangent trig function. We can do this by getting the length of legs a and b and pluging them into the arc tan function.
The following equations give us the lengths of the legs:
- leg a : (xt - x)
- leg b : (yt - y)

So, the equation to finding the target heading would be arc tangent (leg b , leg a). In the case of our robot, (x , y) would be the robot's location (robotLocation.x , robotLocation.y) and the (xt , yt) would be the target position (lookahead.x , lookahead.y):
The faceTowardsAngle has two use-cases:
- When the path is initialized and all the points are added, the faceTowardsAngle of each point determines whether the robot should face towards the target position when the robot is on that specific line segment of the path. For example, a faceTowardsAngle of 90 degrees would mean the robot should be facing towards the lookahead point when the robot is on that segment of the path. The next segment could have a faceTowards angle of 0 , per se, and the robot will face sideways while following the lookahead point on that line segment.
- The faceTowardsAngle is set equal to the new target heading based on the angle to the point.

```java 
    /* The relative point angle will use the faceTowardsAngle of the line segment 
    to find the angle offset to face the desired direction.Subtracting 90 degrees 
    since the forwards angle of a unit circle is 90 degrees while the forwards angle 
    of the robot is 0 degrees */
    double relativePointAngle = (Math.toRadians(currPointInPath.faceTowardsAngle) - Math.toRadians(90));  
    
    // Get the absolute angle to the lookahead point
    double angleToPoint = Math.atan2(lookahead.y - robotLocation , lookahead.x - odometry.getX());
    
    // Change the absolute angle , so we can add in our preference to it (if we should face towards the lookahead, sideways , etc)
    double targetHeading = angleToPoint + relativePointAngle;
    
    /* Angle wrap the target heading and convert it to degrees since the turnController 
    in the goToPosition() method works in degrees */
    
    targetHeading = angleWrap(targetHeading);
    targetHeading = Math.toDegrees(targetHeading);
    
    /* Set the faceTowardsAngle of the lookahead point to the target heading.
    This value will be called and used as the target position for the turnController in goToPosition() */
     
    headingLookahead.faceTowardsAngle = targetHeading;
    
```


### Go To Position

Now, we can call the goToPosition() method to actually go to the lookahead point.

```java 
    goToPosition(lookahead , headingLookahead);
```

---

<p style = "font-weight : 300; font-size : 24px;">
This is what the finished followPath() method should look like:
</p>

```java 
    public followPath(ArrayList<Point> path){
        double stopState = 0;
        double startTime = 0;
        
        // Get the new extended path to use for calculating heading point
        // Extend the path 20 inches above the lookahead distance just to be safe
        ArrayList<Point> extendedPath = lookaheadMath.extendedPath(path , lastPointOfPath.lookaheadDistance + 20);
    
        while(stopState < 500){
            odometry.updateTracker();
            Point robotLocation = new Point(odometry.getX() , odometry.getY());
        
            Point lastPointOfPath = path.get(path.size() - 1);
            
            
            // Get the current index we are on the path
            Point currIndexInPath = clipToPath(path , robotLocation);
    
            // The end point of the line segment we are currently on in the path
            Point currPointInPath = path.get(currPointInPath.pointIndex);
            
            Point lookahead = lookaheadMath.getLookaheadPoint(path , robotLocation , currIndexInPath);
            Point headingLookahead = lookaheadMath.getLookaheadPoint(extendedPath , robotLocation , currIndexInPath);
                  
            /* The relative point angle will use the faceTowardsAngle of the line segment 
            to find the angle offset to face the desired direction.Subtracting 90 degrees 
            since the forwards angle of a unit circle is 90 degrees while the forwards angle 
            of the robot is 0 degrees */
            double relativePointAngle = (Math.toRadians(currPointInPath.faceTowardsAngle) - Math.toRadians(90));  
    
            // Get the absolute angle to the lookahead point
            double angleToPoint = Math.atan2(lookahead.y - robotLocation , lookahead.x - odometry.getX());
    
            // Change the absolute angle , so we can add in our preference to it (if we should face towards the lookahead, sideways , etc)
            double targetHeading = angleToPoint + relativePointAngle;
    
            /* Angle wrap the target heading and convert it to degrees since the turnController 
            in the goToPosition() method works in degrees */
    
            targetHeading = angleWrap(targetHeading);
            targetHeading = Math.toDegrees(targetHeading);
    
            /* Set the faceTowardsAngle of the lookahead point to the target heading.
            This value will be called and used as the target position for the turnController in goToPosition() */
     
            headingLookahead.faceTowardsAngle = targetHeading;
            
            goToPosition(lookahead , headingLookahead);

            if(Math.sqrt(Math.pow(lastPointOfPath.x - robotLocation.x , 2) + Math.pow(lastPointOfPath.y - robotLocation.y , 2) < 4){
                stopState = System.currentTimeMillis() - startTime;
            }else{
                startTime = System.currentTimeMillis();
            }
        }
        
        // Stop the robot when it reaches the end
        stop();
    }

```