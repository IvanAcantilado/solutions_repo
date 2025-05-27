# Orbital Period and Orbital Radius

The orbital period refers to the time a body takes to complete one full orbit around another object, such as the Earth orbiting the Sun or a moon orbiting a planet. This period is typically measured in units of time, such as seconds, days, or years, and depends on the mass of the central object and the distance between the two bodies.

The orbital radius, on the other hand, is the average distance from the orbiting body to the center of the object it is orbiting. For circular or nearly circular orbits, it is essentially the radius of the orbit. This distance plays a crucial role in determining the orbital speed and period through **Kepler’s Laws** and **Newton’s Law of Gravitation**.

Understanding these two properties is essential for calculating satellite trajectories, planning space missions, and studying the dynamics of planetary systems.

---

## Derivation of the Formula

Consider a body of mass $m$ orbiting a much larger body of mass $M$ in a circular orbit of radius $r$ and period $T$.

#### Centripetal Force and Gravitational Force

$$
\frac{G M m}{r^2} = m \frac{v^2}{r}
$$

Where:

- $G$ is the gravitational constant
- $v$ is the orbital speed.

Canceling $m$ and multiplying both sides by $r$:

$$
\frac{GM}{r} = v^2
$$

#### Expressing Speed in Terms of Period

The orbital speed $v$ is also given by:

$$
v = \frac{2 \pi r}{T}
$$

Substitute into the previous equation:

$$
\frac{GM}{r} = \left( \frac{2\pi r}{T} \right)^2
$$

$$
\frac{GM}{r} = \frac{4\pi^2 r^2}{T^2}
$$

Multiply both sides by $T^2 r$:

$$
GM T^2 = 4 \pi^2 r^3
$$

#### Final Form:

$$
T^2 = \frac{4 \pi^2}{GM} r^3
$$

---

### Astronomical Implications

- **Determining Masses**: By observing $T$ and $r$, astronomers can estimate the mass $M$ of the central object.
- **Distance Measurement**: If the mass is known, this law allows the calculation of the orbital radius from the period.
- **Planetary Systems**: It confirms that outer planets in our Solar System have longer periods and larger orbital radii.

---

## Real-World Examples

#### Example 1: The Moon's Orbit

- Orbital radius $r \approx$ 384,400 km  
- Period $T \approx$ 27.3 days

Using Kepler's Law, this fits well with Earth's mass $5.972 \times 10^{24}$ kg.

#### Example 2: Planetary Orbits

- Mars $(T = 687$ days, $r = 1.52$ AU)  
- Jupiter $(T = 11.86$ years, $r = 5.2$ AU)

The ratio $\frac{T^2}{r^3}$ remains nearly constant, verifying Kepler's Third Law.

---

## Computational Model (Python)

We'll simulate bodies in circular orbits and verify $T^2 \propto r^3$.

<pre><code class="language-python">import numpy as np
import matplotlib.pyplot as plt

G = 6.67430e-11  # gravitational constant
\(M\) = 1.989e30     # mass of the Sun (kg)

# Radii in meters (e.g., 1 AU to 10 AU)
radii = np.linspace(1.5e11, 7.5e11, 10)
periods = []

for r in radii:
    T = 2 * np.pi * np.sqrt(r**3 / (G * \(M\)))
    periods.append(T)

radii_au = radii / 1.496e11
periods_yr = np.array(periods) / (60 * 60 * 24 * 365.25)

# Plot T^2 vs r^3
plt.figure(figsize=(8,5))
plt.plot(radii_au**3, periods_yr**2, 'o-', label=r'$T^2 \propto r^3$')
plt.xlabel('Orbital Radius Cubed (AU^3)')
plt.ylabel('Orbital Period Squared (years^2)')
plt.title("Verification of Kepler's Third Law")
plt.grid(True)
plt.legend()
plt.show()
</code></pre>

![image](https://github.com/user-attachments/assets/20ffccf1-100a-429f-b032-b3537b74be7f)

#### Graphical Representation

The graph plots $T^2$ against $r^3$, and the linearity confirms the theoretical relationship. Each point corresponds to a simulated orbit at a different radius.

---

### Extension to Elliptical Orbits

Kepler’s Third Law also applies to elliptical orbits when using the semi-major axis $a$ in place of $r$. The same relationship holds:

$$
T^2 \propto a^3
$$

This is crucial in modeling real planetary orbits, which are slightly elliptical rather than perfectly circular.

---

## Conclusion

The relationship $T^2 \propto a^3$ derived from Newtonian mechanics is a cornerstone of orbital mechanics. It allows astronomers to understand and predict the motions of celestial bodies with high precision.

Whether applied to moons, planets, or artificial satellites, this principle remains a vital tool in both theoretical and applied astrophysics. The computational model and real-world examples strongly support the validity and utility of Kepler's Third Law.
