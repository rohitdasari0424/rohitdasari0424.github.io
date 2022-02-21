
# Odometry

<p style = "font-weight : 300; font-size : 24px;">
This section will go over the code implementation and explanation of Odometry.
</p>

[What is a Odometry?](https://rohitdasari0424.github.io/odometryTerm.html)

---

?>
Create the `Odometry.java` file under the `TeamCode` folder in your project directory.
Create the `ThreeWheelTracker.java` file under the `TeamCode` folder in your project directory.

```
.
└── TeamCode
    ├── Motor.java
    ├── MecanumDriveTrain.java
    ├── TestOpModes
        ├── EncoderReadingTest.java
    ├── Point.java
    ├── PIDController.java
    ├── Odometry.java
    ├── ThreeWheelTracker.java
```

---

## Global Variables

- `LEncoder` : The left encoder motor variable
- `REncoder` : The right encoder motor variable
- `HEncoder` : The horizontal encoder motor variable
- `prevLeftE` : The encoder position of the left encoder at the time of the last update
- `prevRightE` : The encoder position of the right encoder at the time of the last update
- `prevHorizontalE` : The encoder position of the horizontal encoder at the time of the last update
- `x` : Stores the x position of the robot
- `y` : Stores the y position of the robot
- `heading` : Stores the heading of the robot
- `trackWidth` : Stores the [track width](https://rohitdasari0424.github.io/odometryTerm.html#track-width) of the robot
- `auxWidth` : Stores the [aux width](https://rohitdasari0424.github.io/odometryTerm.html#track-width) of the robot
- `telemetry` : Telemetry instance used for debugging

```java 
public Motor LEncoder;
public Motor REncoder;
public Motor HEncoder;

private double prevLeftE = 0;
private double prevRightE = 0;
private double prevHorizontalE = 0;

private double x;
private double y;
private double heading;

private double trackWidth;
private double auxWidth;
    
private Telemetry telemetry;
``` 

## Constructor

The constructor will initialize the trackWidth , auxWidth , LEncoder, REncoder, HEncoder, and telemetry variables:

```java 
//Parameter LeftEncoderName : Name of the motor the Left Encoder is attached to
//Parameter RightEncoderName : Name of the motor the Right Encoder is attached to
//Parameter HorizontalEncoderName : Name of the motor the Horizontal Encoder is attached to
//Parameter trackWidth : Track width of the robot
//Parameter auxWidth : Aux Width of the robot
//Parameter hwMap : HardwareMap instance 
//Parameter telemetry : Telemetry instance
public Odometry(String LeftEncoderName , String RightEncoderName , String HorizontalEncoderName , double trackWidth, double auxWidth , HardwareMap hwmap , Telemetry telemetry){
    LEncoder = new Motor(LeftEncoderName , 1024 , 2.77, hwmap);
    REncoder = new Motor(RightEncoderName , 1024 , 2.77 , hwmap);
    HEncoder = new Motor(HorizontalEncoderName ,  1024 , 2.77, hwmap);
    this.trackWidth = trackWidth;
    this.auxWidth = auxWidth;
    this.telemetry = telemetry;
}
``` 

## updateTracker() method

This method will be called in a loop. It will update the robot location each run:

```java 
public void updateTracker(){
    
}
``` 

## Get Methods

- `getX()` : returns the robot's x position on the field
- `getY()` : returns the robot's y position on the field
- `getHeading()` : return the robot's heading in `RADIANS`
- `getHeadingDegrees()` : return the robot's heading in `DEGREES`

```java 
public double getX(){
    return this.x;
}

public double getY(){
    return this.y;
}
    
public double getHeading(){
    return this.heading;
}
    
public double getHeadingDegrees(){
    return Math.toDegrees(this.heading);
}
``` 

---

## What it should look like
This is what the odometry class should look like thus far :

```java 
public class Odometry {
    public Motor LEncoder;
    public Motor REncoder;
    public Motor HEncoder;

    private double prevLeftE = 0;
    private double prevRightE = 0;
    private double prevHorizontalE = 0;
    
    private double x;
    private double y;
    private double heading;
    
    private double trackWidth;
    private double auxWidth;
    private Telemetry telemetry;

    public odometry(String LeftEncoderName , String RightEncoderName , String HorizontalEncoderName , double trackWidth, double auxWidth , HardwareMap hwmap , Telemetry telemetry){
        LEncoder = new Motor(LeftEncoderName , 1024 , 2.77, hwmap);
        REncoder = new Motor(RightEncoderName , 1024 , 2.77 , hwmap);
        HEncoder = new Motor(HorizontalEncoderName ,  1024 , 2.77, hwmap);
        this.trackWidth = trackWidth;
        this.auxWidth = auxWidth;
        this.telemetry = telemetry;
    }


    public void updateTracker() {

    }

    public double getX(){
        return this.x;
    }

    public double getY(){
        return this.y;
    }

    public double getHeading(){
        return this.heading;
    }
    
    public double getHeadingDegrees(){
        return Math.toDegrees(this.heading);
    }
}
```

<p style = "font-weight : 300; font-size : 24px;">
In the following pages, we will be implementing the updateTracker() method.
</p>
