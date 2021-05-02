# Applied Time Series Analysis - Block 3 Notes

## Detrending Time Series
- Using R's 
- Using the `stl` function
  - Seasonal decomposition of time series using Loess modeling
  - Extracts the seasonal component 

## Linear Filters
- What is the Butterworth filter and explain the inputs to the `butterworth.wge` function
  - The Butterworth filter is a common filter used by scientists and engineers that was developed in the 1970s and updated in 1997.
  - Can be used in several different types of processes
  - *What happens when you change the value of N?*
    - When the n-value is small, the impact on the spectral density is low. Increasing the value of N will sharpen the filter. 
  - *What is the difference between "low pass," "high pass," "band pass" and "band stop" filter types?*
    - Low: low frequencies pass through the filter more or less unchanged, while filtering our high frequencies
    - High: high frequencies pass through the filter and the low frequencies are filtered out 
    - Pass: also referred to as "band-pass", takes two values and keeps everything inbetween them, filtering out everything higher or lower. 
    - Stop: also referred to as "band-stop" or "notch," stop frequencies in a certain band (opposite of band-pass)
  - the inputs to the `butterworth.wge` function is as follows: `butterworth.wge(x, order, type, cutoff,plot=TRUE)`
    - `x` : realization to be filtered
    - `order` : order of the Butterworth filter
    - `type` : Either "low", "high", "stop", or "pass"
    - `cutoff`: For "low" and "high": cutoff is a real number, and for "stop" and "band": cutoff is a 2-component vector 
    - `plot`: If plot = TRUE then the plots of the original and filtered data are produced. 
    
