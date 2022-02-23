
# Delta Time of the PID Controller

<p style = "font-weight : 300; font-size : 24px;">
This page will go over the code implementation of Delta Time in the PID Controller.
</p>

---

`Delta Time` : The time passed since the last loop run

## What is Delta Time used for?

Delta time is the time passed since the last loop run in milliseconds. It is mainly used in the calculation of the I-Value and the D-Value. You will see how it is used for these calculations in the follwoing pages.

## Code implementation

The following is the code implementation of deltaTime :

```java 
    // System.currentTimeMillis() returns the current time in milliseconds
    // previousTime is the time when the loop last run in milliseconds
    this.deltaTime = System.currentTimeMillis() - previousTime;
    this.previousTime = System.currentTimeMillis(); // Store the current time so it can be used the next loop run
```

---

<p style = "font-weight : 300; font-size : 24px;">
This is what the getOutput() methods should look like thus far:
</p>

```java 
    public double getOutput(double currPos , double targetPos){
        this.error = targetPos - currPos;
        double P = KP * error; // Proportional term : KP constant * the error of the system
        this.deltaTime = System.currentTimeMillis() - previousTime;
        this.previousTime = System.currentTimeMillis();
    }
```

[//]: # ()
[//]: # (<!-- tabs:start -->)

[//]: # ()
[//]: # (#### **getOutput&#40;double currPos, double targetPos&#41;**)

[//]: # (```java )

[//]: # (    public double getOutput&#40;double currPos , double targetPos&#41;{)

[//]: # (        this.error = targetPos - currPos;)

[//]: # (        double P = KP * error; // Proportional term : KP constant * the error of the system)

[//]: # (        this.deltaTime = System.currentTimeMillis&#40;&#41; - previousTime;)

[//]: # (        this.previousTime = System.currentTimeMillis&#40;&#41;;)

[//]: # (    })

[//]: # (```)

[//]: # ()
[//]: # (#### **getOutput&#40;double error&#41;**)

[//]: # (```java )

[//]: # (    public double getOutput&#40;double error&#41;{)

[//]: # (        double P = KP * error; // Proportional term : KP constant * the error of the system)

[//]: # (        this.deltaTime = System.currentTimeMillis&#40;&#41; - previousTime;)

[//]: # (        this.previousTime = System.currentTimeMillis&#40;&#41;;)

[//]: # (    })

[//]: # (```)

[//]: # ()
[//]: # (<!-- tabs:end -->)

