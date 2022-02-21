
# Final odometry class

<p style = "font-weight : 300; font-size : 24px;">
This page will go over what the odometry class should look like after implementing the updateTracker() method.
</p>

---

```java 
public class odometry {
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

        this.x += Math.cos(heading) * relativeX - Math.sin(heading) * relativeY;
        this.y += Math.sin(heading) * relativeX + Math.sin(heading) * relativeY;
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
---

<p style = "font-weight : 300; font-size : 24px;">
This marks the end of the odometry section. We now have an odometry class that will allow us to calculate the robot's heading , x position , and y position.
</p>