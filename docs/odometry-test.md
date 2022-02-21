# Odometry Test

In this section, we will be testing the odometry position tracking system to ensure that all the calculations are working as intended.

---

First, we will need to set up a simple OpMode for the odometry system test. This OpMode will output the `x` , `y` , and `heading` of the robot as you move it manually around the field. By observing the telemetry as we move it in specified directions , we can determine the issues and fix them.

>> [!TIP] For this test, we will be using the telemetry output to DC phone, not FTCDashboard

## OpMode

```java
    @TeleOp
    public class OdometryTest extends OpMode{
        MecanumDriveTrain driveTrain;
    
        @Override
        public void init(){
            driveTrain = new MecanumDriveTrain(hardwareMap , telemetry);
        }
    
        @Override
        public void loop(){
            telemetry.addData("x position : " , driveTrain.odometry.getX());
            telemetry.addData("y position : " , driveTrain.odometry.getY());
            telemetry.addData("heading : " , driveTrain.odometry.getHeadingDegrees());
            telemetry.update();
        }
        
    }

```

## Testing

1. We can now begin the testing process. Clear an area for the robot to move in.
2. Initialize the `OdometryTest` OpMode and ensure that no initialization errors are thrown.
3. Run the OpMode using the `DriverController` phone.
4. Drag the robot forward and observe the `y position` in the telemetry.
    
   - Ensure the `y position` is increasing as you move forward. [Trouble shoot](https://rohitdasari0424.github.io/#/odometry-test?id=y-position-doesn39t-increase-moving-forward).
5. Slowly rotate the robot `45 degrees` clock-wise.

   - Ensure the `heading` is decreasing as you're turning it and reads it properly (a 45-degree turn clock-wise should read -45). [Trouble shoot](https://rohitdasari0424.github.io/#/odometry-test?id=heading-increases-as-your-rotate-robot-clock-wise).
6. Drag the robot forward and check that both the `y position` and `x position` are increasing. [Trouble shoot](https://rohitdasari0424.github.io/#/odometry-test?id=y-position-or-x-position-decrease-when-moving-forward-at-45-degrees).
7. Slowly rotate the robot `90 degrees counter-clockwise` to `45 degrees`.
8. Drag the robot forward and ensure that `y position` is increasing while `x position` decreases.
9. Drag the robot to the right such that it strafes and ensure that both the `x position` and `y position` are increasing. [Trouble shoot](https://rohitdasari0424.github.io/#/odometry-test?id=y-position-or-x-position-decreases-when-strafing-right-at-45-degrees).
10. Observe telemetry output as you rotate the robot towards `0 degrees` and ensure that `x position` doesn't significantly change. [Trouble shoot](https://rohitdasari0424.github.io/#/odometry-test?id=x-position-changes-significantly-when-rotating).
11. If all the tests worked as intended, then you have successfully implemented odometry position tracking on your robot. `If some tests did not go as intended, refer to the` [trouble shooting section](https://rohitdasari0424.github.io/#/odometry-test?id=trouble-shooting).


## Trouble Shooting

### Y Position doesn't increase (moving forward)

   1. One of the left or right encoder may need to be reversed. Perform the [encoders test](https://rohitdasari0424.github.io/#/encoder-test).
   2. The left or right encoder may not have been initialized properly
        - Check that neither `cpr` or `wheelDiameter` are set to 0.
        - Ensure that the encoders are mapped to the proper name.
   3. Unplug and replug the left and right encoders from the encoder ports.
   4. Left or right deadwheels may not be spring loaded properly
        - Lift the robot and manually roll the dead wheels and check if the y position increases.

>> [!ATTENTION] 
> All the following troubleshooting changes refer to calculations in the `updateTracker()` method in the odometry java class.

### Heading increases as your rotate robot clock-wise
   1. Multiply heading by `-1.0`:
      ```java 
      this.heading = -1.0 * ( (leftPosition - rightPosition) / trackWidth); 
      ```

### Y position or X position decrease when moving forward at -45 degrees

- If both `Y position` and `X position` decrease, multiply relativeY by `-1.0`
- If only `X position` decreases, multiply relativeY by `-1.0` in the x integration equation
- If only `Y position` decreases, multiply relativeY by `-1.0` in the y integration equation

### Y position or X position decreases when strafing right at 45 degrees

- If both `x position` and `y position` decrease , multiply relativeX by `-1.0` 
- If only `x position` decreases, multiply relativeX by `-1.0` in the x integration equation
- If only `y position` decreases, multiply relativeX by `-1.0` in the y integration equation

### X position changes significantly when rotating

- Retune the `Aux Width`

---

<p style = "font-weight : 300; font-size : 24px;">
We now have a fully implemented and tested odometry position tracking system.
</p>

