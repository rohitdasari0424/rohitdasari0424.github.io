
# Tuneable Constants Interface
<p style = "font-weight : 300; font-size : 24px;">
This section will go over the Constants Interface.
</p>

---

The Constants Interface will store all the tunable constants :

---

<b>Drive Forward PID Controller</b>
- `DRIVE_KP` : KP value
- `DRIVE_KI` : KI value
- `DRIVE_KD` : KD value

---

<b>Strafe PID Controller</b>
- `STRAFE_KP` : KP value
- `STRAFE_KI` : KI value
- `STRAFE_KD` : KD value

---

<b>Turn PID Controller</b>
- `TURN_KP` : KP value
- `TURN_KI` : KI value
- `TURN_KD` : KD value

---

<b>Odometry</b>
- `trackWidth`
- `auxWidth`

---

## Code Implementation

For now , let's set all the values to zero. We can change these values as we tune them.

```java
public interface TUNEABLE_CONSTANT{
    double DRIVE_KP = 0;
    double DRIVE_KI = 0;
    double DRIVE_KD = 0;
    
    double STRAFE_KP = 0;
    double STRAFE_KI = 0;
    double STRAFE_KD = 0;
    
    double TURN_KP = 0;
    double TURN_KI = 0;
    double TURN_KD = 0;
    
    double TRACKWIDTH = 0;
    double AUXWIDTH = 0;
}

```
