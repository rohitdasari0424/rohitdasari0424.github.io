# Track-width Tuning

<p style = "font-weight : 300; font-size : 24px;">
This section will go over the tuning process of three-wheel odometry track width.
</p>

---

Track-width is used for heading calculations in odometry and is the distance between the two parallel dead wheels of the three-wheel odometry system.

## OpMode

First, we will need to set up a simple OpMode that outputs the heading of the robot to telemetry.
We will use the FTCDashboard to tune it as this will allow us to change the trackWidth directly from the configuration window.

### Variables
`driveTrain` : Instance of the MecanumDriveTrain class.


```java
    @TeleOp
    public class TrackWidthTuner extends OpMode {
        private MecanumDriveTrain driveTrain;
        private FTCDashboard dashboard;
        static double trackWidth = PHYSICALLY_TUNED_VALUE;

        @Override
        public void init() {
            driveTrain = new MecanumDriveTrain();
            dashboard = FTCDashboard.getInstance();
            telemtry = new MultipleTelemetry(telemetry , dashboard.getTelemetry());
        }

        @Override
        public void loop() {
            driveTrain.odometry.updateTracker();
            telemetry.addData("Robot Heading : " , driveTrain.odometry.getHeadingDegrees());
            telemetry.update();
        }
    }
```


## Tuning Process

1. Turn the robot to the back and use a tape measure to physically measure the distance between the two parallel dead wheels.
2. Stick this value into the `trackWidth` variable in the class.
3. We will now begin the tuning process. Clear an area for the robot to move and turn in.
4. Place the robot against a wall facing away from it.
5. Initialize the `TrackWidthTuner` OpMode on the FTCDashboard and ensure that no errors are thrown.
6. Run the OpMode
7. Slowly turn the robot manually 90 degrees counter-clockwise such that the side of the robot touches the wall and observe the telemetry readings.
8. Analyze telemetry:

   - If the robot heading is <b>less</b> than 90 degrees, then <b>increase</b> trackWidth
   - If the robot heading is <b>greater</b> than 90 degrees, then <b>decrease</b> trackWidth

9. If the robot heading in telemetry is very close to 90 degrees (89.5 - 90.5 degrees), you have successfully tuned trackWidth.

    - Stick the value into `TUNABLE_CONSTANTS` interface for `trackWidth`.