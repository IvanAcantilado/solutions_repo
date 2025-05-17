# Investigating the Range as a Function of the Angle of Projection

This investigation examines how the range of a projectile is affected by the angle at which it is launched. By varying the angle of projection and measuring the resulting horizontal distance, we aim to identify patterns in the data and determine the angle that produces the maximum range.

## Theoretical Foundation

Projectile motion describes the motion of an object under the influence of gravity, neglecting air resistance. The object follows a parabolic trajectory determined by its initial conditions: initial speed $v_0$, angle of projection $theta$, and gravitational acceleration $g$.

**Equations of Motion:**

We start with Newton's Second Law:  
$$ F = m a $$

For projectile motion, the only force acting is gravity. The horizontal and vertical components of motion can be treated separately:

- **Horizontal:** constant velocity motion  
- **Vertical:** uniformly accelerated motion

Let:  
- $v_0$: initial speed  
- $\theta$: angle of projection  
- $g$: acceleration due to gravity  

**Horizontal motion:**  
$$
x(t) = v_0 \cdot \cos(\theta) \cdot t
$$

**Vertical motion:**  
$$
y(t) = v_0 \cdot \sin(\theta) \cdot t - \frac{1}{2} g t^2
$$

## Time of Flight

The projectile lands when $y(t) = 0$. Solving for $t$:

$$
0 = v_0 \cdot \sin(\theta) \cdot t - \frac{1}{2} g t^2
$$

Simplifying this, we get:

$$
t \left(v_0 \cdot \sin(\theta) - \frac{1}{2} g t \right) = 0
$$

Ignoring the $t = 0$ solution:

$$
t = \frac{2 v_0 \sin(\theta)}{g}
$$

**Range of the Projectile**  
Substitute time of flight into the horizontal motion equation:

$$
R = x(t) = v_0 \cdot \cos(\theta) \cdot \frac{2 v_0 \sin(\theta)}{g}
$$

Simplifying, we get the final form of the range equation:

$$
R = \frac{v_0^2 \sin(2\theta)}{g}
$$

## Analysis of the Range

**Influence of Angle**

As shown by the formula $R = \frac{v_0^2 \sin(2\theta)}{g}$, the range follows a sine curve with respect to $2\theta$, peaking at $45^\circ$. Beyond this, the range decreases symmetrically.

**Influence of Initial Velocity**  
Since $R \propto v_0^2$, increasing the initial speed leads to a quadratic increase in the range.

**Influence of Gravity**  
The range is inversely proportional to gravity. On planets with lower gravity (e.g., the Moon), the range increases.

## Practical Applications

- **Uneven Terrain:** The standard model assumes launch and landing at the same height. When the launch or landing height changes, the time of flight and range must be recalculated using modified kinematic equations.  
- **Air Resistance:** In real-world applications (e.g., ballistics, sports, engineering), air resistance can significantly reduce the range and alter the trajectory shape. Incorporating drag involves solving differential equations with velocity-dependent forces.  
- **Sports:** Optimizing projectile angles in games like basketball or soccer.  
- **Engineering:** Designing trajectories in ballistics or launching mechanisms.

## Implementation

**Python Simulation**

<pre><code class="language-python">import numpy as np
import matplotlib.pyplot as plt

# Parameters
v0 = 20  # initial velocity in m/s
g = 9.81  # gravity in m/s^2
angles = np.radians(np.linspace(0, 90, 100))

# Calculate ranges
ranges = (v0**2 * np.sin(2 * angles)) / g

# Plot
plt.figure(figsize=(10, 6))
plt.plot(np.degrees(angles), ranges)
plt.title("Range as a Function of Angle of Projection")
plt.xlabel("Angle of Projection (degrees)")
plt.ylabel("Range (meters)")
plt.grid(True)
plt.axvline(45, color='r', linestyle='--', label='Max Range at 45°')
plt.legend()
plt.show()
</code></pre>

![image](https://github.com/user-attachments/assets/2e946e2a-a438-4e49-aea2-ee4c5e49554c)

*Running the above script will generate a graph showing the horizontal range as a function of the angle of projection for a given initial velocity. The curve will demonstrate that the range is maximized at 45∘*

## Conclusion
The range of a projectile depends on the initial velocity, gravitational acceleration, and the angle of projection. The range is maximized at an angle of 45∘, and the relationship between the range and the angle is symmetrical.

The theoretical model assumes ideal conditions with no air resistance and flat terrain. In real-world scenarios, modifications are needed to account for factors like air resistance and uneven terrain, which can significantly alter the trajectory. The model provides a foundational understanding of projectile motion, but further analysis is required to simulate more complex situations.
