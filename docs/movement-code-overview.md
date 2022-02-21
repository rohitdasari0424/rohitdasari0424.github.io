
# Movement Code

<p style = "font-weight : 300; font-size : 24px;">
This section will go over the methods and equation to set powers to the motor and bring the robot to the final point in a path.
</p>

---

## File to create

There are no files we need to create for this section. We will be adding the necessary variables directly to the mecanum drive class we made earlier.

## Methods to create
- `goToPosition()` : Get the three movement variables to get the robot from one position to another
- `fieldCentric()` : Turns the three movement variables into field centric powers to get the robot from one position to another based on robot heading
- `followPath()` : Will calculate the lookahead point , heading point , and call the goToPosition() method to go to these target positions

---

<p style = "font-weight : 300; font-size : 24px;">
In the following pages, we will implement the fieldCentric, goToPosition() , and followPath() methods.
</p>
