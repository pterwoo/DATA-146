### DATA 202 Exam 1 Problem 3
#### Peter Woo
#### March 3, 2021



| Vocabulary|Definition|Source|
|---|---|---|
|Runtime|Software/instructions that are executed while program is running|e.Jamese.James . 2010. “What Is ‘Runtime’?” Stack Overflow. https://stackoverflow.com/questions/3900549/what-is-runtime (March 1, 2021).    |
|Kernel|The core of an operating system. Responsible for memory and task management, etc.|“What Is Kernel in Operating System and What Are the Various Types of Kernel?” 2019. AfterAcademy. https://afteracademy.com/blog/what-is-kernel-in-operating-system-and-what-are-the-various-types-of-kernel (March 1, 2021).  |   
|Sum of squares|Variance of a sample|   |   
|Degrees of freedom|Maximum number of logically independent values   |   |
|Random Variable|A function defined on a sample space $\Omega$|   |   
|Real Numbers|Numbers that are not imaginary   |   |   
|Observation|$\omega \in \Omega$ and is a real number   |   |
|Stochastic process|Collection of random variables where all random variables are defined on the same sample space   |   |   
|Time|A measure for sample space|   |   
|Time Series|The stochastic process where the sample space represents time   |   |
|Continuous|Real numbers in the sample space T   |   |   
|Discrete|   |   |   
|Realization|The set of values that result from the occurrence of some observed event   |   |
|Ensemble|Collection of all realizations   |   |   
|Expected value|Represented by the ensemble mean   |   |   
|Ordinate|The vertical axis   |   |
|Abscissa|The horizontal axis  |   |   
|Covariance|Joint variability of two random variables	   |   |   
|Autocovariance|When covariance is within the same time series, represented by the following equation:$$\gamma(t_1, t_2) = E\{[X(t_1) - \mu(t_1)][X(t_2) - \mu(t_2)]\}$$|   |
|Autocorrelation|Degree of correlation of the same variables between two successive time intervals|“Autocorrelation - Overview, How It Works, and Tests.” 2015. Corporate Finance Institute. https://corporatefinanceinstitute.com/resources/knowledge/other/autocorrelation/ (March 1, 2021).    |   
|Stationarity|State of “statistical equilibrium” (i.e., the basic behavior of a stationary time series does not change in time)   |   |   
|Ergodic|A time series where ensemble averages are consistent with those from a single realization|   |
|Strictly stationary|A time series where: for any $t_1, t_2 \in T$, the distributions of $X(t_1$) and $X(t_2)$ must also be the same and all bivariate distributions $\{X(t), X(t+h)\}$ must be the same for all values of $h$|   |   
|Covariance stationarity|Also known as weak stationarity, where: $E[X(t)] = \mu$ and is constant for all values of $t$ <br /> * $\mathrm{Var}[X(t)] = \sigma^2 < \infty$ (i.e., is finite for all $t$) <br /> * $\gamma(t_1, t_2)$ depends only on $t_2  - t_1$ (also known as the lag or $h$) <br /> * $\gamma(h)$ is a semi-definite process (i.e., it's positive or zero for all scalar multiples)|   |   
|Cauchy-schwarz inequality| $\vert\gamma(h)\vert \le \gamma(0)$ for all $h$   |   |
|Sample autocovariance function|The estimate from a single realization that best preserves the overall pattern of the autocovariance function   |   |   
|Sample autocorrelation function|The natural estimator for the autocorrelation function   |   |   
|Time domain|Analysis of time series with respect to time   |   |
|Frequency domain|Analysis of time series with respect to frequency   |   |   
|Hertz|A measure of frequency. Number of cycles per second   |   |   
|Aperiodic|A function that has no period    |   |
|Spectral density|The Fourier transform of the autocorrelation. Relevant information in the autocorrelation is more readily conveyed through spectral density rather than the autocorrelation when determining frequency.   |   |   
|Periodogram|Fundamental tool of spectral analysis, based on squared correlation between the time series and the sin/cosine waves of frequency and displays the same information as the autocovariance function. Used as an estimate of the spectral density of a signal   |   |   
|Decibel|Standard unit for measuring acoustical energy   |   |
|Parzen window|A non-parametric way to estimate the probability density function of a random variable. Smoothes the spectrum    |“Kernel Density Estimation.” 2021. Wikipedia. https://en.wikipedia.org/wiki/Kernel_density_estimation (March 1, 2021).   |   
|AR(1)|first order autoregressive process where the dependent variable , $X_t$, is equal to 0.9 times its previous value plus some Gaussian white noise, $a_t$, with zero mean and unit variance.   |   |   
