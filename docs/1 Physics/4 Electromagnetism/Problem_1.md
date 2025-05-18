# Simulating the effects of the Lorentz Force

**The Lorentz force**, expressed as  
$$\vec{F} = q\vec{E} + q\vec{v} \times \vec{B}$$  
governs the behavior of charged particles in the presence of electric and magnetic fields. It is a cornerstone concept in **plasma physics**, **astrophysics**, and **particle accelerator technology**. Through simulation, we can gain a visual and intuitive understanding of how charged particles move under the influence of these fields.

### Exploration of Applications

**Key Systems:**
- **Particle Accelerators**: Control and acceleration of particles using electric/magnetic fields.
- **Mass Spectrometers**: Use magnetic deflection to separate particles by mass-to-charge ratio.
- **Plasma Confinement Devices**: Such as tokamaks, which rely on magnetic fields to trap hot plasma.

**Field Relevance:**
- **Electric Fields** $\vec{E}$: Accelerate particles.
- **Magnetic Fields** $\vec{B}$: Change direction, creating circular or helical motion.
- Crossed fields can induce drift velocities and lead to phenomena like $\vec{E} \times \vec{B}$ drift.

### Simulating Particle Motion

Numerically simulate the motion of a charged particle under various electromagnetic field configurations.

**Simulation Scenarios:**

