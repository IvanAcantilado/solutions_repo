# Exploring the Central Limit Theorem through simulations

The **Central Limit Theorem (CLT)** is a foundational principle in probability and statistics. It states that as the size of a sample increases, the distribution of the sample mean tends to approximate a normal distribution, no matter the shape of the original population distribution.  
This remarkable property enables statisticians to make inferences about population parameters even when the data are not normally distributed.

### Simulating Sampling Distributions

We'll generate large populations using three types of distributions:  
To simulate the Central Limit Theorem, we must first create large datasets (populations) from which we can draw random samples.

![image](https://github.com/user-attachments/assets/7d39b39f-bd1f-4839-b1ca-5c16b9284f9c)

The **Central Limit Theorem (CLT)** shows that no matter the original distribution (here, uniform), as the sample size increases, the sampling distribution of the sample mean approximates a normal distribution.

![image](https://github.com/user-attachments/assets/b6e44cd8-60dc-4dc2-a585-4266122a027c)

Despite the exponential distribution being **right-skewed**, the sample means normalize as the sample size increases, illustrating the **CLT's** power to make sampling distributions normal even from skewed populations.

![image](https://github.com/user-attachments/assets/4daddfb7-9bee-4366-8ade-0c982dd7f095)

The **CLT** transforms the **discrete** binomial distribution into a normal distribution as the sample size increases, allowing for easier statistical analysis.

<pre><code>
import matplotlib.pyplot as plt
import seaborn as sns

# For reproducibility
np.random.seed(42)

# Step 1: Define population size
N = 100000  # A large sample to represent the population

# Step 2: Generate different types of populations

# 1. Uniform distribution (values between 0 and 1)
uniform_pop = np.random.uniform(low=0, high=1, size=N)

# 2. Exponential distribution (scale = 1)
exponential_pop = np.random.exponential(scale=1.0, size=N)

# 3. Binomial distribution (n=10 trials, p=0.5 success probability)
binomial_pop = np.random.binomial(n=10, p=0.5, size=N)

# Step 3: Create a dictionary for easier iteration
populations = {
    'Uniform': uniform_pop,
    'Exponential': exponential_pop,
    'Binomial': binomial_pop
}

# Step 4: Set the style and color palette
sns.set(style="whitegrid")  # Sets background style for better readability
palette = sns.color_palette("viridis", as_cmap=True)  # Smooth color map for better aesthetics

# Step 5: Plot each population distribution and save individually
for i, (name, data) in enumerate(populations.items()):
    # Create the plot for each population
    plt.figure(figsize=(8, 6))  # Adjust figure size
    sns.histplot(data, bins=50, stat='density', color=palette(i / 3), linewidth=1.5)
    
    # Customize the plot
    plt.title(f'{name} Population', fontsize=14, weight='bold')
    plt.xlabel('Value', fontsize=12)
    plt.ylabel('Density', fontsize=12)
    plt.grid(True, linestyle='--', alpha=0.6)

    # Save the plot to a PNG file
    plt.tight_layout()
    plt.savefig(f"{name}_population.png")  # Save each plot as a separate file
    plt.close()  # Close the figure to prevent overlap in the next plot

print("Plots saved successfully!")
</code></pre>

### Sampling and Visualization

We will take random samples from the population and compute the sample mean for each sample.  
We'll repeat this process multiple times to create a sampling distribution for each sample size.  
We'll plot histograms of the sample means and observe how the sampling distribution approaches a normal distribution as the sample size increases.  
We will calculate the mean (average) of that sample by summing the values and dividing by the number of items in the sample.

$$
\bar{x} = \frac{1}{n} \sum_{i=1}^{n} x_i
$$

- $ \bar{x} $ is the sample mean  
- $ n $ is the sample size  
- $ x_i $ are the individual data values in the sample  

![image](https://github.com/user-attachments/assets/343705a6-71a4-43bf-9957-97813e859bd1)

The plot shows **sampling distributions** of the mean for different **sample sizes** (5, 10, 30, 50) drawn from the same normal population.  
Each colored histogram represents the distribution of **1,000 sample means**, where:
- A sample of a given size is randomly taken from the population.
- The mean of that sample is computed.
- This process is repeated 1,000 times to build the histogram.

This demonstrates the **Central Limit Theorem**: as sample size increases, the sampling distribution of the mean becomes more **normal and less variable**, even when sampling from the same population.

### Parameter Exploration

**Shape of the Original Distribution**  
- **Normal population**: The sampling distribution of the mean is normal regardless of sample size.  
- **Skewed** or non-normal populations (e.g., exponential, uniform):  
  - For **small sample** sizes, the sampling distribution retains the skewness or shape of the population.  
  - As **sample size increases**, the sampling distribution becomes more **normal**, even if the original distribution is not.

**Sample Size**  
- **Larger samples** (e.g., $n=30$, $n=50$) lead to:  
  - Faster convergence to normality.  
  - Smaller standard error (i.e., narrower distribution).  
- **Smaller samples** (e.g., $n=5$) show more variability and reflect the original population more closely.

**Population Variance**  
- The **spread (standard deviation)** of the sampling distribution of the mean is:  
  $$
  \text{Standard Error} = \frac{\sigma}{\sqrt{n}}
  $$  
  - $ \sigma $: population standard deviation  
  - $ n $: sample size  

**Higher variance** in the population = wider sampling distributions, even as the shape becomes normal.

### Practical Applications

The **Central Limit Theorem (CLT)** is one of the most powerful concepts in statistics, with broad **practical applications across many fields**. Here's how it plays a vital role in real-world scenarios:

1. **Estimating Population Parameters**  
   - In surveys, medical trials, and experiments, we rarely have access to entire populations.  
   - **CLT allows us to use sample means** (from random samples) to estimate the population mean with known accuracy.  
   - It also underpins confidence intervals and hypothesis testing by assuming the sampling distribution is approximately normal when the sample size is large enough.

2. **Quality Control in Manufacturing**  
   - In industries like electronics or pharmaceuticals, it's impractical to test every product.  
   - Manufacturers take **random samples** from each production batch and use sample means to monitor consistency and detect defects.  
   - The CLT justifies the use of control charts (e.g., X̄ charts), because the distribution of **sample means becomes normal**, allowing for predictable control limits.

3. **Predicting Outcomes in Financial Models**  
   - Finance often deals with returns from stocks, portfolios, or investments — all subject to variability.  
   - When modeling **average returns over time or over different assets**, CLT supports the assumption that the **average return will be normally distributed**, making statistical models more reliable.  
   - This is crucial for **risk assessment**, **option pricing**, and **forecasting**.
