# Exploring the Central Limit Theorem through simulations

The **Central Limit Theorem (CLT)** is a foundational principle in probability and statistics. It states that as the size of a sample increases, the distribution of the sample mean tends to approximate a normal distribution, no matter the shape of the original population distribution.  
This remarkable property enables statisticians to make inferences about population parameters even when the data are not normally distributed.

### Simulating Sampling Distributions

We'll generate large populations using three types of distributions:  
To simulate the Central Limit Theorem, we must first create large datasets (populations) from which we can draw random samples.

![Uniform population](https://i.ibb.co/vxzTjht6/Uniform-population.png)

The **Central Limit Theorem (CLT)** shows that no matter the original distribution (here, uniform), as the sample size increases, the sampling distribution of the sample mean approximates a normal distribution.

![Exponential population](https://i.ibb.co/HfH4Mf9s/Exponential-population.png)

Despite the exponential distribution being **right-skewed**, the sample means normalize as the sample size increases, illustrating the **CLT's** power to make sampling distributions normal even from skewed populations.

![Binomial population](https://i.ibb.co/35JgDc2d/Binomial-population.png)

The **CLT** transforms the **discrete** binomial distribution into a normal distribution as the sample size increases, allowing for easier statistical analysis.

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

![Sampling Distribution](https://i.ibb.co/BHMRQK68/Sampling-Distribution-of-the-Mean-for-Different-Sample-Sizes.png)

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
