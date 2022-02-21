# PID Tuning

<p style = "font-weight : 300; font-size : 24px;">
This section will go over the tuning process of PID. The process of tuning the three controllers consists of tuning the turn controller first, then the drive controller, and finally the strafe controller.
</p>

---

Much of using the Pure Pursuit algorithm is spent on tuning its three PID controllers, as well-tuned PID controllers are essential for an accurate and smooth path following algorithm.

---

## Tuning a PID Controller
Tuning a PID Controller can be a hard learning process, but eventually gets easier after time.
Sometimes, using a P or PD (Proportional or Proportional-Derivative) controller will suffice for many purposes, but a PID controller (using all terms) is optimal.

### Tuning Proportional
The goal for tuning the proportional term is to get to a state where the robot oscillates at the target but still settles (or stops)
at the target eventually. We can adjust for KP so that we can get the desired oscillation (ex: should the robot oscillate a minimal amount or not?)

<figure align="center">
    <img src="Images/d-value-use-case.gif" alt="Example where D-Value should be used" style="width : 60%;">
    <figcaption class="mt-2 text-sm text-center text-gray-600">The robot overshoots target , then undershoots, then overshoots a tiny bit, and finally arrives at the target. This is called oscillation.</figcaption>
</figure>

1. First, enter a random KP value. It must be small. Using 0.05 as an initial KP value will be fine.
2. Run the code
- If the robot undershoots the target a considerable amount then increase KP.
- If the robot oscillates at the target and doesn't settle at the target, then decrease KP and re-run code.
- If the robot oscillates at the target but does settle at the target eventually,
  you can slightly adjust KP until you get your desired oscillation. Once you get to the state, you are done with tuning KP and can move onto KD.


### Tuning Derivative
The robot reaches the target properly but oscillates around it, hence the solution to this is adding the derivative term to the equation.

<figure align="center">
    <img src="Images/properly-tuned-d-value.gif" alt="Properly tuned KD" style="width : 60%;">
    <figcaption class="mt-2 text-sm text-center text-gray-600">A properly tuned KD value brings the robot to the target position smoothly with minimal oscillation.</figcaption>
</figure>

1. First, enter a random KD value. It must be MINUSCULE. Using a 0.00005 as an initial KP value will be fine.
2. Run the code
- If the robot reaches its target but still oscillates a noticeable amount, then increase KD and re-run code.
- If the robot jitters at the target (rapidly oscillates at the target), then decrease KD a lot and re-run code.
- If the robot reaches its target with noticeably small amount of oscillation, then keep increasing KD and re-running the code until the robot reaches its target with very little to no oscillations. If this state is reached, then you are done with tuning KD.

### Tuning Integral
The robot can now reach its target with little to no oscillations. However, the robot sometimes is just slightly out of range for the stop state to trigger. This is where the Integral term will be helpful because as the summation of error increases over time,
the robot will be pushed into the range where stop state can be triggered. In other words, the I term is used to bring the error to 0 as close as possible.

1. First, enter a random KI value. As earlier, using 0.05 as an initial KI value will be fine.
2. Run the code
- If the robot is slightly out of range at times, then increase KI slightly and re-run code.
- If the robot overshoots, then decrease KI depending on how much it overshot and re-run code.
- If the robot reaches its target with a tiny error value, then keep increasing KI and re-running the code until the robot reaches its target with a minisucle error amoutn. If this state is reached, then you are done with tuning KI.
