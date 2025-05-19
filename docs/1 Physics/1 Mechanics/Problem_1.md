# Investigating the Range as a Function of the Angle of Projection

---

## Theoretical Foundation

### Derivation of the Equations of Motion

Projectile motion is a form of two-dimensional motion under constant acceleration due to gravity. It can be derived from Newton’s second law:

$$
\vec{F} = m \vec{a}
$$

In the absence of air resistance, the only force acting on the projectile after launch is gravity. The motion can be decomposed into two orthogonal components: horizontal and vertical.

**Horizontal motion (constant velocity):**

$$
x(t) = v_0 \cos \theta \cdot t
$$

**Vertical motion (uniform acceleration):**

$$
y(t) = v_0 \sin \theta \cdot t - \frac{1}{2} g t^2
$$

Here:  
- $v_0$ is the initial velocity,  
- $\theta$ is the angle of projection,  
- $g$ is the acceleration due to gravity,  
- $t$ is the time.

These are solutions to the second-order differential equations:

$$
\frac{d^2 x}{dt^2} = 0 \quad \text{(no horizontal acceleration)}
$$

$$
\frac{d^2 y}{dt^2} = -g \quad \text{(constant vertical acceleration)}
$$

Solving these gives the first derivatives:

$$
\frac{dx}{dt} = v_0 \cos \theta
$$

$$
\frac{dy}{dt} = v_0 \sin \theta - g t
$$

Integrating with respect to time yields the position functions given above.

---

### Range as a Function of Angle

To determine the range $R$ (the horizontal distance traveled when $y=0$), solve $y(t) = 0$ for $t \neq 0$:

$$
t = \frac{2 v_0 \sin \theta}{g}
$$

Substitute this into the horizontal displacement:

$$
R(\theta) = v_0 \cos \theta \times \frac{2 v_0 \sin \theta}{g} = \frac{v_0^2 \sin (2\theta)}{g}
$$

This expression reveals that the range is maximized when $\theta = 45^\circ$ and symmetrically decreases for angles above or below this value.

---

### Family of Solutions

The parametric nature of projectile motion means that by varying:

- $v_0$: changes the scale of motion,
- $\theta$: alters the shape and symmetry,
- $g$: affects vertical acceleration (useful for different planetary conditions),
- initial height $h$ (if added): modifies time of flight and total range,

we obtain a family of trajectories — all governed by the same physical laws but producing a wide variety of outcomes. This makes projectile motion an excellent model for studying how initial conditions influence physical systems.

---

## Analysis of the Range

### Dependence on Angle of Projection

The range function

$$
R(\theta) = \frac{v_0^2 \sin (2\theta)}{g}
$$

indicates that:

- The maximum range occurs at $\theta = 45^\circ$ because $\sin(2\theta)$ reaches its peak value of 1 at $90^\circ$.
- The range is symmetric about $45^\circ$; angles $\theta$ and $90^\circ - \theta$ give the same range.

### Effect of Initial Velocity and Gravity

- Increasing $v_0$ increases the range quadratically since $R \propto v_0^2$.
- Increasing gravitational acceleration $g$ decreases the range inversely: $R \propto \frac{1}{g}$.

### Influence of Launch Height

If the launch height $h$ is non-zero, the total flight time increases and the symmetry in range with respect to angle is lost. The range formula becomes more complex and must be found by solving the quadratic equation in $t$ given by:

$$
y(t) = h + v_0 \sin \theta \cdot t - \frac{1}{2} g t^2 = 0
$$

The range is then:

$$
R(\theta) = v_0 \cos \theta \cdot t_{\text{flight}}
$$

where $t_{\text{flight}}$ is the positive root of the above quadratic.

Graphs illustrating these effects help visualize how the range curve shifts and scales when parameters change.

---

## Practical Applications

The idealized projectile model can be adapted or extended to more realistic situations:

- **Uneven Terrain:** Launch and landing heights differ, requiring adjustment of the time of flight and range calculations.
- **Air Resistance:** Drag forces slow the projectile, reducing range and changing optimal launch angle, often requiring numerical solutions.
- **Wind Effects:** Lateral forces cause trajectory deviation, adding complexity beyond two-dimensional motion.
- **Sports:** Optimizing angles in golf, basketball, or soccer to maximize distance or accuracy.
- **Engineering and Ballistics:** Designing trajectories for rockets or projectiles where precise targeting is crucial.
- **Astrophysics:** Calculations of orbital launches and landings on planets with different gravitational accelerations.

