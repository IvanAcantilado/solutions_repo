# Investigating the Range as a Function of the Angle of Projection
This investigation examines how the range of a projectile is affected by the angle at which it is launched. By varying the angle of projection and measuring the resulting horizontal distance, we aim to identify patterns in the data and determine the angle that produces the maximum range.

## Theoretical Foundation
Projectile motion describes the motion of an object under the influence of gravity, neglecting air resistance. The object follows a parabolic trajectory determined by its initial conditions: initial speed 𝑣𝜃, angle of projection 𝜃, and gravitational acceleration 𝑔.

<b>Equations of Motion:</b>

We start with Newton's Second Law:
<p>$$ F = m \\a $$</p>

For projectile motion, the only force acting is gravity. The horizontal and vertical components of motion can be treated separately:
- Horizontal: constant velocity motion
- Vertical: uniformly accelerated motion

Let:
<ul>
<li>𝑣𝜃: initial speed<</li>
<li>𝜃: angle of projection</li>
<li>𝑔: acceleration due to gravity</li>
</ul>

<b>Horizontal motion:</b>
<p>$$ x(t) = v_0 \cdot \cos(\theta) \cdot t $$</p>
<b>Vertical motion:</b>
<p>$$ y(t) = v_0 \cdot \sin(\theta) \cdot t - \frac{1}{2} g t^2 $$</p>

## Time of Flight
The projectile lands when <b>𝑦(𝑡)=<i>0</i></b>. Solving for <b>𝑡</b>:
<p>$$ 0 = v_0 \cdot \sin(\theta) \cdot t - \frac{1}{2} g t^2 $$</p>
Simplifying this, we get:
<p>$$ t(v_0 \cdot \sin(\theta) - \frac{1}{2} g t) = 0 $$</p>
Ignoring the <b>𝑡=<i>0</i></b> solution:
<p>$$ t = \frac{2v_0 \sin(\theta)}{g} $$</p>
<b>Range of the Projectile</b><br />
Substitute time of flight into the horizontal motion equation:
<p>$$ R = x(t) = v_0 \cdot \cos(\theta) \cdot \frac{g}{2v_0 \sin(\theta)} $$</p>
Simplifying, we get the final form of the range equation:
<p>$$ R = \frac{v_0^2 \sin(2\theta)}{g} $$</p>
## Analysis of the Range
<b>Influence of Angle</b>

As shown by the formula $R = \frac{v_0^2 \sin(2\theta)}{g}$, the range follows a sine curve with respect to $2\theta$, peaking at $45^\circ$.Beyond this, the range decreases symmetrically.

<b>Influence of Initial Velocity</b><br />
Since $R \propto v_0^2$ increasing the initial speed leads to a quadratic increase in the range.
<b>Influence of Gravity</b><br />
The range is inversely proportional to gravity. On planets with lower gravity (e.g., the Moon), the range increases.
## Practical Applications
<b>Uneven Terrain</b>: The standard model assumes launch and landing at the same height. When the launch or landing height changes, the time of flight and range must be recalculated using modified kinematic equations.<br />
<b>Air Resistance</b>: In real-world applications (e.g., ballistics, sports, engineering), air resistance can significantly reduce the range and alter the trajectory shape. Incorporating drag involves solving differential  equations with velocity-dependent forces.<br />
<b>Sports</b>: Optimizing projectile angles in games like basketball or soccer.<br />
<b>Engineering</b>: Designing trajectories in ballistics or launching mechanisms.<br />
## Implementation
<b>Python Simulation</b>
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
![image](https://github.com/user-attachments/assets/dbb7d00f-973d-49d5-8e31-54a1622f1c24)
<i>Running the above script will generate a graph showing the horizontal range as a function of the angle of projection for a given initial velocity. The curve will demonstrate that the range is maximized at 45∘</i>

## Conclusion
The range of a projectile depends on the initial velocity, gravitational acceleration, and the angle of projection. The range is maximized at an angle of 45∘, and the relationship between the range and the angle is symmetrical.

The theoretical model assumes ideal conditions with no air resistance and flat terrain. In real-world scenarios, modifications are needed to account for factors like air resistance and uneven terrain, which can significantly alter the trajectory. The model provides a foundational understanding of projectile motion, but further analysis is required to simulate more complex situations.
