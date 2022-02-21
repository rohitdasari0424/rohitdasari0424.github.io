
# Final PID Controller class

<p style = "font-weight : 300; font-size : 24px;">
This page will go over what the PIDController class should look like after implementing the P-Value , I-Value , and D-Value.
</p>

---

## Final getOutput() method

Now that we have calculated the P-Value , I-Value , and D-value, we can calculate the final output by adding these terms together. The getOutput() method will return this value:

```java 
    public double getOutput(double currPos , double targetPos){
        this.error = targetPos - currPos;
        this.previousError = error;
        double P = KP * error; // Proportional term : KP constant * the error of the system
        this.deltaTime = System.currentTimeMillis() - previousTime;
        this.previousTime = System.currentTimeMillis();
        this.i += currPos > targetPos * 0.8 ? deltaTime * error : 0;
        double I = KI * i;
        this.d = (error - previousError) / deltaTime
        double D = KD * d

        return P + I + D;
    }
``` 

## Final PIDController class

<p style = "font-weight : 300; font-size : 24px;">
This is how your final PIDController class should look like:
</p>

```java 

public class PIDController{
    private double KP;
    private double KI;
    private double KD;
    private double previousTime = 0;
    private double error;
    private double i = 0;
    private double d = 0;
    private double deltaTime = 0;
    private double previousError = 0;

    public PIDController(double KP , double KI , double KD){
        this.KP = KP;
        this.KI = KI;
        this.KD = KD;
    }

    public double getOutput(double currPos , double targetPos){
        this.error = targetPos - currPos;
        this.previousError = error;
        double P = KP * error; // Proportional term : KP constant * the error of the system
        this.deltaTime = System.currentTimeMillis() - previousTime;
        this.previousTime = System.currentTimeMillis();
        this.i += currPos > targetPos * 0.8 ? deltaTime * error : 0;
        double I = KI * i;
        this.d = (error - previousError) / deltaTime
        double D = KD * d

        return P + I + D;
    }
    
    public double getError(){
        return this.error;
    }    

    public void setConstants(double KP , double KI , double KD){
        this.KP = KP;
        this.KI = KI;
        this.KD = KD;
    }   
}
``` 
---



This marks the end of the PID Control System section. From this section, we have learned how to implement the different values and how they work. We now have a method that can get the robot from one state to another in an accurate manner.

