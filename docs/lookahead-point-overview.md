# Lookahead Point

<p style = "font-weight : 300; font-size : 24px;">
This section will go over the code implementation and the math behind the calculation of the lookahead point.
</p>

[What is a Lookahead Point?](https://rohitdasari0424.github.io/lookaheadPointTerm.html)

---

The lookahead point is a core element of our path following algorithm. As the robot moves along the path, the algorithm will calculate the lookahead point and then set this lookahead point as its target. The lookahead point is constantly changing and calculated using the [lookahead distance constant.](https://rohitdasari0424.github.io/lookaheadPointTerm.html#lookahead-distance).

---

?>
Create the `LookaheadMath.java` file under the `TeamCode` folder in your project directory.
> ```text
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
    ├── LookaheadMath.java
>```

---

## Methods we will implement
We will make all the following methods static, so that we wouldn't have to create an object of the `LookaheadMath` class when we want to use these methods.

- `lineCircleIntersection()` : Get the intersection points between the robot and the line segment we are currently on
- `clipToLine()` : Get the intersection point between a perpendicular line going through the robot's center and each line segment of the path
- `clipToPath()` : Get the index of the end point of the line segment the robot is currently on in the path
- `getLookahead()` : Gets the lookahead point using the lineCircleIntersection() method and choosing between the intersections
- `extendPath()` : Extends the path a certain distance


---

<p style = "font-weight : 300; font-size : 24px;">
We will add the necessary methods to this class in the following pages.
</p>
