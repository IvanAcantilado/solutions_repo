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

![Uniform Magnetic Field](https://github.com/user-attachments/assets/d457b78b-a17b-48b6-a1fb-07c42e36993c)

- Expect circular motion (if velocity is perpendicular to $\vec{B}$) or **helical** (if there's a component along $\vec{B}$).
- Demonstrates cyclotron motion and introduces the concept of **Larmor radius** and **cyclotron frequency**.

![Uniform Magnetic Field](https://github.com/user-attachments/assets/09490a9e-0bfe-453c-a230-b6817ce9e175)

- Non-trivial motion—often helical with drift.
- Depending on vector orientation, the particle can accelerate, spiral, or follow curved paths.

![Crossed E B Fields](https://github.com/user-attachments/assets/f4eca2fb-2d5d-4719-85bf-36a253be53bb)

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

<head>
    <meta charset="UTF-8">
    <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
</head>
<body>
    <div id="sliders" class="slider-group"></div>
    <div id="plot" style="width: 100%; height: 80vh;"></div>

    <script>
        const sliderDefs = [
            { id: 'q', label: 'Charge (q)', min: -2, max: 2, step: 0.1, value: 1 },
            { id: 'm', label: 'Mass (m)', min: 0.1, max: 5, step: 0.1, value: 1 },
            { id: 'Ex', label: 'E_x', min: -2, max: 2, step: 0.1, value: 0 },
            { id: 'Ey', label: 'E_y', min: -2, max: 2, step: 0.1, value: 0 },
            { id: 'Ez', label: 'E_z', min: -2, max: 2, step: 0.1, value: 0 },
            { id: 'Bx', label: 'B_x', min: -2, max: 2, step: 0.1, value: 0 },
            { id: 'By', label: 'B_y', min: -2, max: 2, step: 0.1, value: 0 },
            { id: 'Bz', label: 'B_z', min: -2, max: 2, step: 0.1, value: 1 },
            { id: 'vx', label: 'v_x', min: -2, max: 2, step: 0.1, value: 1 },
            { id: 'vy', label: 'v_y', min: -2, max: 2, step: 0.1, value: 0 },
            { id: 'vz', label: 'v_z', min: -2, max: 2, step: 0.1, value: 0 }
        ];

        const sliders = {};
        const slidersDiv = document.getElementById('sliders');

        sliderDefs.forEach(def => {
            const wrapper = document.createElement('div');
            wrapper.className = 'slider';

            const label = document.createElement('label');
            label.innerText = def.label;

            const input = document.createElement('input');
            input.type = 'range';
            input.min = def.min;
            input.max = def.max;
            input.step = def.step;
            input.value = def.value;
            input.id = def.id;

            const valueDisplay = document.createElement('span');
            valueDisplay.innerText = ` ${input.value}`;

            input.oninput = () => {
                valueDisplay.innerText = ` ${input.value}`;
                plotTrajectory();  // update on slider change
            };

            wrapper.appendChild(label);
            wrapper.appendChild(input);
            wrapper.appendChild(valueDisplay);
            slidersDiv.appendChild(wrapper);

            sliders[def.id] = input;
        });

        function simulateParticle(q, m, E, B, v0, r0 = [0, 0, 0], dt = 0.01, steps = 1000) {
            let r = Array(steps).fill().map(() => [0, 0, 0]);
            let v = Array(steps).fill().map(() => [0, 0, 0]);
            r[0] = [...r0];
            v[0] = [...v0];

            const cross = (a, b) => [
                a[1] * b[2] - a[2] * b[1],
                a[2] * b[0] - a[0] * b[2],
                a[0] * b[1] - a[1] * b[0]
            ];

            for (let i = 1; i < steps; i++) {
                const crossVB = cross(v[i - 1], B);
                const F = E.map((Ei, j) => q * (Ei + crossVB[j]));
                const a = F.map(f => f / m);
                v[i] = v[i - 1].map((vi, j) => vi + a[j] * dt);
                r[i] = r[i - 1].map((ri, j) => ri + v[i][j] * dt);
            }

            return r;
        }

        function plotTrajectory() {
            const q = parseFloat(sliders.q.value);
            const m = parseFloat(sliders.m.value);
            const E = [parseFloat(sliders.Ex.value), parseFloat(sliders.Ey.value), parseFloat(sliders.Ez.value)];
            const B = [parseFloat(sliders.Bx.value), parseFloat(sliders.By.value), parseFloat(sliders.Bz.value)];
            const v0 = [parseFloat(sliders.vx.value), parseFloat(sliders.vy.value), parseFloat(sliders.vz.value)];

            const r = simulateParticle(q, m, E, B, v0);
            const x = r.map(p => p[0]);
            const y = r.map(p => p[1]);
            const z = r.map(p => p[2]);

            const trace = {
                x, y, z,
                type: 'scatter3d',
                mode: 'lines',
                name: 'Trajectory',
                line: { width: 4 }
            };

            const start = {
                x: [x[0]], y: [y[0]], z: [z[0]],
                type: 'scatter3d',
                mode: 'markers',
                marker: { size: 5, color: 'green' },
                name: 'Start'
            };

            const end = {
                x: [x[x.length - 1]], y: [y[y.length - 1]], z: [z[z.length - 1]],
                type: 'scatter3d',
                mode: 'markers',
                marker: { size: 5, color: 'red' },
                name: 'End'
            };

            const layout = {
                title: `Lorentz Force (q=${q}, m=${m})`,
                scene: {
                    xaxis: { title: 'X' },
                    yaxis: { title: 'Y' },
                    zaxis: { title: 'Z' }
                },
                margin: { l: 0, r: 0, t: 40, b: 0 }
            };

            Plotly.newPlot('plot', [trace, start, end], layout);
        }

        plotTrajectory(); // initial plot
    </script>
</body>



**Field Strengths ($\vec{E}, \vec{B}$)**

- **Stronger $\vec{B}$** → tighter spirals (smaller radius, faster cycles)  
- **Stronger $\vec{E}$** → more acceleration/drift  

**Initial Velocity ($\vec{v}_0$)**

- Controls direction and shape of trajectory  
- Component **perpendicular to $\vec{B}$** → circular motion  
- Component **parallel to $\vec{B}$** → helical motion  

**Charge ($q$) and Mass ($m$)**

- Affects acceleration:  
  $$ 
  \vec{a} = \frac{q}{m} \left( \vec{E} + \vec{v} \times \vec{B} \right) 
  $$
- Heavier particles → move more slowly, spiral wider  

---

**Suggested Variations to Try**

| Parameter              | Try Changing From              | Expected Effect                  |
|------------------------|-------------------------------|----------------------------------|
| **$\vec{B}$**          | $[0, 0, 1] \rightarrow [0, 0, 2]$ | Tighter spirals               |
| **$\vec{E}$**          | $[0.5, 0, 0] \rightarrow [0, 0, 1]$ | Helical → Accelerated spiral |
| **$\vec{v}_0$**        | $[1, 0, 0] \rightarrow [0, 0, 1]$ | Circular → Linear motion     |
| **$q$**                | $1 \rightarrow -1$               | Reverse rotation direction       |
| **$m$**                | $1 \rightarrow 0.1$              | Faster spirals (lighter particle)|

By varying field strengths, initial velocities, charge, and mass, we observe:

- Circular or helical motion under **magnetic fields**  
- Acceleration or drift under **electric fields**  
- Trajectory shape and speed heavily influenced by $\frac{q}{m}$  
- **Direction reversal** when charge flips

## Task #4: Visualization

Show particle motion under various field configurations using **clear, labeled plots**. Emphasize key features such as:

- **Larmor radius**: Radius of circular motion in a magnetic field  
- **Drift velocity**: Constant velocity **perpendicular to both** $\vec{E}$ and $\vec{B}$

---


**Larmor Radius**  
The radius of circular motion in a magnetic field:

$$
r_L = \frac{m v_\perp}{|q| B}
$$

- $v_\perp$: component of velocity perpendicular to $\vec{B}$  
- $B$: magnetic field magnitude  
- $q$: particle charge  
- $m$: particle mass

**Drift Velocity** (for crossed $\vec{E} \times \vec{B}$ fields):

$$
\vec{v}_d = \frac{\vec{E} \times \vec{B}}{B^2}
$$

- This velocity is **independent of charge and mass**  
- Direction is **perpendicular** to both $\vec{E}$ and $\vec{B}$

---

**2D Plot** (e.g., x-y plane):

![2D View Crossed E B Fields](https://github.com/user-attachments/assets/6f708a64-7638-4a5d-ad6c-4105bcf76857)

- Shows **circular motion** plus **drift**
- **Larmor radius** indicated as a **dashed circle**
- **Drift velocity** shown with an **arrow**

**3D Plot**:

![3D View Trajectory under E B Fields](https://github.com/user-attachments/assets/8637e599-0e3c-48cb-b029-6f0cd18c6bd4)

- Displays **full trajectory** (helical or linear drift)  
- Vector arrows for $\vec{E}$ and $\vec{B}$ for reference  
- Visualizes how fields influence particle path in space

**Visualization Summary**

- A charged particle follows a **helical or drift path** depending on the field configuration  
- **Larmor radius** determines the size of the circular motion in a magnetic field  
- In crossed $\vec{E} \times \vec{B}$ fields, the particle **drifts at constant speed perpendicular** to both fields  
- These visuals help explain **energy transfer and particle control** in devices like **mass spectrometers** and **plasma traps**

