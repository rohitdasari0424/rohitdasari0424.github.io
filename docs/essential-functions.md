# Essential Functions

<p style = "font-weight : 300; font-size : 24px;">
Here are some of the main math functions you will need to understand
</p>

---

## Math.toRadians(angle)

This is one of the most important functions that will be used in this algorithm. The Math.toRadians(angle) function converts an angle given in the `DEGREES` unit to `RADIANS`.
Radians are used over degrees when dealing with angles , because trig functions such as Math.sin() , Math.cos() , Math.atan2() require angles to be in `RADIANS`.

```java 
   //Converts 45 Degrees to Radians
   double angleInDegrees = 45;
   double angleInRadians = Math.toRadians(angleInDegrees);
   System.out.println("Angle in radians :" + angleInRadians);
```

```java 
   Output:
   Angle in radians :0.7853981633974483
```

## Distance Calculation

Example of using the distance formula to calculate distance between the current position and the target position :
```java 
    //distance formula = √((m2 - m1)^2 + (n2 - n1)^2);
    
    // Initializing the starting point and end point
    Point currentPosition = new Point(0 , 0); // X Coordinate : 0 , Y Coordinate : 0
    Point targetPoint = new Point(25 , 15); // X Coordinate : 25 , Y Coordinate : 15
    
    double distanceBetweenPoints = Math.sqrt(Math.pow(targetPoint.x - currentPosition.x , 2) + Math.pow(targetPoint.y - currentPosition.y , 2));
    System.out.println("Distance between points: " + distanceBetweenPoints); 
```

```java 
   Output:
   Distance between points: 29.154759474226502
```

## Encoder Ticks To Inches

This method converts the encoder ticks into inches. The method works by having the encoder ticks being divided by the `TICKS_PER_INCH` constant.

```java 
    double WHEEL_DIAMETER; //Wheel diameter of wheel
    double CPR; // Counts per revolution of the encoder
    double TICKS_PER_INCH = CPR / (WHEEL_DIAMETER * Math.PI); // Encoder ticks per inch moved
    
    public double getCurrPosInches(){
        return (motor.getCurrentPosition() / TICKS_PER_INCH);
    }
```

## Math.sqrt(number)

Returns the square root of the inputted number

## Math.pow(number , n)

Returns the number inputted to the nth power

## Math.sin(angle)

Returns the sin of an angle. The input angle must be in `RADIANS`.

## Math.cos(angle)

Returns the sin of an angle. The input angle must be in `RADIANS`.

## Math.atan2(angle)

Returns the tangent of an angle. The input angle must be in `RADIANS`.

