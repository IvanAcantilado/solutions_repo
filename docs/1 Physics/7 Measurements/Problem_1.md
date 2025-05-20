# Measuring Earth's Gravitational Acceleration with a Pendulum

## Theoretical Background

#### Equation for a simple pendulum:

$$
T = 2\pi \sqrt{\frac{L}{g}}
$$

Rearranged to solve for $g$:

$$
g = \frac{4 \pi^2 L}{T^2}
$$

Where:

- $T$: Period of the pendulum (seconds)  
- $L$: Length from pivot to the center of mass (meters)  
- $g$: Acceleration due to gravity (m/s²)

### Pendulum Experiment Data

| L (m) | ΔL (m) | T₁₀ (s) | σT (s) | ΔT (s) | g (m/s²) | Δg (m/s²) |
|-------|--------|----------|--------|---------|-----------|-------------|
| 1.000 | 0.0005 | 20.12   | 0.027 | 0.0085 | 9.75     | 0.07        |
| 1.000 | 0.0005 | 20.15   | 0.031 | 0.0098 | 9.72     | 0.08        |
| 1.500 | 0.0005 | 25.18   | 0.033 | 0.0104 | 9.34     | 0.06        |
| 1.500 | 0.0005 | 25.14   | 0.029 | 0.0091 | 9.37     | 0.05        |
| 1.200 | 0.0005 | 22.14   | 0.027 | 0.0085 | 9.66     | 0.07        |
| 1.200 | 0.0005 | 22.19   | 0.030 | 0.0094 | 9.62     | 0.08        |
| 1.800 | 0.0005 | 27.35   | 0.027 | 0.0085 | 9.50     | 0.08        |
| 1.800 | 0.0005 | 27.31   | 0.029 | 0.0091 | 9.53     | 0.07        |
| 2.000 | 0.0005 | 29.25   | 0.031 | 0.0098 | 9.23     | 0.06        |
| 2.000 | 0.0005 | 29.28   | 0.027 | 0.0085 | 9.21     | 0.07        |

---

## Calculations

#### Determine the Period of One Oscillation

The period $T$ of a single oscillation is calculated by dividing the mean time for 10 oscillations by 10:

$$
T = \frac{T_{10}}{10}
$$

#### Determine the Uncertainty in the Period

The uncertainty in the period, $\Delta T$, is obtained by dividing the uncertainty in the mean time for 10 oscillations by 10:

$$
\Delta T = \frac{\Delta T_{10}}{10}
$$

*These values of $T$ and $\Delta T$ will be used in the next step to compute the gravitational acceleration and analyze uncertainty propagation.*

#### Determination of Gravitational Acceleration and Uncertainty Analysis

The acceleration due to gravity, $g$, is calculated using the formula:

$$
g = \frac{4\pi^2 L}{T^2}
$$

Where:

- $L$: Length of the pendulum (in meters)  
- $T$: Period of one oscillation (in seconds)

#### Propagation of Uncertainties

To determine the uncertainty in $g$, denoted $\Delta g$, we use the standard propagation of error formula. Since $g$ depends on both $L$ and $T$:

$$
\frac{\Delta g}{g} = \sqrt{ \left( \frac{\Delta L}{L} \right)^2 + \left( 2 \cdot \frac{\Delta T}{T} \right)^2 }
$$

Therefore, the absolute uncertainty in $g$ is:

$$
\Delta g = g \cdot \sqrt{ \left( \frac{\Delta L}{L} \right)^2 + \left( 2 \cdot \frac{\Delta T}{T} \right)^2 }
$$

Final result:

$$
g = (\text{value} \pm \Delta g)\ \text{m/s}^2
$$

---

## Analysis

### Comparison with Standard Gravitational Acceleration

The standard accepted value for gravitational acceleration at Earth's surface is:

$$
g_{\text{standard}} = 9.81\ \text{m/s}^2
$$

Compare your experimentally determined value of $g$ with this standard by calculating the percent error:

$$
\text{Percent Error} = \left| \frac{g_{\text{measured}} - g_{\text{standard}}}{g_{\text{standard}}} \right| \times 100\%
$$

If the measured value lies within the range $g_{\text{standard}} \pm \Delta g$, the result is considered consistent within experimental uncertainty.

If not, consider possible sources of discrepancy, such as:

- Reaction time delays in manual timing  
- Inaccurate length measurement (e.g., not measuring to the center of mass)  
- Air resistance or large angular displacements violating the small-angle approximation  
- Non-rigid support allowing unwanted motion

### Effect of Measurement Resolution on $\Delta L$

The resolution of the measuring tool (e.g., ruler) directly determines the uncertainty in length, $\Delta L$. For example, a 1 mm resolution yields:

$$
\Delta L = \pm 0.5\,\text{mm}
$$

This propagates into the final value of $g$, though it has a smaller effect compared to timing uncertainty due to $g$’s direct (not squared) dependence on $L$.

### Variability in Timing and Its Impact on $\Delta T$

Human reaction time introduces variability in timing measurements. Since $T$ appears squared in the formula for $g$, even small uncertainties can significantly affect the result. Repeated measurements and statistical analysis help mitigate this impact.

### Assumptions and Experimental Limitations

- **Small-Angle Approximation**: Valid only for angles <15°. Larger angles introduce systematic errors.  
- **Negligible Air Resistance**: Assumes damping is insignificant.  
- **Rigid Support and Frictionless Pivot**: Idealized conditions that may not fully apply.  
- **Point Mass and Massless String**: Simplified model; real systems deviate slightly.

---

## Uncertainty and Their Impact

### Human Error

Introduces both random and systematic uncertainties. These increase $\sigma_T$ and consequently $\Delta T$, which leads to greater $\Delta g$.

### Resolution of Measuring Instruments

Directly affects uncertainties in $L$ and $T_{10}$, propagating through to $T$ and $g$.

### Timing

Since $g$ depends on $T^2$, timing errors have an amplified impact on the uncertainty in $g$.
