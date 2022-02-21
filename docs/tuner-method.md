
# Drive Controller tuning

<p style = "font-weight : 300; font-size : 24px;">
This section will go over the tuner() method that we will be using to tune the turn , drive , and strafe controller.
</p>

---

This method will be used for tuning the Turn , Drive , and Strafe Controllers.
Since we have already learned the concepts used in this method, we can go straight to the code implementation part.

## Code Implementation

```java 
    public void tuner(double x , double y , double targetHeading , double movementSpeed){
        double startTime = 0;
        double stopState = 0;

        while(stopState < 500){
            odometry.updateTracker();
            
            double movement_y = driveController.getOutput(odometry.getY() , y);
            double movement_x = strafeController.getOutput(odometry.getX() , x);
            double movement_turn = turnController.getOutput(odometry.getHeading(), targetHeading);

            fieldCentric(movement_x , movement_y , movement_turn , movementSpeed);
            
            telemetry.addData("x error" , strafeController.getError());
            telemetry.addData("y error" , driveController.getError());
            telemetry.addData("turn error" , turnController.getError());
            telemetry.update();

            /* You can adjust the range of error in which stopState starts: 
            If you need very accurate movement, then have one that is lower but if 
            you just want to get to some general area, then use a higher range */
            if(Math.abs(displacement) < 2){
                stopState = System.currentTimeMillis() - startTime;
            }else{
                startTime = System.currentTimeMillis();
            }

        }

        stop();
    }

```

--- 

<p style = "font-weight : 300; font-size : 24px;">
We now have a method that we can use to move in different directions : Forward for driveController tuning , Strafing for strafeController tuning, and Turning for turnController tuning
</p>
