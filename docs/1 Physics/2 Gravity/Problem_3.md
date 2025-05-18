# Trajectories of a Freely Released Payload Near Earth

# Orbital Motion Analysis

When a payload is released near Earth, its subsequent path is governed by the laws of gravitational motion. Depending on its velocity and direction at the moment of release, the payload may follow a **parabolic**, **elliptical**, **circular**, or **hyperbolic trajectory**. These paths are crucial to understanding outcomes such as **orbital insertion**, **reentry**, or **escape** from Earth's gravitational influence.

This presentation is an analytical and numerical study of these trajectories, supported by simulations that visualize the motion under various initial conditions.

---

## Theoretical Background

### Newton's Law of Universal Gravitation

The gravitational force exerted by Earth on a payload of mass $m$ is:

$$
F = \frac{G M_E m}{r^2}
$$

Where:

- $G = 6.67430 \times 10^{-11}$ N·m²/kg² (gravitational constant)
- $M_E = 5.972 \times 10^{24}$ kg (mass of Earth)
- $r$ = distance from Earth’s center

### Equation of Motion

The payload's acceleration $\vec{a}$ due to gravity is:

$$
\vec{a} = -\frac{G M_E}{r^3} \vec{r}
$$

This leads to a second-order differential equation for numerical integration.

### Orbital Shapes

The total mechanical energy $E$ of the system defines the trajectory type:

- Elliptical orbit: $E < 0$
- Parabolic escape: $E = 0$
- Hyperbolic escape: $E > 0$
- Circular orbit (special case of ellipse): constant radius

$$
E = \frac{1}{2}mv^2 - \frac{G M_E m}{r}
$$

---

## Numerical Analysis and Simulation

### Initial Conditions

The payload is released from a point $\vec{r}_0$ (typically above Earth’s surface) with a velocity $\vec{v}_0$. Varying $\vec{v}_0$ and its direction simulates different outcomes.

### Numerical Method: Runge-Kutta (RK4)

The fourth-order Runge-Kutta method is used to solve the equations of motion:

$$
\mathbf{r}_{n+1}, \mathbf{v}_{n+1} = f(\mathbf{r}_n, \mathbf{v}_n, \Delta t)
$$

A time step $\Delta t$ is chosen small enough to ensure accuracy.

### Python Implementation Overview

<pre><code class="language-python">def simulate_trajectory(r0, v0, t_max=6000, dt=1):
    r, v = r0, v0
    trajectory = [r.copy()]
    for _ in range(int(t_max/dt)):
        r, v = rk4(r, v, dt)
        trajectory.append(r.copy())
        if np.linalg.norm(r) < R_earth:
            break
    return np.array(trajectory)

# Example
r0 = np.array([R_earth + 200e3, 0])
v0 = np.array([0, 7800])
trajectory = simulate_trajectory(r0, v0)

plt.plot(trajectory[:,0], trajectory[:,1])
circle = plt.Circle((0, 0), R_earth, color='blue', alpha=0.3)
plt.gca().add_artist(circle)
plt.axis('equal')
plt.title("Payload Trajectory Near Earth")
plt.xlabel("x (m)")
plt.ylabel("y (m)")
plt.grid()
plt.show()
</code></pre>


