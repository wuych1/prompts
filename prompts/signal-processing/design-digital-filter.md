---
title: Design Digital Filter
description: Design and analyze digital filters using Signal Processing Toolbox
tags: [matlab, signal-processing, filter-design, dsp, butterworth, chebyshev, fir, iir]
release: Requires Signal Processing Toolbox
notes:
---

# Design Digital Filter

Design and analyze digital filters (lowpass, highpass, bandpass, bandstop) using various design methods.

## Metadata

- **Tags:** `matlab` `signal-processing` `filter-design` `dsp` `butterworth` `chebyshev` `fir` `iir` `filterAnalyzer`
- **MATLAB Release:** Requires Signal Processing Toolbox
- **Required Toolboxes:** Signal Processing Toolbox

## The Prompt

```text
Design a digital filter in MATLAB with the following specifications:

Filter requirements:
- Type: [lowpass/highpass/bandpass/bandstop]
- Design method: [butter/cheby1/cheby2/ellip/fir1/firpm]
- Sampling frequency: [VALUE] Hz
- Cutoff frequency: [VALUE] Hz (or passband/stopband for bandpass)
- Filter order: [VALUE] or determine optimal

Include:
1. Filter design code
2. Frequency response plot (magnitude and phase)
3. Pole-zero plot
4. Filter application to example signal
5. Before/after comparison plots
6. Comments on filter characteristics and performance
```

## Usage Tips

1. **Specify complete requirements:** Include all frequencies and the sampling rate
2. **Mention constraints:** Real-time processing, linear phase, etc.
3. **Request specific analyses:** Group delay, impulse response, etc.
4. **Include test signal:** Describe what signal to filter

## Example Usage

### Example 1: Basic Lowpass Filter

```
Design a digital filter in MATLAB with the following specifications:

Filter requirements:
- Type: lowpass
- Design method: butterworth (butter)
- Sampling frequency: 1000 Hz
- Cutoff frequency: 100 Hz
- Filter order: 6

Include:
1. Filter design code
2. Frequency response plot (magnitude and phase)
3. Pole-zero plot
4. Filter application to noisy sine wave signal
5. Before/after comparison plots
6. Comments on filter characteristics
```

### Example 2: Bandpass Filter for Audio

```
Design a bandpass filter for audio processing:

Filter requirements:
- Type: bandpass
- Design method: Chebyshev Type I (cheby1)
- Sampling frequency: 44100 Hz
- Passband: 300 Hz to 3400 Hz (telephone bandwidth)
- Filter order: Determine optimal for < 1 dB passband ripple
- Maximum passband ripple: 0.5 dB

Include:
- Filter design with optimal order calculation
- Frequency response (magnitude in dB, phase, group delay)
- Application to speech signal
- Spectrogram comparison before/after
```

### Example 3: FIR Filter with Linear Phase

```
Design a linear-phase FIR lowpass filter:

Filter requirements:
- Type: lowpass
- Design method: fir1 (window method)
- Sampling frequency: 10 kHz
- Cutoff frequency: 1 kHz
- Filter order: 50
- Window: Hamming

Include:
- Filter coefficients
- Magnitude and phase response
- Impulse response
- Demonstrate zero-phase filtering with filtfilt
- Compare phase response with equivalent IIR filter
```

## Filter Design Methods

### IIR Filters
```matlab
% Butterworth (maximally flat)
[b, a] = butter(order, Wn);

% Chebyshev Type I (passband ripple)
[b, a] = cheby1(order, Rp, Wn);

% Chebyshev Type II (stopband ripple)
[b, a] = cheby2(order, Rs, Wn);

% Elliptic (optimal stopband and passband)
[b, a] = ellip(order, Rp, Rs, Wn);
```

### FIR Filters
```matlab
% Window method
b = fir1(order, Wn, 'low', hamming(order+1));

% Parks-McClellan (equiripple)
b = firpm(order, F, A);

% Least squares
b = firls(order, F, A);
```

## Analysis Functions

```matlab
% Frequency response
[h, w] = freqz(b, a, 1024, fs);

% Zero-pole plot
zplane(b, a);

% Filter visualization
fvtool(b, a);

% Group delay
[gd, w] = grpdelay(b, a, 1024, fs);
```

## Application Patterns

```matlab
% Standard filtering
y = filter(b, a, x);

% Zero-phase filtering (forward-backward)
y = filtfilt(b, a, x);

% Second-order sections (more stable)
[sos, g] = tf2sos(b, a);
y = filtfilt(sos, g, x);
```

## Related Prompts

- [Analyze Signal Spectrum](analyze-signal-spectrum.md) - For analyzing filter output
- [Optimize MATLAB Code Performance](../matlab-core-programming/optimize-code-performance.md) - For real-time filtering

## References

- [MATLAB Documentation: Filter Design](https://www.mathworks.com/help/signal/filter-design.html)
- [MATLAB Documentation: Practical Introduction to Digital Filter Design](https://www.mathworks.com/help/signal/ug/practical-introduction-to-digital-filter-design.html)
