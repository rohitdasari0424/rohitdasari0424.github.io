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

[//]: # ()
[//]: # (<!-- tabs:start -->)

[//]: # (#### **Tank Drive Extra**)

[//]: # ()
[//]: # (The PIDController class requires one extra method for Tank Drivetrains. This method will be named the same as the `getOutput&#40;&#41;` method and contain similar code. It will, however, only have one paramter as opposed to the two parameters required for the other `getOutput&#40;&#41;` method. This would allow us to directly pass in the error instead of passing in current position and target position and calculating the error within the method. The significance of this will be seen later in the implementation of the `goToPosition&#40;&#41;` method for tank drive. Both `getOutput&#40;&#41;` methods are necessary for the implementation on Tank Drivetrains.)

[//]: # ()
[//]: # (```java )

[//]: # (    // Parameter error: The error between the current state of the system and the target state of the system)

[//]: # (    public double getOutput&#40;double error&#41;{)

[//]: # (    })

[//]: # (```)

[//]: # ()
[//]: # (<!-- tabs:end -->)


## Set Methods

```java 
    public void setConstants(double KP , double KI , double KD){
        this.KP = KP;
        this.KI = KI;
        this.KD = KD;
    }
```

---

<p style = "font-weight : 300; font-size : 24px;">
Here's what the `PIDController` class should look like thus far:
</p>


```java 
    private double KP;
    private double KI;
    private double KD;
    private double error;
    private double previousTime = 0;
    private double deltaTime = 0;
    private double previousError = 0;
    
    // Parameter KP : kp value of the PID Controller initialized
    // Parameter KI : ki value of the PID Controller initialized
    // Parameter KD : kd value of the PID Controller initialized
    public PIDController(double KP , double KI , double KD){
        this.KP = KP;
        this.KI = KI;
        this.KD = KD;
    } 
    
    // Parameter currPos : Current position of the state (For example, the heading of the robot currently)
    // Parameter targetPos : Target position of the robot (For example, the target heading you are trying to turn towards)
    public double getOutput(double currPos , double targetPos){
    }
    
    public void setConstants(double KP , double KI , double KD){
        this.KP = KP;
        this.KI = KI;
        this.KD = KD;
    }
```

[//]: # ()
[//]: # (<!-- tabs:start -->)

[//]: # ()
[//]: # (#### **Mecanum Drivetrain**)

[//]: # ()
[//]: # (```java )

[//]: # (    private double KP;)

[//]: # (    private double KI;)

[//]: # (    private double KD;)

[//]: # (    private double error;)

[//]: # (    private double previousTime = 0;)

[//]: # (    private double deltaTime = 0;)

[//]: # (    private double previousError = 0;)

[//]: # (    )
[//]: # (    // Parameter KP : kp value of the PID Controller initialized)

[//]: # (    // Parameter KI : ki value of the PID Controller initialized)

[//]: # (    // Parameter KD : kd value of the PID Controller initialized)

[//]: # (    public PIDController&#40;double KP , double KI , double KD&#41;{)

[//]: # (        this.KP = KP;)

[//]: # (        this.KI = KI;)

[//]: # (        this.KD = KD;)

[//]: # (    } )

[//]: # (    )
[//]: # (    // Parameter currPos : Current position of the state &#40;For example, the heading of the robot currently&#41;)

[//]: # (    // Parameter targetPos : Target position of the robot &#40;For example, the target heading you are trying to turn towards&#41;)

[//]: # (    public double getOutput&#40;double currPos , double targetPos&#41;{)

[//]: # (    })

[//]: # (    )
[//]: # (    public void setConstants&#40;double KP , double KI , double KD&#41;{)

[//]: # (        this.KP = KP;)

[//]: # (        this.KI = KI;)

[//]: # (        this.KD = KD;)

[//]: # (    })

[//]: # (```)

[//]: # ()
[//]: # (#### **Tank Drivetrain**)

[//]: # ()
[//]: # (```java )

[//]: # (    private double KP;)

[//]: # (    private double KI;)

[//]: # (    private double KD;)

[//]: # (    private double error;)

[//]: # (    private double previousTime = 0;)

[//]: # (    private double deltaTime = 0;)

[//]: # (    private double previousError = 0;)

[//]: # (    )
[//]: # (    // Parameter KP : kp value of the PID Controller initialized)

[//]: # (    // Parameter KI : ki value of the PID Controller initialized)

[//]: # (    // Parameter KD : kd value of the PID Controller initialized)

[//]: # (    public PIDController&#40;double KP , double KI , double KD&#41;{)

[//]: # (        this.KP = KP;)

[//]: # (        this.KI = KI;)

[//]: # (        this.KD = KD;)

[//]: # (    } )

[//]: # (    )
[//]: # (    // Parameter currPos : Current position of the state &#40;For example, the heading of the robot currently&#41;)

[//]: # (    // Parameter targetPos : Target position of the robot &#40;For example, the target heading you are trying to turn towards&#41;)

[//]: # (    public double getOutput&#40;double currPos , double targetPos&#41;{)

[//]: # (    })

[//]: # (    )
[//]: # (    // Parameter error: The error between the current state of the system and the target state of the system)

[//]: # (    public double getOutput&#40;double error&#41;{)

[//]: # (    })

[//]: # (    )
[//]: # (    public void setConstants&#40;double KP , double KI , double KD&#41;{)

[//]: # (        this.KP = KP;)

[//]: # (        this.KI = KI;)

[//]: # (        this.KD = KD;)

[//]: # (    })

[//]: # (```)

[//]: # ()
[//]: # (<!-- tabs:end -->)


<p style = "font-weight : 300; font-size : 24px;">
In the following pages, we will implement the getOutput() method by calculating the P , I , and D value.
</p>
