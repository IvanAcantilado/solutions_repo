# Estimating π Using Monte Carlo Methods

**Monte Carlo simulations** are a powerful class of computational techniques that use randomness to solve problems or estimate values. One particularly elegant application is the estimation of $\pi$ through geometric probability. By randomly generating points within a square and observing how many fall inside an inscribed circle, we can approximate $\pi$ in an intuitive and visually engaging way.  
This approach bridges key ideas from probability, geometry, and numerical computation—offering not only a practical example of Monte Carlo methods but also a foundation for understanding how randomness is used to tackle complex problems in physics, finance, and computer science.

## Theoretical Foundation

**Monte Carlo methods** allow us to estimate $\pi$ by leveraging geometric probability. By comparing the number of random points that fall inside a unit circle to the total number of points in the surrounding square, we can derive an estimate for $\pi$:

- The unit circle is inscribed in a square with side length 2 (from −1 to 1 in both $x$ and $y$).
- The area of the square is 4.
- The area of the unit circle is $\pi$.
- Therefore, the ratio of the areas is $\pi / 4$.

This leads to the estimation formula:

$$
\pi \approx 4 \times \left( \frac{\text{Points inside the circle}}{\text{Total points}} \right)
$$

We estimate $\pi$ using the area ratio of a unit circle inscribed in a square:

- The area of a square with side length 2 (from −1 to 1) is $A_{\text{square}} = 2^2 = 4$
- The area of the unit circle is $A_{\text{circle}} = \pi r^2 = \pi(1)^2 = \pi$

By generating points uniformly within the square, the probability $P$ that a point falls inside the circle is:

$$
A_{\text{square}} = 2^2 = 4
$$

Rearranging gives us the current formula.

## Simulation and Visualization

