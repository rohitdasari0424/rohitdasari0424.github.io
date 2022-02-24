
# Line Circle Intersection

<p style = "font-weight : 300; font-size : 24px;">
This page will go over the code implementation and math behind the line circle intersection.
</p>

---

<b>The Line circle intersection</b> algorithm finds the points at which a circle equation given in the form: `(x - h)^2 + (y - k)^2 = r^2` intersects with a line equation given in the form: `y = mx + b`.

<figure align="center">
    <img src="../Images/line-equation.png" class="rounded-lg" alt="Line equation">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Visual of the line equation. The equation of a line is y = mx + b where m is equal to the slope and b is equal to the y intercept of the line.</figcaption>
</figure>

---

<figure align="center">
    <img src="../Images/circle-equation.jpg" class="rounded-lg" alt="circle equation">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Visual of the circle equation. The equation of a circle is (x - h)^2 + (y - k) ^ 2 = r^2 where (h , k) is the center of the circle and r is the radius of the circle.</figcaption>
</figure>

---

<figure align="center">
    <img src="../Images/line-circle-visual.jpg" class="rounded-lg" alt="circle intersects line">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Example of a circle intersecting a line.</figcaption>
</figure>

---


## What will we use line-circle intersection for?

Line-circle intersection will play a key role in our path following algorithm. It will calculate the intersections between the robot and the path that we are following:

<figure align="center">
    <video id="sampleMovie" src="Images/lookahead_circle.mov" height = "100%" width = "100%" style="border-radius: 1.5%" controls></video>
    <figcaption class="mt-2 text-sm text-center text-gray-600">Circle around the robot center intersecting the path</figcaption>
</figure>


In the case of our path following algorithm, the line-circle intersection equation would use the robot as the circle and the current segment of the path we are as the line. The center of the circle can be given by (robot x position , robot y position) with the radius being the lookahead distance. The two intersections between the circle are then fed into another method that chooses which one is the actual lookahead point by calculating how far they are from the end point of the path.

---

To find the coordinates at which the circle equation intersects the line equation, we will use the quadratic formula and the plug the respective quadratic values into the quadratic equation.

First, we need to do some math, so we can get the equations to find the a , b , and c terms of a quadratic equation to implement in our code.

## Turning Line-circle intersection into quadratic equation

To find the intersections between a circle and a line, we can directly plug the equation of a line into the y value of the circle.

- `Line equation` : mx + b
- `Circle equation` : (x - h)^2 + (y - k)^2 = r^2
- `Intersection equation` : (x - h)^2 + (mx + b - k)^2 = r^2

?> Now that we have the equation of the line-circle intersection, we can expand this equation and rearrange it.

<figure align="center">
    <img src="../Images/line-intersection-derive-1.jpg" class="rounded-lg" alt="lien circle intersection deriving 1">
    <figcaption class="mt-2 text-sm text-center text-gray-600">The equation for finding the intersection points of a line equation and a circle equation.</figcaption>
</figure>

---

<figure align="center">
    <img src="../Images/line-intersection-derive-2.jpg" class="rounded-lg" alt="line circle intersection deriving 2">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Group the constants, b and k , together to make the future math easier.</figcaption>
</figure>

---

<figure align="center">
    <img src="../Images/line-intersection-derive-3.jpg" class="rounded-lg" alt="line circle intersection deriving 3">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Expand the equation using the principle x^2 = x * x.</figcaption>
</figure>

---

<figure align="center">
    <img src="../Images/line-intersection-derive-4.jpg" class="rounded-lg" alt="line circle intersection deriving 4">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Use the distributive property to further expand the equation.</figcaption>
</figure>

---

<figure align="center">
    <img src="../Images/line-intersection-derive-5.jpg" class="rounded-lg" alt="line circle intersection deriving 5">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Rearrange the terms of the equation such that like terms are next to each other.</figcaption>
</figure>

---

<figure align="center">
    <img src="../Images/line-intersection-derive-6.jpg" class="rounded-lg" alt="line circle intersection deriving 6">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Factor out x^2 from the first two terms.</figcaption>
</figure>

---

