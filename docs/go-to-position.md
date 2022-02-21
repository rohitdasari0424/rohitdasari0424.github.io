
# Go To Position

<p style = "font-weight : 300; font-size : 24px;">
This page will go over the implementation of the goToPosition() method. This method should be placed in the Mecanum Drivetrain Class we made earlier.
</p>

---

The <b>goToPosition()</b> will be used to calculate the PID Outputs to get to the target position (lookahead point) and pass in these three movement outputs : movement_x , movement_y , and movement_turn to the field centric method.

## Code Implementation

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

---

<p style = "font-weight : 300; font-size : 24px;">
We now have a goToPosition() that calculated the movement_x , movement_y , and movement_turn that we can call after getting the lookahead point.
</p>