![image](https://github.com/user-attachments/assets/d74b1f09-e08b-441d-b2c6-446f4fb5cf03)

The **circle-based Monte Carlo method** is a straightforward yet powerful technique to estimate $\pi$. By generating random points within a square that bounds a unit circle, we determine whether each point lies inside the circle based on the equation $x^2 + y^2 \leq 1$. The simulation’s effectiveness hinges on the law of large numbers—as the number of random samples increases, the estimation of $\pi$ becomes more accurate.

The visualization plays a crucial role in reinforcing the concept:

- **Blue points** indicate those that fall inside the circle.
- **Red points** fall outside the circle but within the square.
- Overlaying a visible circle provides an intuitive understanding of the proportion being measured.

This method provides an interactive way to observe how randomness converges to a deterministic value. Additionally, the convergence plot ($\pi$ vs. number of iterations) helps quantify the estimate's stability as the number of samples grows.

![image](https://github.com/user-attachments/assets/1fba961f-83c3-42d5-8342-b84f7bcfa85e)

### Convergence and Efficiency

- The convergence rate of the estimate is proportional to $\frac{1}{\sqrt{N}}$, meaning that to gain one additional digit of accuracy, the number of samples must increase by a factor of 100.
- The computational cost scales linearly with the number of samples, but due to the simplicity of the calculations, the method is computationally efficient.
- However, achieving high precision requires a very large number of samples, making this method more educational than practical for computing $\pi$ to many decimal places.

<pre><code class="language-python">import numpy as np
import matplotlib.pyplot as plt

def monte_carlo_pi(num_points):
    x = np.random.uniform(-1, 1, num_points)
    y = np.random.uniform(-1, 1, num_points)
    
    inside = x**2 + y**2 <= 1
    pi_estimate = 4 * np.sum(inside) / num_points

    return pi_estimate, x, y, inside

def plot_simulation(x, y, inside, pi_estimate, num_points):
    fig, ax = plt.subplots(figsize=(6,6))
    ax.set_aspect('equal')
    ax.set_title(f'Monte Carlo π Estimate\nπ ≈ {pi_estimate:.6f} using {num_points} points')
    ax.scatter(x[inside], y[inside], color='blue', s=1, label='Inside Circle')
    ax.scatter(x[~inside], y[~inside], color='red', s=1, label='Outside Circle')
    ax.add_patch(plt.Circle((0, 0), 1, color='black', fill=False, linewidth=1))
    ax.set_xlim(-1, 1)
    ax.set_ylim(-1, 1)
    ax.legend()
    plt.grid(True)
    plt.show()

def plot_convergence(max_points, step=1000):
    estimates = []
    points_range = range(step, max_points + 1, step)
    for n in points_range:
        pi_estimate, _, _, _ = monte_carlo_pi(n)
        estimates.append(pi_estimate)

    plt.figure(figsize=(10, 5))
    plt.plot(points_range, estimates, label='Estimated π', color='green')
    plt.axhline(y=np.pi, color='black', linestyle='--', label='Actual π')
    plt.title('Convergence of π Estimate')
    plt.xlabel('Number of Points')
    plt.ylabel('Estimated π')
    plt.legend()
    plt.grid(True)
    plt.show()

# Example usage
num_points = 10000
pi_estimate, x, y, inside = monte_carlo_pi(num_points)
plot_simulation(x, y, inside, pi_estimate, num_points)

# Convergence plot
plot_convergence(50000, step=1000)
</code></pre>

## Buffon’s Needle

**Buffon’s Needle** is a famous problem where $\pi$ is estimated based on the probability of a needle crossing parallel lines:

- Floor has equally spaced parallel lines a distance $d$ apart.
- Needle of length $l \leq d$ is randomly dropped.
- The probability of the needle crossing a line relates to $\pi$.

The formula is:

$$
\pi \approx \frac{2 \cdot l \cdot N}{d \cdot C}
$$

Where:

- $l$: needle length  
- $d$: distance between lines  
- $N$: total throws  
- $C$: crossings  

The probability of a crossing is derived using integral geometry:

$$
P(\text{cross}) = \frac{2l}{d\pi}
$$

So the expected number of crossings in $N$ trials is:

$$
E[C] = N \cdot P = N \cdot \frac{2l}{d\pi}
$$

Rearranging to solve for $\pi$ gives us the formula.

![image](https://github.com/user-attachments/assets/ea42b977-d0ad-4747-82c6-31728c8fe00d)

**Buffon's Needle** simulation offers a fascinating probabilistic route to estimating $\pi$. Each trial involves randomly dropping a needle onto a surface marked with evenly spaced parallel lines.  
Whether the needle crosses a line depends on both its angle and its position relative to the lines. By aggregating a large number of such random drops, the probability of a crossing approximates a known function of $\pi$.

In the visualization:

- **Crossing needles** can be highlighted (e.g., in red), while non-crossing ones remain in a neutral color.
- Parallel lines and needle orientations help visually interpret why a crossing does or does not occur.

<pre><code class="language-python">import numpy as np
import matplotlib.pyplot as plt

# Parameters
needle_length = 1
line_spacing = 2
num_needles = 1000

# Generate random needle centers and angles
x_centers = np.random.uniform(-line_spacing / 2, line_spacing / 2, num_needles)
y_centers = np.random.uniform(0, 2, num_needles)
angles = np.random.uniform(0, np.pi, num_needles)

# Calculate needle endpoints
x1 = x_centers - (needle_length / 2) * np.cos(angles)
x2 = x_centers + (needle_length / 2) * np.cos(angles)
y1 = y_centers - (needle_length / 2) * np.sin(angles)
y2 = y_centers + (needle_length / 2) * np.sin(angles)

# Determine crossings
crosses = (np.floor(x1 / (line_spacing / 2)) != np.floor(x2 / (line_spacing / 2)))
num_crosses = np.sum(crosses)

# Estimate π
pi_estimate = (2 * needle_length * num_needles) / (line_spacing * num_crosses)

# Plot
plt.figure(figsize=(10, 6))
for i in range(num_needles):
    color = 'red' if crosses[i] else 'blue'
    plt.plot([x1[i], x2[i]], [y1[i], y2[i]], color=color, linewidth=0.5)

# Draw parallel lines
for i in range(-2, 3):
    plt.axvline(i * line_spacing / 2, color='gray', linestyle='--', linewidth=1)

# Aesthetics
plt.title(f"Buffon's Needle Simulation\nEstimated π ≈ {pi_estimate:.5f} (n={num_needles})", fontsize=14)
plt.xlabel("X Position (arbitrary units)")
</code></pre>

### Buffon's Method Comparison

**Buffon's method** converges more slowly than the circle-based method, especially when the number of needle crossings is low (leading to higher variance).  
Since the method relies on trigonometric calculations and a more complex crossing condition, it is computationally more intensive.  
It provides historical and conceptual value but is less practical for large-scale precision estimation compared to simpler Monte Carlo methods.

## Conclusion

Through this, we explored two classical **Monte Carlo methods** for estimating $\pi$—one based on geometric probability within a circle and another based on Buffon's Needle experiment. Both approaches demonstrated how randomness and statistical sampling can provide surprisingly accurate approximations of mathematical constants. While the circle-based method proved to be more computationally efficient and intuitive, Buffon’s Needle offered historical context and a richer understanding of geometric probability. Ultimately, these simulations highlight the power and elegance of probabilistic thinking in solving problems that are otherwise analytically intractable.
