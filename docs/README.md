# Get Started

<p style = "font-weight : 300; font-size : 24px;">
A comprehensive guide and documentation on implementation a minimalistic path following algorithm in FTC
</p>

---

>[!WARNING]
> This site assumes that you are already moderately-versed with the Java language the FTC SDK.

> [!TIP]
> I aim to provide explanations and implementations of the different control systems to programmers of FTC regardless of their experience or prior knowledge level.

> [!TIP]
> If your team does not want to invest money into expensive hardware such as encoders and dead wheels, this implementation may not be the right one for you.


## Introduction

---


### Mission
Welcome! This website serves as a comprehensive documentation and guide on the implementation of field centric “pure pursuit” for Holonomic Drivetrains in FTC.
This is intended to serve tips , sample code, and resources needed along with explanations and implementations of different control systems for accurate path following.

Any team looking to implement a minimalistic and time efficient path following algorithm in FTC will be able to do so by following the code and conceptual explanations in this documentation.
My goal is that the code samples and concept sections will give simple explanations that will
enable anyone to understand the algorithm completely and trouble shoot any problems they may incur.


## Tank Drive vs Mecanum


---


<figure align="center">
    <img src="Images/field-centric-pure-pursuit-implementation.gif" class="rounded-lg" alt="Example of field-centric pure pursuit" style="border-radius:1.5%;">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Path follower implemented for a Mecanum Drivetrain</figcaption>
</figure>

---

<figure align="center">
    <img src="Images/tank-follow.gif" class="rounded-lg" alt="Example of field-centric pure pursuit" style="border-radius:1.5%;">
    <figcaption class="mt-2 text-sm text-center text-gray-600">Path follower implemented for a Tank Drivetrain</figcaption>
</figure>


---

This path follower can be implemented for both Tank and Mecanum drivetrains. However, there are some key differences between what is needed and how some methods are implemented for each respective drive train.
Each page will contain one of the notification bars shown below:

> [!ATTENTION]
> This is for both Tank and Mecanum Drivetrains

> [!ATTENTION]
> This is only for Mecanum drivetrains

> [!ATTENTION]
> This is only for Tank drivetrains

If the page does not contain implementations or explanations necessary for your drive train type, you may skip over it.

---

## Skills you will need

> [!TIP]
> Make sure you know all of these topics thoroughly as it is the foundation for our path-following algorithm. Without knowing these topics, you will get lost as we progress through the difficult topics and concepts.

<span style = "font-size : 20px; font-weight : 100;">
Although this implementation is very simple, there are some topics you will need to understand before proceeding. The topics are listed below along with links to resources that may help refresh these topics or learn them from scratch.
</span>

---

1. Understanding of simple Trigonometry (Cosine , Secant , Tangent, etc.)
   - [Visual explanation of trig functions](https://www.mathsisfun.com/sine-cosine-tangent.html)
   - [The Organic Chemistry Tutor trig functions](https://www.youtube.com/watch?v=HAole1-hadc)

2. Understanding of hardware (Motors , Encoders)
   - [Rev robotics: Explanation of encoder modes and getting positions](https://docs.revrobotics.com/rev-control-system/programming/using-encoder-feedback)

3. Basic Calculus (Derivatives , integrals)
   - [An intro to derivatives in Calculus](https://www.mathsisfun.com/calculus/derivatives-introduction.html)
   - [An intro to Integrals in Calculus](https://www.cuemath.com/calculus/integral/)

4. Knowledge of the java programming knowledge
   - [A full 12-hour Java course](https://www.youtube.com/watch?v=xk4_1vDrzzo)


```java 
    public static void main(String[] args) {
        // An arraylist of type Point is initialized
        ArrayList<Point> pathPoints = new ArrayList<>();

        // Adding points to the array list
        pathPoints.add(new Point(0 , 0));
        pathPoints.add(new Point(0 , 25));
        pathPoints.add(new Point(15 , 40));

        // Storing the output of the method as a variable
        boolean valueExists = xValueExists(pathPoints , 40);

        // Printing the variable to view the result
        System.out.println(valueExists);

    }

      /*
        Method returns a boolean
        Parameter pathPoints is of type ArrayList<Point>
        Parameter xValue is of type double
      */
  
    public static boolean xValueExists(ArrayList<Point> pathPoints , double xValue){
        // Iterates through the list of points
  
        for(int i = 0 ; i < pathPoints.size(); i ++){
            /* If statement checks the x value of the current point in the iteration process is
             equal to the x value you are looking for */
  
            if(pathPoints.get(i).x == xValue){
                return true;
            }
        }

       // returns false if none of the x values of the points in the list were equal to the xValue
       return false;
    }
```


