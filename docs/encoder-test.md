# Encoder Test OpMode

<p style = "font-weight : 300; font-size : 24px;">
On this page we will code a basic OpMode that will output telemetry readings of the encoder positions to the RC phone.
By doing this, we will be able to decide which encoder has to be reversed and if the ticks to inches conversion constants are working properly.
</p>

---


?> Create the folder `TestOpModes` under the `TeamCode` folder in your project directory. This will contain all the 
OpModes we will use later on to test code and tune values.

?> Create the file `EncoderReadingTest.java` under the `TestOpModes` folder.

> ```text
.
└── TeamCode
    ├── Motor.java
    ├── MecanumDriveTrain.java
    ├── TestOpModes
        ├── EncoderReadingTest.java
> ```

?> This class will extend the OpMode class with the `@TeleOp` annotation. Running this class as a tele op will prevent the time limit which would give us as much time needed to observe the encoder readings.

---

# Global Variables
`driveTrain` : An instance of the mecanum drivetrain class

## Init Method

In this method, we will initialize the `driveTrain` variable and pass in the motor and encoder names.

```java 
    @Override
    public void init() {
        driveTrain = new MecanumDriveTrain(YOUR_TL_MOTOR_NAME , YOUR_BL_MOTOR_NAME , YOUR_TR_MOTOR_NAME
         , YOUR_BR_MOTOR_NAME , L_ENCODER_MOTOR_NAME, R_ENCODER_MOTOR_NAME , H_ENCODER_MOTOR_NAME , hardwareMap , telemetry)
    }
```
## Loop Method

In this method, we will call the outputEncoderReadings method we made earlier which will output the data to telemetry
as we manually maneuver the robot around.

```java 
    @Override
    public void loop() {
        driveTrain.outputEncoderReadings()
    }
```

## Deciding which motors to reverse

1. You will begin the encoder reading test. Clear a wide area of space for the robot to move on.
2. Run the `EncoderReadingTest` OpMode.
3. Make sure the RC phone does not throw any errors in regard to hardware initialization.
4. Slowly drag the robot forward and observe the left and right encoder readings in the telemetry
5. Both encoder readings should increase as you move the robot forward. Check if either one is decreasing and take note of it.
6. Now, slowly drag the robot to the right
7. Observe the horizontal encoder reading and take note of if it is increasing or decreasing.

If any of the motor encoder readings were decreasing as you moved them in the specified directions, reverse these encoders in the Mecanum Drivetrain constructor as shown below :

```java 
    // In the case of my robot, the encoder cpr is 1024 and the wheelDiameter is 2.77 inches so I will initialize the LEncoder, REncoder , and HEncoder accordingly.
    public MecanumDriveTrain(String tlName, String blName, String trName, String brName , String LEncoderName , String REncoderName , String HEncoderName , HardwareMap hardwareMap , Telemetry telemetry) {
        this.tl = new Motor(tlName , hardwareMap);
        this.bl = new Motor(blName ,  hardwareMap);
        this.tr = new Motor(trName , hardwareMap);
        this.br = new Motor(brName , hardwareMap);
        
        this.LEncoder = new Motor(LEncoderName , 1024 , 2.77 , hardwareMap);
        this.REncoder = new Motor(REncoderName , 1024 , 2.77 , hardwareMap);
        this.HEncoder = new Motor(HEncoderName , 1024 , 2.77 , hardwareMap);
        
        this.LEncoder.reset();
        this.REncoder.reset();
        this.HEncoder.reset();
        
        // On my robot, only the right encoder reading was decreasing when I performed the test so I will reverse it
        this.REncoder.reverse();
        
        this.tl.setBreakMode();
        this.bl.setBreakMode();
        this.tr.setBreakMode();
        this.br.setBreakMode();
        
        this.telemetry = telemetry;
    }
```

## Testing Ticks to Inches conversion

1. You will begin the Ticks to Inches test. Clear a straight line for your bot to travel in. (4 - 5 field tiles should suffice)
2. Measure the distance of the stretch and note it down
3. Set the robot facing forward at the beginning of the stretch
4. Run the `EncoderReadingTest` OpMode
5. Make sure the RC phone does not throw any errors in regard to hardware initialization.
6. Slowly drag the robot forward along this stretch while making sure to keep the robot facing forward as straight as possible.
7. Once you reach the end of your stretch, stop. Compare the current position of the right and left encoder in inches to the length of the stretch that the robot traveled.
8. Analyze the test :
- If the encoder readings are off, it is likely that the `cpr` and/or `wheelDiameter` values are incorrect. Change these values by looking up the hardware spec and perform this test again.
- If the encoder readings are close to the length of the stretch, your values are correct and the ticks to inches conversion is working properly.

## Trouble Shooting CPR and Wheel Diameter

1. Make sure you did not confuse `PPR` with `CPR`
   - PPR refers to pulses per revolution
   - PPR can be converted to CPR by multiplying it by 4.0
2. Make sure the `Wheel Diameter` is in the correct unit, inches
   - If you inputted the diameter in mm instead of inches, you can convert them using the [mm to inches calculator](https://www.google.com/search?q=mm+to+inches&rlz=1C1CHZN_enUS979US979&oq=mm+to+inches&aqs=chrome..69i57j6j0i512l8.1331j0j7&sourceid=chrome&ie=UTF-8)
3. Make sure you are measuring the diameter of the dead wheel , not the drive train wheels.