![image](https://github.com/user-attachments/assets/48bc2f95-da9d-4f82-8796-0bd832154aff)

---

### Simulation Cases

<head>
  <b>Orbital Simulation</b>
  <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
</head>
<body>
  <h1>Orbital Simulation</h1>
  <div id="controls">
    <label for="speedSlider">Initial Speed (m/s): </label>
    <input type="range" id="speedSlider" min="3000" max="12000" step="100" value="3000">
    <span id="speedValue">3000</span>
  </div>
  <div id="plot" style="width:700px;height:700px;margin:auto;"></div>

  <script>
    const G = 6.67430e-11;
    const M = 5.972e24;
    const R_earth = 6371e3;
    const altitude = 200e3;
    const dt = 1.0;
    const t_max = 10000;

    function acceleration(r) {
      const norm = Math.sqrt(r[0]**2 + r[1]**2);
      return [-G * M * r[0] / norm**3, -G * M * r[1] / norm**3];
    }

    function rk4_step(r, v, dt) {
      const a1 = acceleration(r);
      const k1r = [v[0] * dt, v[1] * dt];
      const k1v = [a1[0] * dt, a1[1] * dt];

      const r2 = [r[0] + 0.5 * k1r[0], r[1] + 0.5 * k1r[1]];
      const v2 = [v[0] + 0.5 * k1v[0], v[1] + 0.5 * k1v[1]];
      const a2 = acceleration(r2);
      const k2r = [v2[0] * dt, v2[1] * dt];
      const k2v = [a2[0] * dt, a2[1] * dt];

      const r3 = [r[0] + 0.5 * k2r[0], r[1] + 0.5 * k2r[1]];
      const v3 = [v[0] + 0.5 * k2v[0], v[1] + 0.5 * k2v[1]];
      const a3 = acceleration(r3);
      const k3r = [v3[0] * dt, v3[1] * dt];
      const k3v = [a3[0] * dt, a3[1] * dt];

      const r4 = [r[0] + k3r[0], r[1] + k3r[1]];
      const v4 = [v[0] + k3v[0], v[1] + k3v[1]];
      const a4 = acceleration(r4);
      const k4r = [v4[0] * dt, v4[1] * dt];
      const k4v = [a4[0] * dt, a4[1] * dt];

      const r_next = [
        r[0] + (k1r[0] + 2*k2r[0] + 2*k3r[0] + k4r[0]) / 6,
        r[1] + (k1r[1] + 2*k2r[1] + 2*k3r[1] + k4r[1]) / 6
      ];
      const v_next = [
        v[0] + (k1v[0] + 2*k2v[0] + 2*k3v[0] + k4v[0]) / 6,
        v[1] + (k1v[1] + 2*k2v[1] + 2*k3v[1] + k4v[1]) / 6
      ];

      return [r_next, v_next];
    }

    function simulate(initial_speed) {
      let r = [R_earth + altitude, 0];
      let v = [0, initial_speed];
      let x = [], y = [];

      for (let t = 0; t < t_max; t += dt) {
        [r, v] = rk4_step(r, v, dt);
        if (Math.hypot(r[0], r[1]) < R_earth) break;
        x.push(r[0]);
        y.push(r[1]);
      }

      const earth = {
        type: "scatter",
        x: [0],
        y: [0],
        mode: "markers",
        marker: { size: R_earth / 100000, color: "blue", opacity: 0.5 },
        name: "Earth"
      };

      const orbit = {
        type: "scatter",
        x: x,
        y: y,
        mode: "lines",
        line: { color: "red" },
        name: `Speed: ${initial_speed} m/s`
      };

      const layout = {
        title: `Orbital Path for Initial Speed: ${initial_speed} m/s`,
        xaxis: { scaleanchor: "y", title: "x (m)" },
        yaxis: { title: "y (m)" },
        showlegend: true
      };

      Plotly.newPlot("plot", [earth, orbit], layout);
    }

    const slider = document.getElementById("speedSlider");
    const speedVal = document.getElementById("speedValue");
    slider.addEventListener("input", () => {
      const speed = parseFloat(slider.value);
      speedVal.textContent = speed;
      simulate(speed);
    });

    simulate(parseFloat(slider.value));
  </script>
</body>

**Case 1: Suborbital Reentry**
- Initial altitude: 200 km  
- Initial speed: 3,000 m/s (horizontal)  
- Result: Elliptical path intersecting Earth → reentry

**Case 2: Stable Orbit**
- Initial speed: ~7,800 m/s  
- Result: Circular orbit at 200 km altitude

**Case 3: Escape Trajectory**
- Initial speed: >11,200 m/s (escape velocity)  
- Result: Hyperbolic trajectory

---

## Orbital Insertion, Reentry, and Escape

### Orbital Insertion

A payload must achieve a tangential velocity of:

$$
v_c = \sqrt{\frac{G M_E}{r}}
$$

This ensures centripetal force equals gravitational pull, leading to a circular orbit.

### Reentry

If $v < v_c$, the trajectory is elliptical with perigee within Earth's atmosphere, causing atmospheric drag and reentry.

### Escape

If $v \geq v_{\text{esc}} = \sqrt{\frac{2 G M_E}{r}}$, the object escapes Earth's gravitational field.

---

## Real-World Applications

- **Satellite Deployment**: Accurate velocity ensures correct orbit.  
- **Space Mission Planning**: Trajectory types determine fuel needs and mission profiles.  
- **Planetary Exploration**: Gravity assists and escape trajectories are used to reach other planets.  

---

## Visualization Tool

The simulation tool plots trajectories using `matplotlib` or an interactive JavaScript plot (e.g., Plotly) to dynamically observe how initial speed affects the path.

![image](https://github.com/user-attachments/assets/0cc90d9e-dc15-4475-b3c9-d0d3359842d2)

---

## Conclusion

By applying fundamental physics and numerical modeling, we’ve shown how the trajectory of a released payload is determined by initial conditions. This study highlights critical concepts in spaceflight mechanics and offers a practical tool for visualizing and planning near-Earth missions.