![image](https://github.com/user-attachments/assets/731e1e52-2506-4795-b979-8dbcedabe76a)

- Expect circular motion (if velocity is perpendicular to $\vec{B}$) or **helical** (if there's a component along $\vec{B}$).
- Demonstrates cyclotron motion and introduces the concept of **Larmor radius** and **cyclotron frequency**.

![image](https://github.com/user-attachments/assets/f15af851-73a9-4ef0-95c9-ca24a454b417)

- Non-trivial motion—often helical with drift.
- Depending on vector orientation, the particle can accelerate, spiral, or follow curved paths.

![image](https://github.com/user-attachments/assets/de06c814-c144-4a25-a102-1d8126d128bd)

- Produces a **drift velocity**: $\vec{v}_{\text{drift}} = \frac{\vec{E} \times \vec{B}}{B^2}$
- Important for **magnetron motion** and behavior in **Hall effect**.

### Parameter Exploration

**Field Strength (E and B):**
- The strength of the magnetic field **B** will directly impact the radius of the motion of the particle. A stronger **B** leads to a smaller radius of motion.
- The electric field **E**, if present, could affect the overall trajectory and cause the particle to deviate from a perfect circular path.

**Initial Particle Velocity (V):**
- The velocity of the particle will affect the speed at which the particle moves in its path. The initial velocity should be broken down into components. If the velocity is perpendicular to the magnetic field, the particle will undergo circular motion. If there’s a component of velocity parallel to the magnetic field, the motion will become helical.

**Charge and Mass of the Particle (q and m):**
- The charge **q** affects the force exerted on the particle by the magnetic field. A greater charge leads to a larger Lorentz force, influencing the radius of the motion.
- The mass **m** of the particle determines the inertia of the particle, and thus, a heavier particle will have a larger radius of motion under the same field strength and velocity.

**Python Code**

<pre><code class="language-python">
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants
q = 1.0       # Charge (C)
m = 1.0       # Mass (kg)
B = np.array([0, 0, 1.0])  # Magnetic field (T)
E = np.array([0, 0, 0])    # Electric field (V/m)

# Initial conditions
v0 = np.array([1.0, 0.0, 0.5])  # Initial velocity (m/s)
r0 = np.array([0.0, 0.0, 0.0])  # Initial position (m)

# Simulation parameters
dt = 0.01  # Time step (s)
T = 20     # Total time (s)
N = int(T / dt)

# Arrays to store position and velocity
r = np.zeros((N, 3))
v = np.zeros((N, 3))
r[0] = r0
v[0] = v0

# Boris algorithm for integrating motion in E and B fields
def boris_push(v, r, q, m, E, B, dt):
    t = (q * B / m) * (dt / 2)
    s = 2 * t / (1 + np.dot(t, t))
    v_minus = v + (q * E / m) * (dt / 2)
    v_prime = v_minus + np.cross(v_minus, t)
    v_plus = v_minus + np.cross(v_prime, s)
    v_new = v_plus + (q * E / m) * (dt / 2)
    r_new = r + v_new * dt
    return v_new, r_new

# Simulate motion
for i in range(1, N):
    v[i], r[i] = boris_push(v[i-1], r[i-1], q, m, E, B, dt)

# Plotting the trajectory in 3D and 2D
fig = plt.figure(figsize=(14, 6))

# 3D trajectory
ax = fig.add_subplot(121, projection='3d')
ax.plot(r[:, 0], r[:, 1], r[:, 2], label='Trajectory', color='orange')
ax.set_title('3D Trajectory (Helical Motion)')
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_zlabel('Z')
ax.legend()

# 2D projection
ax2 = fig.add_subplot(122)
ax2.plot(r[:, 0], r[:, 1], label='XY Projection', color='orange')
ax2.set_title('2D Projection (Top View)')
ax2.set_xlabel('X')
ax2.set_ylabel('Y')
ax2.axis('equal')
ax2.legend()

plt.tight_layout()
plt.show()
</code></pre>

![image](https://github.com/user-attachments/assets/ef16ebc4-85b7-4ba5-ab6e-2baa1e0e757a)
![image](https://github.com/user-attachments/assets/3c92c261-ad98-4e76-86da-f97d0acea338)

The simulation shows a charged particle's helical motion in a uniform magnetic field. The 3D plot displays a spiral trajectory caused by circular motion in the XY-plane (due to the Lorentz force) combined with linear motion along the Z-axis. The 2D plot highlights the circular component of this motion.  
Key features include the **Larmor radius** (circular path size) and the **helix pitch**, reflecting the particle's velocity components perpendicular and parallel to the magnetic field.

<pre><code class="language-python">import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

# Constants for circular motion (v ⊥ B)
q = 1.0       # Charge (C)
m = 1.0       # Mass (kg)
B = np.array([0, 0, 1.0])  # Magnetic field (T)
E = np.array([0, 0, 0])    # Electric field (V/m)

# Initial conditions: velocity entirely perpendicular to B
v0 = np.array([1.0, 0.0, 0.0])  # No z-component
r0 = np.array([0.0, 0.0, 0.0])  # Starting at origin

# Simulation parameters
dt = 0.01  # Time step (s)
T = 20     # Total time (s)
N = int(T / dt)

# Arrays to store position and velocity
r = np.zeros((N, 3))
v = np.zeros((N, 3))
r[0] = r0
v[0] = v0

# Boris algorithm for integrating motion
def boris_push(v, r, q, m, E, B, dt):
    t = (q * B / m) * (dt / 2)
    s = 2 * t / (1 + np.dot(t, t))
    v_minus = v + (q * E / m) * (dt / 2)
    v_prime = v_minus + np.cross(v_minus, t)
    v_plus = v_minus + np.cross(v_prime, s)
    v_new = v_plus + (q * E / m) * (dt / 2)
    r_new = r + v_new * dt
    return v_new, r_new

# Simulate motion
for i in range(1, N):
    v[i], r[i] = boris_push(v[i-1], r[i-1], q, m, E, B, dt)

# Plotting the trajectory in 3D and 2D
fig = plt.figure(figsize=(14, 6))

# 3D trajectory
ax = fig.add_subplot(121, projection='3d')
ax.plot(r[:, 0], r[:, 1], r[:, 2], label='Trajectory', color='blue')
ax.set_title('3D Trajectory (Circular Motion)')
ax.set_xlabel('X')
ax.set_ylabel('Y')
ax.set_zlabel('Z')
ax.legend()

# 2D projection
ax2 = fig.add_subplot(122)
ax2.plot(r[:, 0], r[:, 1], label='XY Projection', color='blue')
ax2.set_title('2D Projection (Top View)')
ax2.set_xlabel('X')
ax2.set_ylabel('Y')
ax2.axis('equal')
ax2.legend()

plt.tight_layout()
plt.show()
</code></pre>

![image](https://github.com/user-attachments/assets/94ee6df1-2659-4769-a677-17771c9ae0bf)


This shows the particle confined to the XY-plane with a constant radius circular path. The Z-coordinate remains at zero throughout, which is consistent with a velocity entirely perpendicular to the magnetic field directed along the Z-axis.  
These plots visualize the fundamental physics of **cyclotron motion**, where the particle revolves at a constant **cyclotron frequency** with a radius known as the **Larmor radius**.

