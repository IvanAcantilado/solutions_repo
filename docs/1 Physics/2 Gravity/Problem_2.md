# Escape Velocities and Cosmic Velocities

Understanding **Escape Velocity** is fundamental to grasping what it takes to overcome a celestial body's gravitational pull. Building on this idea, the first, second, and third cosmic velocities represent the critical speeds needed to achieve orbit, break free from a planet's gravity, and ultimately exit an entire star system.

These concepts form the foundation of modern space exploration, enabling everything from satellite deployment to deep-space missions.

## Definitions

**1. First Cosmic Velocity (Orbital Velocity)**  
Minimum velocity required to orbit a planet near its surface in a circular path. It's the speed at which centripetal force equals gravitational force.  

*From Newton’s law of gravitation and centripetal force:*

$$
\frac{GMm}{R^2} = \frac{mv^2}{R} \Rightarrow v_1 = \sqrt{\frac{GM}{R}}
$$

**2. Second Cosmic Velocity (Escape Velocity)**  
Minimum speed required to break free from a celestial body's gravitational field without further propulsion.  

*Total mechanical energy at the surface must be zero for escape:*

$$
\frac{1}{2}mv^2 - \frac{GMm}{R} = 0 \Rightarrow v_2 = \sqrt{\frac{2GM}{R}}
$$

**3. Third Cosmic Velocity (Interstellar Velocity)**  
Minimum velocity needed to escape the Sun’s gravity starting from a planet’s orbit (used for interstellar missions).  

*Assuming solar escape velocity from orbit:*

$$
v_3 = \sqrt{2} \cdot v_{\text{orbital around Sun}}
$$

*From Earth’s orbital radius and Sun’s mass:*

$$
v_3 \approx \sqrt{\frac{2GM_\odot}{R_{\text{orbit}}}
$$

*Or, estimated from Earth’s escape speed plus solar influence:*

$$
v_3 \approx \sqrt{2} \cdot v_1
$$

---

### Simulation Results

**Here are calculated values for Earth, Mars, and Jupiter:**

#### 🌍 Earth

- **1st Cosmic (~7900 m/s)** – Velocity needed to maintain a circular orbit just above Earth's surface (Low Earth Orbit).  
- **2nd Cosmic (~11200 m/s)** – The escape velocity — needed to break free from Earth’s gravity without further propulsion.  
- **3rd Cosmic (~11180 m/s)** – Velocity to leave the solar system, starting from Earth’s orbit — accounting for Earth’s motion around the Sun.

#### 🔴 Mars

- **1st Cosmic (~3500 m/s)** – Much lower orbital velocity due to Mars' smaller mass and gravity.  
- **2nd Cosmic (~5000 m/s)** – Escape velocity is also lower than Earth’s.  
- **3rd Cosmic (~4950 m/s)** – Slightly less than the escape velocity again, due to Mars already orbiting the Sun at high speed.

#### 🟠 Jupiter

- **1st Cosmic (~42200 m/s)** – Very high orbital speed needed due to Jupiter's strong gravity.  
- **2nd Cosmic (~59500 m/s)** – The energy needed to escape Jupiter’s gravity is massive.  
- **3rd Cosmic (~59600 m/s)** – Almost the same as the 2nd cosmic velocity — Jupiter is already moving fast in its solar orbit.

---

## Computational Model (Python)

<pre><code class="language-python">import matplotlib.pyplot as plt
import numpy as np

# Data
bodies = ['Earth', 'Mars', 'Jupiter']
v1 = [7900, 3500, 42200]    # 1st Cosmic Velocity
v2 = [11200, 5000, 59500]   # 2nd Cosmic Velocity
v3 = [11180, 4950, 59600]   # 3rd Cosmic Velocity

x = np.arange(len(bodies))  # the label locations
width = 0.25                # width of the bars

# Plot
fig, ax = plt.subplots(figsize=(10, 6))

bars1 = ax.bar(x - width, v1, width, label='1st Cosmic Velocity (Orbital)', color='orange')
bars2 = ax.bar(x, v2, width, label='2nd Cosmic Velocity (Escape)', color='orangered')
bars3 = ax.bar(x + width, v3, width, label='3rd Cosmic Velocity (Interstellar)', color='deeppink')

# Labels and Title
ax.set_ylabel('Velocity (m/s)')
ax.set_title('Cosmic Velocities for Different Celestial Bodies')
ax.set_xticks(x)
ax.set_xticklabels(bodies)
ax.legend()

# Grid and Layout
ax.grid(axis='y', linestyle='--', alpha=0.7)
plt.tight_layout()
plt.show()
</code></pre>

![image](https://github.com/user-attachments/assets/938cf3a5-fe1a-4ae2-8012-235c2e0b795b)

---

## Importance in Space Exploration

| Velocity Type | Relevance |
|---------------|-----------|
| 1st Cosmic    | Launching satellites into low Earth orbit (LEO), like the ISS. |
| 2nd Cosmic    | Space probes, lunar missions (Apollo), Mars rovers. |
| 3rd Cosmic    | Voyager, New Horizons — missions aiming to leave the solar system. |

---

## Conclusion

**Understanding these velocities is crucial for**:  
Efficient fuel planning, mission architecture, propulsion system requirements, and future interplanetary and interstellar missions.
