# fourier-series-week3
# Week 3: Some Fourier Series | Seasons of Code - AnimAI Project

import numpy as np
import matplotlib.pyplot as plt
from ipywidgets import interact

# Square wave function
def square_wave(t, T):
    return np.where((t % T) < (T / 2), 1, -1)

# Fourier Series approximation for square wave
def fourier_series_square_wave(t, T, n_terms):
    result = np.zeros_like(t)
    for n in range(1, 2 * n_terms, 2):  # odd harmonics only
        result += (1 / n) * np.sin(2 * np.pi * n * t / T)
    return (4 / np.pi) * result

# Plotting the Fourier Series approximation against the true square wave
def plot_fourier_series(n_terms):
    T = 1e-3  # 1 ms period
    t = np.linspace(0, 2 * T, 1000)
    sq = square_wave(t, T)
    approx = fourier_series_square_wave(t, T, n_terms)
    
    plt.figure(figsize=(10, 4))
    plt.plot(t * 1e3, sq, label='Square Wave')
    plt.plot(t * 1e3, approx, label=f'Fourier Approx. (n={n_terms})')
    plt.title('Fourier Series Approximation of Square Wave')
    plt.xlabel('Time (ms)')
    plt.ylabel('Amplitude')
    plt.grid(True)
    plt.legend()
    plt.tight_layout()
    plt.show()

# Interactive widget to visualize different n_terms
interact(plot_fourier_series, n_terms=(1, 50))

"""
Concepts Covered:

1. Fourier Series:
   - Periodic signals like square waves can be expressed as infinite sums of sine and cosine terms.
   - Only odd harmonics are used in square wave expansion.
   - Each term improves approximation of the signal.

2. Fourier Transform:
   - Generalization of Fourier Series for non-periodic signals.
   - Helps in understanding frequency components of a signal.

3. Laplace vs. Fourier:
   - Laplace Transform: For solving differential equations, focuses on causality.
   - Fourier Transform: For analyzing signals, especially frequency content.

Use Cases:
- Animation smoothing
- Machine learning on temporal data
- Signal filtering and compression

Resources:
- 3Blue1Brown Fourier Series Video: https://www.youtube.com/watch?v=r6sGWTCMz2k&t=1109s
- Fourier Transform Visual Explanation: https://www.youtube.com/watch?v=spUNpyF58BY&t=513s
"""