<figure align="center">
    <img src="../Images/line-intersection-derive-7.jpg" class="rounded-lg" alt="line circle intersection deriving 7">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Factor out x from second two terms.</figcaption>
</figure>

---

<figure align="center">
    <img src="../Images/line-intersection-derive-8.jpg" class="rounded-lg" alt="line circle intersection deriving 8">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Subtract r^2 from both sides, so we can bring all the constants on one side of the equation.</figcaption>
</figure>

---

- `m` : Slope of the line that we are intersecting
- `b` : Y intercept of the line that we are intersecting
- `k` : Y value of the circle center (robot y position)
- `h` : X value of the circle center (robot x position)
- `r` : Radius of the circle (lookahead distance)

Since the highest degree of the final expanded equation is 2, we can come to the conclusion that this is a quadratic equation.


## Quadratic Equation

The quadratic equation is an algebraic equation of the second degrees in x:

- `Quadratic formula` : ax^2 + bx + c = 0

The a and b terms are the coefficients , x is the variable, and c is the constant.

<figure align="center">
    <img src="../Images/quadratic-equation.png" class="rounded-lg" alt="quadratic equation">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Example of a quadratic equation.</figcaption>
</figure>

---

<figure align="center">
    <img src="../Images/line-circle-quadratic.jpg" class="rounded-lg" alt="line circle quadratic">
    <figcaption class="mt-2 text-sm text-center text-gray-600">We have established that the line-circle intersection equation is quadratic, so we can find the a , b , and c term accordingly.</figcaption>
</figure>

- `a` : Term highlighted in red
- `b` : Term highlighted in blue
- `c` : Term highlighted in green

## Quadratic formula

The quadratic formula takes the 2 coefficients, a and b , and the constant, c , of a quadratic formula and finds the solutions of the quadratic.

<figure align="center">
    <img src="../Images/quadratic-formula.png" class="rounded-lg" alt="quadratic formula">
    <figcaption class="mt-2 text-sm text-center text-gray-600">The quadratic formula</figcaption>
</figure>

We can use this to find the x values at which the circle (robot) and the line (line segment of the path) intersect and then plug that back into the line equation to get the y value.

## Code implementation

For the code implementation, we will calculate the three quadratic terms using the equations we have found and plugging in the values using the robot's location and the points of the current line segment we are on in the path:
- `a` : m^2 + 1
- `b` : 2m(b - k) - 2h
- `c` : (b - k)^2 + h^2 -r^2

Since a line-circle intersection could possibly have two solutions (two intersection points), the method should return an array of intersection points instead of a single point.


