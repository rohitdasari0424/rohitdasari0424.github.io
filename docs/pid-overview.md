# PID Controller

<p style = "font-weight : 300; font-size : 24px;">
This section will go over the code implementation of the PID Controller.
This page will go over the variables to declare and the methods to make for the PID Controller class.
</p>

[What is a PID Controller?](https://rohitdasari0424.github.io/pidTerm.html)

---

?>
Create the `PIDController.java` file under the `TeamCode` folder in your project directory.
> ```text
.
└── TeamCode
    ├── Motor.java
    ├── MecanumDriveTrain.java
    ├── TestOpModes
        ├── EncoderReadingTest.java
    ├── Point.java
    ├── PIDController.java
> ```

---

## Variables
- `KP` : Proportional Constant for the PID Controller
- `KI` : Integral Constant for the PID Controller
- `KD` : Derivative Constant for the PID Controller
- `previousTime` : Stores the time the pid loop last ran in milliseconds
- `error` : Stores the difference between the target state and the current state
- `deltaTime` : Amount of time passed since the last loop run
- `previousError` : Stores the error from the past loop run

```java 
    private double KP;
    private double KI;
    private double KD;
    private double error;
    private double previousTime = 0;
    private double deltaTime = 0;
    private double previousError = 0;
```

## Constructor

```java 
    // Parameter KP : kp value of the PID Controller initialized
    // Parameter KI : ki value of the PID Controller initialized
    // Parameter KD : kd value of the PID Controller initialized
    public PIDController(double KP , double KI , double KD){
        this.KP = KP;
        this.KI = KI;
        this.KD = KD;
    }
```

## Output method

This method will be called in a loop and will return the PID power. This method will be implemented in the following pages of the section.
```java 
    // Parameter currPos : Current position of the state (For example, the heading of the robot currently)
    // Parameter targetPos : Target position of the robot (For example, the target heading you are trying to turn towards)
    public double getOutput(double currPos , double targetPos){
    }
```

---

## Set Methods

```java 
    public void setConstants(double KP , double KI , double KD){
        this.KP = KP;
        this.KI = KI;
        this.KD = KD;
    }
```

<p style = "font-weight : 300; font-size : 24px;">
In the following pages, we will implement the getOutput() method by calculating the P , I , and D value.
</p>