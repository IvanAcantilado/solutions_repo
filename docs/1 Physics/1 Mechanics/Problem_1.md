# Investigating the Range as a Function of the Angle of Projection
This investigation examines how the range of a projectile is affected by the angle at which it is launched. By varying the angle of projection and measuring the resulting horizontal distance, we aim to identify patterns in the data and determine the angle that produces the maximum range.

## Theoretical Foundation
Projectile motion describes the motion of an object under the influence of gravity, neglecting air resistance. The object follows a parabolic trajectory determined by its initial conditions: initial speed 𝑣𝜃, angle of projection 𝜃, and gravitational acceleration 𝑔.

<b>Equations of Motion:</b><br />
We start with Newton's Second Law:
<p>$$ F = m \\a $$</p>
For projectile motion, the only force acting is gravity. The horizontal and vertical components of motion can be treated separately:<br />
<ul><li>Horizontal: constant velocity motion</li>
<li>Vertical: uniformly accelerated motion</li></ul>
Let:<br />
<ul><li>𝑣𝜃: initial speed</li>
<li>𝜃: angle of projection</li>
<li>𝑔: acceleration due to gravity</li></ul>
<b>Horizontal motion:</b><br />
<p>$$ x(t) = v_0 \cdot \cos(\theta) \cdot t $$</p>
<b>Vertical motion:</b><br />
<p>$$ y(t) = v_0 \cdot \sin(\theta) \cdot t - \frac{1}{2} g t^2 $$</p>
## Time of Flight
The projectile lands when <b>𝑦(𝑡)=<i>0</i></b>. Solving for <b>𝑡</b>:<br />
<p>$$ 0 = v_0 \cdot \sin(\theta) \cdot t - \frac{1}{2} g t^2 $$</p>
Simplifying this, we get:<br />
<p>$$ t(v_0 \cdot \sin(\theta) - \frac{1}{2} g t) = 0 $$</p>
Ignoring the <b>𝑡=<i>0</i></b> solution:<br />
<p>$$ t = \frac{2v_0 \sin(\theta)}{g} $$</p>
<b>Range of the Projectile</b><br />
Substitute time of flight into the horizontal motion equation:<br />
<p>$$ R = x(t) = v_0 \cdot \cos(\theta) \cdot \frac{g}{2v_0 \sin(\theta)} $$</p>
Simplifying, we get the final form of the range equation:<br />
<p>$$ R = \frac{v_0^2 \sin(2\theta)}{g} $$</p>
## Analysis of the Range
<b>Influence of Angle</b><br />
<p>As shown by the formula <span class="arithmatex">$R = \frac{v_0^2 \sin(2\theta)}{g}$</span>, the range follows a sine curve with respect to <span class="arithmatex">$2\theta$</span>, peaking at <span class="arithmatex">$45^\circ$</span>.</p>
