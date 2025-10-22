---
title: Analyze Signal Spectrum
description: Perform frequency domain analysis using FFT and spectral techniques
tags: [matlab, signal-processing, fft, spectral-analysis, frequency-domain, psd]
release: Core FFT in base MATLAB, advanced features require Signal Processing Toolbox
notes:
---

# Analyze Signal Spectrum

Perform frequency domain analysis of signals using FFT and spectral analysis techniques.

## Metadata

- **Tags:** `matlab` `signal-processing` `fft` `spectral-analysis` `frequency-domain` `psd`
- **MATLAB Release:** Core FFT functions in base MATLAB, advanced features require Signal Processing Toolbox
- **Required Toolboxes:** None (base MATLAB), Signal Processing Toolbox for advanced features

## The Prompt

```text
Create MATLAB code to analyze the frequency spectrum of a signal:

Requirements:
1. Load or generate the signal
2. Compute FFT with proper scaling
3. Calculate power spectral density
4. Create frequency vector with correct units
5. Plot time-domain signal
6. Plot magnitude spectrum (linear and dB)
7. Plot power spectral density
8. Identify dominant frequencies
9. Add proper labels, titles, and units to all plots

Signal details: [DESCRIBE SIGNAL]
Sampling rate: [VALUE] Hz
Expected frequency components: [FREQUENCIES]
```

## Usage Tips

1. **Describe signal source:** Real data file, synthetic signal, measured signal
2. **Mention known components:** Expected frequencies help validate analysis
3. **Specify plot preferences:** Log scale, frequency range, resolution
4. **Request specific analyses:** Harmonics, peaks, bandwidth

## Example Usage

### Example 1: Synthetic Signal Analysis

```
Create MATLAB code to analyze the frequency spectrum of a signal:

Requirements:
1. Generate a signal (sum of three sine waves)
2. Compute FFT with proper scaling
3. Calculate power spectral density
4. Create frequency vector with correct units
5. Plot time-domain signal
6. Plot magnitude spectrum (linear and dB)
7. Plot power spectral density
8. Identify dominant frequencies
9. Add proper labels, titles, and units to all plots

Signal details: Sum of sine waves at 50 Hz, 120 Hz, and 200 Hz with additive noise
Sampling rate: 1000 Hz
Duration: 1 second
Expected frequency components: 50, 120, 200 Hz
```

### Example 2: Audio Signal Analysis

```
Create MATLAB code to analyze the frequency spectrum of an audio file:

Signal details: Load audio file 'speech.wav'
Sampling rate: From file (likely 44.1 kHz)

Requirements:
- Compute FFT of entire signal
- Compute spectrogram (time-frequency analysis)
- Plot magnitude spectrum (20 Hz to 8 kHz, dB scale)
- Identify formant frequencies
- Calculate fundamental frequency if speech/voice
- Plot spectrogram with proper time and frequency axes
```

### Example 3: Windowed FFT with Averaging

```
Create MATLAB code for spectral analysis with windowing:

Signal details: Noisy sensor measurement, 10 seconds duration
Sampling rate: 2000 Hz
Expected frequency components: Unknown, need to identify peaks

Requirements:
- Use Hamming window to reduce spectral leakage
- Implement Welch's method (pwelch) for averaged PSD
- Plot single-sided spectrum (0 to Nyquist)
- Find and label top 5 peaks
- Calculate frequency resolution
- Compare windowed vs non-windowed FFT
```

## FFT Implementation Pattern

```matlab
% Parameters
fs = 1000;              % Sampling frequency (Hz)
T = 1/fs;               % Sampling period
L = 1000;               % Signal length
t = (0:L-1)*T;          % Time vector

% Generate or load signal
x = sin(2*pi*50*t) + 0.5*sin(2*pi*120*t) + randn(size(t))*0.1;

% Compute FFT
Y = fft(x);
P2 = abs(Y/L);          % Two-sided spectrum
P1 = P2(1:L/2+1);       % Single-sided spectrum
P1(2:end-1) = 2*P1(2:end-1);

% Frequency vector
f = fs*(0:(L/2))/L;

% Plot
figure;
subplot(2,1,1);
plot(t, x);
title('Time Domain');
xlabel('Time (s)');
ylabel('Amplitude');
grid on;

subplot(2,1,2);
plot(f, P1);
title('Single-Sided Amplitude Spectrum');
xlabel('Frequency (Hz)');
ylabel('|P1(f)|');
grid on;
```

## Power Spectral Density

```matlab
% Welch's method (averaged periodogram)
[pxx, f] = pwelch(x, hamming(256), 128, 256, fs);

% Plot
figure;
plot(f, 10*log10(pxx));
title('Power Spectral Density');
xlabel('Frequency (Hz)');
ylabel('Power/Frequency (dB/Hz)');
grid on;
```

## Finding Peaks

```matlab
% Find peaks in spectrum
[pks, locs] = findpeaks(P1, f, 'MinPeakHeight', threshold, ...
                        'SortStr', 'descend', 'NPeaks', 5);

% Display results
fprintf('Dominant Frequencies:\n');
for i = 1:length(pks)
    fprintf('  %.2f Hz (Amplitude: %.4f)\n', locs(i), pks(i));
end
```

## Common Issues and Solutions

### Spectral Leakage
**Problem:** Frequencies spread across multiple bins
**Solution:** Apply window function (Hamming, Hann, Blackman)

### Frequency Resolution
**Problem:** Cannot distinguish close frequencies
**Solution:** Increase signal length or use zero-padding

### Noise
**Problem:** Spectrum dominated by noise
**Solution:** Use Welch's method with averaging

## Related Prompts

- [Design Digital Filter](design-digital-filter.md) - For filtering before analysis
- [Process and Enhance Images](../image-video-processing/process-enhance-images.md) - 2D FFT for images

## References

- [MATLAB Documentation: FFT](https://www.mathworks.com/help/matlab/ref/fft.html)
- [MATLAB Documentation: Spectral Analysis](https://www.mathworks.com/help/signal/spectral-analysis.html)