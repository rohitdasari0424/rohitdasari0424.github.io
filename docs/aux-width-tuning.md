# Aux Width Tuning

<p style = "font-weight : 300; font-size : 24px;">
This section will go over the tuning process of three-wheel odometry aux width.
</p>

Aux width is used for calculating the horizontal change offset when turning. It is the distance between the horizontal dead wheel and the center of rotation.

---

>[!TIP]
> Aux width tuning isn't necessary if the dead wheel is placed exactly at the center of rotation. In that situation, you can plug in zero for Aux Width.

## OpMode

```java
    @TeleOp
    public class AuxWidthTuner extends OpMode {
        private MecanumDriveTrain driveTrain;
        private FTCDashboard dashboard;
        static double auxWidth = PHYSICALLY_TUNED_VALUE;

        @Override
        public void init() {
            driveTrain = new MecanumDriveTrain();
            dashboard = FTCDashboard.getInstance();
            telemtry = new MultipleTelemetry(telemetry , dashboard.getTelemetry());
        }

        @Override
        public void loop() {
            driveTrain.odometry.updateTracker();
        }
    }
```

In the updateTracker() method in the odometry class, use the telemetry instance to output the `relativeX` :

```java
   public void updateTracker(){
        double leftPosition = LEncoder.getCurrPosInches();
        double rightPosition = REncoder.getCurrPosInches();
        double horizontalPosition = HEncoder.getCurrPosInches();

        double deltaLeft = leftPosition - prevLeftE;
        this.prevLeftE = leftPosition; // Stores the current leftPosition to be used during the next update

        double deltaRight = rightPosition - prevRightE;
        this.prevRightE = leftPosition; // Stores the current rightPosition to be used during the next update
        double deltaHorizontal = horizontalPosition - prevHorizontalE;
        this.prevHorizontalE = leftPosition; // Stores the current horizontalPosition to be used during the next update

        double deltaHeading = (deltaLeft - deltaRight) / trackWidth;

        this.heading = (leftPosition - rightPosition) / trackWidth;

        double horizontalOffset = auxWidth * deltaHeading;
        double relativeX = horizontalChange - horizontalOffset;
        double relativeY = (deltaLeft + deltaRight) / 2.0;
        
        `this.telemetry.addData("horizontal change : " + relativeX);`

        this.x += Math.cos(heading) * relativeX - Math.sin(heading) * relativeY;
        this.y += Math.sin(heading) * relativeX + Math.sin(heading) * relativeY;
    }

```


## Tuning Process

1. Turn the robot to the back and use a tape measure to physically measure the distance bettween the center of rotation and the horizontal dead wheel.
2. Stick this value into the `auxWidth` variable in the class.
3. We will now begin the tuning process. Clear an area for the robot to move and turn in.
4. Place the robot against a wall facing away from it.
5. Initialize the `AuxWidthTuner` OpMode on the FTCDashboard and ensure that no errors are thrown.
6. Run the OpMode
7. Slowly turn the robot manually 90 degrees counter-clockwise such that the side of the robot touches the wall and observe the telemetry readings.
8. Analyze telemetry:

   - If the horizontal change was negative as you moved the robot, then decrease auxWidth
   - If the horizontal change was positive as you moved the robot, then increase auxWidth
   
9. If the horizontal change was very close to 0 (0.5 error from 0), then you have successfully tuned auxWidth.

    - Stick the value into `TUNABLE_CONSTANTS` interface for `auxWidth`.
