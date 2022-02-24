
# Clip To Path

<p style = "font-weight : 300; font-size : 24px;">
This page will go over the clipToPath() method.
</p>

---


This method will intersect a perpendicular line going through the robot's center ( x position , y position) with every line segment of the path. It will then check which intersection point is the closest to the robot which will determine which line segment we are on. It will also tell us the index of the path we are currently on which we can then use to get that point of the path's details such as lookahead distance , movement speed , etc. This gives us control over the robot's lookahead distance and movement speed for each segment of the path.

---

<figure align="center">
    <video id="sampleMovie" src="Images/clip_to_path.mov" height = "100%" width = "100%" style="border-radius: 1.5%" controls></video>
    <figcaption class="mt-2 text-sm text-center text-gray-600">Current index and current segment example</figcaption>
</figure>

---

## Code Implementation

---

```java 
// Parameter path : Pass in the path array list that the robot is following
// Parameter robotLocation : Pass in the robot location (x position , y position)
public static Point clipToPath(ArrayList<Point> path , Point robotLocation){

}
```

### Iterate through path points

```java 
// Parameter path : Pass in the path array list that the robot is following
// Parameter robotLocation : Pass in the robot location (x position , y position)
public static Point clipToPath(ArrayList<Point> path , Point robotLocation){
        // Start off the closest distance really high
        double closestPointDistance = Double.MAX_VALUE;
        // Define the index to a random number so it isn't null
        int currLineIndex = 0;
        // Define a point at a random index so it isn't null. This will store the x and y of the intersection closest to us.
        CurvePoint pointOnPath = path.get(0);
        
        // Iterate through the points of the path
        for(int i = 0 ; i < path.size() - 1; i ++){
            
        }
}
```

### Clip To Line

```java 
// Parameter path : Pass in the path array list that the robot is following
// Parameter robotLocation : Pass in the robot location (x position , y position)
public static Point clipToPath(ArrayList<Point> path , Point robotLocation){
        // Start off the closest distance really high
        double closestPointDistance = Double.MAX_VALUE;
        // Define the index to a random number so it isn't null
        int currLineIndex = 0;
        // Define a point at a random index so it isn't null. This will store the x and y of the intersection closest to us.
        Point pointOnPath = path.get(0);
        
        // Iterate through the points of the path
        for(int i = 0 ; i < path.size() - 1; i ++){
            Point startPoint = path.get(i); // The start point of the line segment
            Point endPoint = path.get(i + 1); // The end point of the line segment
            
            // Intersect the perpendicular line
            Point clippedToLine = clipToLine(startPoint , endPoint , robotLocation);

            // Calulate the distance between the intersection and the robot
            double distanceToPoint = Math.sqrt(Math.pow(robotLocation.y - clippedToLine.y , 2) + Math.pow(robotLocation.x - clippedToLine.x , 2));
            
            /* If the distance is less than closestPointDistance, set the new closestPointDistance to
             distance and set currIndex to i + 1 and pointOnPath to the clippedLinePoint */
            if(distanceToPoint < closestPointDistance){
                closestPointDistance = distanceToPoint; // Save the closest distance
                pointOnPath = clippedToLine; // Set the x and y of pointOnPath equal to the intersection
                currLineIndex = i + 1; // We are setting it equal to i + 1 because that is the end point (destination) of the line segment 
            }
            // Go through loop again
        }
}
```

---

<p style = "font-weight : 300; font-size : 24px;">
Here's how the final clipToPath() method should look like:
</p>

```java 
// Parameter path : Pass in the path array list that the robot is following
// Parameter robotLocation : Pass in the robot location (x position , y position)
public static Point clipToPath(ArrayList<Point> path , Point robotLocation){
        // Start off the closest distance really high
        double closestPointDistance = Double.MAX_VALUE;
        // Define the index to a random number so it isn't null
        int currLineIndex = 0;
        // Define a point at a random index so it isn't null. This will store the x and y of the intersection closest to us.
        Point pointOnPath = path.get(0);
        
        // Iterate through the points of the path
        for(int i = 0 ; i < path.size() - 1; i ++){
            Point startPoint = path.get(i); // The start point of the line segment
            Point endPoint = path.get(i + 1); // The end point of the line segment
            
            // Intersect the perpendicular line
            Point clippedToLine = clipToLine(startPoint , endPoint , robotLocation);

            // Calulate the distance between the intersection and the robot
            double distanceToPoint = Math.sqrt(Math.pow(clippedToLine.y - robotLocation.y , 2) + Math.pow(clippedToLine.x - robotLocation.x , 2));
            
            /* If the distance is less than closestPointDistance, set the new closestPointDistance to
             distance and set currIndex to i + 1 and pointOnPath to the clippedLinePoint */
            if(distanceToPoint < closestPointDistance){
                closestPointDistance = distanceToPoint; // Save the closest distance
                pointOnPath = clippedToLine; // Set the x and y of pointOnPath equal to the intersection
                currLineIndex = i + 1; // We are setting it equal to i + 1 because that is the end point (destination) of the line segment 
            }
            // Go through loop again
        }
        
        // Return the point of intersection and index
        return new Point(pointOnPath.x , pointOnPath.y , currLineIndex);
}
```

<p style = "font-weight : 300; font-size : 24px;">
We now have a method that can tell us which index of the path we are currently following. By using this method, we can set specific lookahead distances and movement speeds for each line segment of the path.
</p>