```java 
// Parameter linePoint1: The starting point of the line segment we are on
// Parameter linePoint2: The ending point of the line segment we are on
// Parameter robotLocation: The coordinate point of the robot location
// Parameter lookaheadDistance: The radius of the circle
public static ArrayList<Point> lineCircleIntersection(Point linePoint1 , Point linePoint2 , Point robotLocation , double lookaheadDistance){
    /* First we need to account for a line segment on the path that could be straight vertical. 
    If this is the case, calculating the slope of this angle would return a divide by 
    zero error since the run would be zero in the rise / run formula.*/
    
    /*We can do this by checking if the difference between the end point x and 
    starting point x of the line is very low , indicating the line is vertical.
    If it is, then we can move the line a tiny amount so that the slope wouldn't be 0. */
    if(Math.abs(linePoint1.y - linePoint2.y) < 0.003){
        linePoint1.y = linePoint2.y + 0.003;
    }
    
    if(Math.abs(linePoint1.x - linePoint2.x) < 0.003){
        linePoint1.x = linePoint2.x + 0.003;
    }
    
    // Now we can calculate the slope of the line and store it
    // rise / run
    double lineSlope = (linePoint2.y - linePoint1.y) / (linePoint2.x - linePoint1.x);
    
    // Now that we have the slope of the line, we can calculate the y intercept by isolating b:
    /* y = mx + b
      -mx -mx
      y - mx = b, where (x , y) is any point of the line and m is the slope
    */
    // lets use the linePoint2 as the (x , y) and the lineSlope for m
    double yIntercept = linePoint2.y - lineSlope * linePoint2.x;
    
    // Now, we can calculate the quadratic A using the equation we found earlier :  m^2 + 1
    
    double quadraticA = Math.pow(lineSlope , 2) + 1;
    
    // Calculate the quadratic B using the equation we found earlier :  2m(b - k) - 2h
    /*
        m : slope of the line segment (lineSlope)
        b : y-intercept of the line segment (yIntercept)
        h : x value of the circle center (robotLocation.x)
        k : y value of the circle center (robotLocation.y)
    */
    
    double quadraticB = 2 * lineSlope * (yIntercept - robotLocation.y) - 2.0 * robotLocation.x;
    
    // Calculate the quadratic C using the equation we found earlier : (b - k)^2 + h^2 - r^2
    /*
        r : radius of the circle (lookaheadDistance)
    */
    
    double quadraticC = Math.pow((yIntercept - robotLocation.y) , 2) + Math.pow(robotLocation.x , 2) - Math.pow(lookaheadDistance , 2);
    
    /*Now that we have the quadraticA , quadraticB , and quadraticC , we can plug these
     values into the quadratic formula to the get the x values of the intersection points*/
 
    // Let's initialize an array list that we can add the intersection points to
    ArrayList<Point> intersectionPoints = new ArrayList<>();
    
    try{
        /*Since the quadratic formula has a plus or minus , we can compute two x solutions
        by using one equation with a minus sign and one with a plus sign.
        */
        
        // Use plus quadratic formula to get the first x solution
        double x1 = (-quadraticB + Math.sqrt(Math.pow(quadraticB , 2) - 4.0 * quadraticA * quadraticC)) / (2.0 * quadraticA);
        // Now that we have the x value of the intersection point on the line, we can plug it into our line equation to get the y value
        double y1 = lineSlope * x1 + yIntercept;
        
        // Now we have to make sure that the point is in range of the line.
        /* This is because the algorithm assume that the path is a continuous line.
            For example:
                robotLocation : ( 0 , 2)
                linePoint1 : (0 , 0)
                linePoint2 : (0 , 10)
                lookaheadDistance : 5.0
           The lookahead algorithm would calculate to intersections : one at (0 , 7) and one at (0 , -3). 
           We don't want the algorithm to recognize (0 , -3) as an intersection since it doesn't 
           even exist on the current path we are following. We can do this by setting a minimum and 
           maximum value an x value can have which in this case would be both 0 and a minimum and maximum value 
           an y value can have which in this case would be 0 and 10. 
        */
        
        // Check which point of the line segment has a lower x value
        double minX = linePoint1.x < linePoint2.x ? linePoint1.x : linePoint2.x;
        // Check which point of the line segment has a higher x value
        double maxX = linePoint1.x > linePoint2.x ? linePoint1.x : linePoint2.x;
        
        // Check which point of the line segment has a lower y value
        double minY = linePoint1.y < linePoint2.y ? linePoint1.y : linePoint2.y;
        // Check which point of the line segment has a higher y value
        double maxY = linePoint1.y > linePoint2.y ? linePoint1.y : linePoint2.y;
        
        // If the intersection is in the range of the line segment, then add it as an intersection
        
        if(x1 > minX && x1 < maxX && y1 > minY && y1 < maxY){
            intersectionPoints.add(new Point(x1 , y1));
        }
        
        // Now, let's use the minus quadratic formula to find any other existing intersections
        
        double x2 = (-quadraticB - Math.sqrt(Math.pow(quadraticB , 2) - 4.0 * quadraticA * quadraticC)) / (2.0 * quadraticA);
        double y2 = lineSlope * x2 + yIntercept;
        
        if(x2 > minX && x2 < maxX && y2 > minY && y2 < maxY){
            intersectionPoints.add(new Point(x2 , y2));
        }
        
    }catch (Exception e){
    
    }
    
    // Return all the intersections
    
    return intersectionPoints;
}
```

---

<p style = "font-weight : 300; font-size : 24px;">
This marks the end of the line-circle intersection page. In the following page, we will develop a method that takes in a path and the robot's location , gets the intersection points by inputting those into the line intersection method and chooses between the intersections to determine the lookahead point.
</p>
