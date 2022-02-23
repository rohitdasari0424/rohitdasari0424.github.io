
# Go To Position

<p style = "font-weight : 300; font-size : 24px;">
This page will go over the implementation of the goToPosition() method. This method should be placed in the Mecanum Drivetrain Class we made earlier.
</p>

---

The <b>goToPosition()</b> will be used to calculate the PID Outputs to get to the target position (lookahead point) and pass in the movement variables to the robot or field centric methods to calculate the individual motor powers.

## Code Implementation

<!-- tabs:start -->

#### **Mecanum Drivetrain**

Since the power-setting is being handled in the field centric, the goToPosition() method is rather simple. We will calculate three PID outputs:
- `PID Output of x error`
- `PID Output of y error`
- `PID Output of turn error`


```java 
    // Parameter targetPoint : The target point (x , y , targetHeading , movementSpeed , lookaheadDistance)
    public void goToPosition(Point targetPoint , Point headingPoint){
        // Whenever we deal with movements, we should always update the position tracker first
        odometry.updateTracker();
        
        // The strafe controller is just an instance of the PID Controller class for strafing
        // Pass in current position as the robot x and target position as the targetPoint.x
        double movement_x = strafeController.getOutput(odometry.getX() , targetPoint.x);
        
        // The forwardController is just an instance of the PID Controller class for moving in the y direction
        // Pass in current position as the robot y and target position as the targetPoint.y
        double movement_y = forwardController.getOutput(odometry.getY() , targetPoint.y);
        
        // The turnController is just an instance of the PID Controller class for moving in the y direction
        // Pass in current position as the robot heading and target position as the headingPoint.faceTowardsAngle
        // Since faceTowardsAngle is in the degrees unit, we have to convert heading to degrees
        double movement_turn = turnController.getOutput(Math.toDegrees(odometry.getHeading()) , headingPoint.faceTowardsAngle);
        
        /* Now we can just input these movement 
        variables into the field centric method which 
        will get the robot to the target position */
        
        fieldCentric(movement_x , movement_y , movement_turn , movementSpeed);
    }
```

#### **Tank Drivetrain**

Since the power-setting is being handled in the robot-centric method, the goToPosition() method is rather simple. We will calculate twocdcd cd PID outputs:
- `PID Output of displacement`
- `PID Output of angle error`

```java 
    // Parameter targetPoint : The target point (x , y , targetHeading , movementSpeed , lookaheadDistance)
    public void goToPosition(Point targetPoint){
        // Whenever we deal with movements, we should always update the position tracker first
        odometry.updateTracker();
        
        // The getOutput takes the target position and current position as inputs
        // In the case of the error of the system being displacement (distance between the target point and current robot position) , the distance formula can be used to calculate the error
        // The distance formula : d = √( (x2 - x1)^2 + (y2 - y1)^2 ) 
        // Since the getOutput() method already subtracts the currentPosition
        // from the targetPosition to calculate error, we can use the (odometry.getX(), odometry.getY()) 
        // as (x2, y2) and (0, 0) as (x1, y1) to calculate the current state of the system.
        
        double currPos = Math.sqrt(Math.pow(odometry.getX(), 2) + Math.pow(odometry.getY(), 2));
        
        // Calculate the targetPos using the same principles
        double targetPos = Math.sqrt(Math.pow(targetPoint.x, 2) - Math.pow(targetPoint.y,2));
        
        // The driveController controller is just an instance of the PID Controller class for displacement
        // Pass in current position as currPos and target position as targetPos
        double movement_drive = driveController.getOutput(currPos , targetPos);
        
        // The turnController is just an instance of the PID Controller class for moving in the y direction
        // Pass in current position as the robot heading and target position as the headingPoint.faceTowardsAngle
        // Since faceTowardsAngle is in the degrees unit, we have to convert heading to degrees
        double movement_turn = turnController.getOutput(Math.toDegrees(odometry.getHeading()) , targetPoint.faceTowardsAngle);
        
        /* Now we can just input these movement 
        variables into the field centric method which 
        will get the robot to the target position */
        
        robotCentric(movement_drive , movement_turn , movementSpeed);
    }
```


<!-- tabs:end -->



<p style = "font-weight : 300; font-size : 24px;">
We now have a goToPosition() that calculated the movement_x , movement_y , and movement_turn that we can call after getting the lookahead point.
</p>