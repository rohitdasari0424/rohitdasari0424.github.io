# Lookahead Point Test

In this section, we will be the testing the GetLookahead() method.

---

First, we will need to set up a simple OpMode for the lookahead point test. This OpMode will output the `x` , `y` , and `heading` of the robot as you move it manually around the field. It will also output the `(x , y , movementSpeed , faceTowardsAngle , lookaheadDistance)` of the lookahead point.

>> [!TIP] For this test, we will be using the telemetry output to DC phone, not FTCDashboard.

>> [!WARNING] Perform this test only after successfully testing odometry first.

## OpMode

```java
    @TeleOp
    public class LookaheadTest extends OpMode{
        MecanumDriveTrain driveTrain;
        ArrayList<Point> path;
    
        @Override
        public void init(){
            driveTrain = new MecanumDriveTrain(hardwareMap , telemetry);
            path = new ArrayList<>();
            
            // Add points to the path (x , y , movementSpeed , faceTowardsAngle , lookaheadDistance)
            path.add(new Point(0 , 0 , 0.75 , 90 , 5.0 ));
            path.add(new Point(0 , 25 , 0.5 , 90 , 7.5 ));
            path.add(new Point(25 , 25 , 0.65 , 90 , 6.5 ));
        }
    
        @Override
        public void loop(){
            driveTrain.odometry.updateTracker();
            
            // Store the robot's x and y location as a Point
            Point robotLocation = new Point(driveTrain.odometry.getX() , driveTrain.odometry.getY());
            
            // Get the current index of the path the robot is currently on , pass in (Path , Robot Location)
            Point currIndexInPath = LookaheadMath.clipToPath(path , robotLocation);
            
            // Get the lookahead point , pass in (Path , Robot Location , Current index in the path)
            Point lookaheadPoint = LookaheadMath.getLookaheadPoint(path , robotLocation , currIndexInPath);
                    
            // Output everything to telemetry
            
            telemetry.addData("x position : " , driveTrain.odometry.getX());
            telemetry.addData("y position : " , driveTrain.odometry.getY());
            telemetry.addData("heading : " , driveTrain.odometry.getHeadingDegrees());
            telemetry.addData("Lookahead x : " , lookaheadPoint.x);
            telemetry.addData("Lookahead y : " , lookaheadPoint.y);
            telemetry.addData("Lookahead movementSpeed : " , lookaheadPoint.movementSpeed);
            telemetry.addData("Lookahead faceTowardsAngle : " , lookaheadPoint.faceTowardsAngle);
            telemetry.addData("Lookahead lookaheadDistance : " , lookaheadPoint.lookaheadDistance);
            telemetry.update();
        }
        
    }

```

## Testing

1. We will now begin the testing process. Begin by clearing a wide area of space for the robot to move in.
2. Place the robot facing forward and initialize the `LookaheadTest` OpMode using the DC Phone.
3. Run the OpMode
4. Slowly drag the robot forward and ensure that odometry is working properly. 
    - If it isn't, then navigate to the [odometry test page](https://rohitdasari0424.github.io/#/odometry-test).
5. Observe the telemetry output of lookahead x and lookahead y and make sure they make sense.
    - For example, if `robotLocation` is (0 , 0) in this path with a `lookahead distance` of 6.5 , a reasonable
      `lookahead point` would be (0 , 6.5).
    - If they don't , revisit the [line-circle intersection page](https://rohitdasari0424.github.io/#/line-circle-intersection) and the [Get Lookahead Page](https://rohitdasari0424.github.io/#/get-lookahead) and ensure your code matches up with the respective code implementation section.
6. Observe the telemetry output of movementSpeed , faceTowardsAngle , and lookaheadDistance and ensure that they match up with the end point of the current segment we are on.
    - In this test, when the robot is on the first segment of the path `(0 , 0)` to `(0 , 25)`, the `movementSpeed` should be 0.5 , `faceTowardsAngle` should be 90, and `lookaheadDistance` should be 6.5.
    - If they don't , revisit the [clip to line page](https://rohitdasari0424.github.io/#/clip-to-line) and the [clip to path page](https://rohitdasari0424.github.io/#/clip-to-path) and ensure your code matches up with the respective code implementation section.
7. Drag the robot along the entirety of the path until it reaches the end.
    - Ensure that the `movementSpeed` , `faceTowardsAngle` , and `lookaheadDistance` values are working properly (set equal to the values of the end point of the current line segment we are on) throughout the entirety of the path.
8. If all the tests worked , then you have successfully implemented the lookahead algorithm.

---

<p style = "font-weight : 300; font-size : 24px;">
We now have a fully implemented and tested lookahead point algorithm.
</p>