These real-world factors motivate expanding the model beyond simple analytic solutions.

---

## Implementation

### Computational Simulation

Develop a Python program to simulate projectile motion and analyze the range:

- Input parameters: initial velocity $v_0$, angle $\theta$, gravitational acceleration $g$, and launch height $h$.
- Calculate the time of flight by solving $y(t) = 0$ (for $h \neq 0$, solve quadratic numerically).
- Compute the range as:

$$
R = v_0 \cos \theta \times t_{\text{flight}}
$$

- Sweep $\theta$ from $0^\circ$ to $90^\circ$ to plot $R(\theta)$.
- Visualize representative projectile trajectories for selected angles.

<head>
    <meta charset="UTF-8">
</head>
<body>

    <button onclick="toggleCode()">Show Code</button>

    <div id="code-block" style="display: none;">
<pre><code>
import numpy as np
import matplotlib.pyplot as plt

# Constants
g = 9.81  # gravity (m/s^2)
v0 = 30   # initial velocity (m/s)
h = 0     # launch height (m)
angles = np.radians(np.linspace(0, 90, 100))  # angles in radians

def compute_range(theta, v0, g, h=0):
sin_theta = np.sin(theta)
cos_theta = np.cos(theta)
if h == 0:
t_flight = 2 * v0 * sin_theta / g
else:
discriminant = (v0 * sin_theta)**2 + 2 * g * h
t_flight = (v0 * sin_theta + np.sqrt(discriminant)) / g
return v0 * cos_theta * t_flight

ranges = np.array([compute_range(theta, v0, g, h) for theta in angles])

# Plot Range vs Angle
plt.figure(figsize=(10, 6))
plt.plot(np.degrees(angles), ranges)
plt.title('Range vs. Angle of Projection')
plt.xlabel('Angle (degrees)')
plt.ylabel('Range (m)')
plt.grid(True)
plt.savefig("range_vs_angle.png")
plt.show()

# Plot Trajectories
plt.figure(figsize=(10, 6))
for theta_deg in [15, 30, 45, 60, 75]:
theta = np.radians(theta_deg)
t_max = compute_range(theta, v0, g, h) / (v0 * np.cos(theta))
t = np.linspace(0, t_max, num=200)
x = v0 * np.cos(theta) * t
y = h + v0 * np.sin(theta) * t - 0.5 * g * t**2
plt.plot(x, y, label=f'{theta_deg}°')

plt.title('Projectile Trajectories for Various Angles')
plt.xlabel('Horizontal Distance (m)')
plt.ylabel('Vertical Height (m)')
plt.legend()
plt.grid(True)
plt.savefig("trajectories.png")
plt.show()
        </pre></code>
    </div>

    <script>
        function toggleCode() {
            const codeBlock = document.getElementById("code-block");
            const button = document.querySelector("button");
            if (codeBlock.style.display === "none") {
                codeBlock.style.display = "block";
                button.textContent = "Hide Code";
            } else {
                codeBlock.style.display = "none";
                button.textContent = "Show Code";
            }
        }
    </script>

</body>

![Range as a Functio of Angle of Projection](https://github.com/user-attachments/assets/c43f1c8c-6b17-44eb-9435-a6dd436df76f)

![Projection Trajectories for Various Angles](https://github.com/user-attachments/assets/ae7d24e7-caad-4408-aef3-a8e4144889fc)

The simulation provides a hands-on way to explore how changing parameters affects projectile motion.

---

## 5. Limitations and Proposed Extensions

### Limitations

- Assumes no air resistance or drag, which is unrealistic for most practical cases.
- Assumes constant gravitational acceleration and flat terrain.
- Neglects wind and lateral forces.
- Assumes instantaneous launch without propulsion after initial velocity.

### Proposed Extensions

- Incorporate drag force models (linear or quadratic) to simulate air resistance and its effect on range and trajectory.
- Add wind effects as lateral forces that affect horizontal displacement.
- Introduce terrain models with variable landing heights for more realistic conditions.
- Use numerical solvers (e.g., Runge-Kutta methods) to solve differential equations that do not have closed-form analytical solutions.

These enhancements make the model closer to real-world physics, expanding its applicability in sports science, engineering, and astrophysics.
