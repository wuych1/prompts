---
title: Design PID Controller
description: Design and tune PID controllers for plant models with stability analysis
tags: [matlab, control-systems, pid, tuning, stability, feedback]
release: Requires Control System Toolbox
notes:
---

# Design PID Controller

Design and tune PID controllers for given plant models with stability analysis and performance evaluation.

## Metadata

- **Tags:** `matlab` `control-systems` `pid` `tuning` `stability` `feedback`
- **MATLAB Release:** Requires Control System Toolbox
- **Required Toolboxes:** Control System Toolbox

## The Prompt

```text
Design a PID controller for the given system in MATLAB:

Requirements:
1. Define the plant transfer function or state-space model
2. Use pidTuner or manual tuning to design PID gains
3. Create closed-loop system
4. Analyze step response (rise time, settling time, overshoot)
5. Analyze stability margins (gain and phase margins)
6. Plot Bode diagram and root locus
7. Compare open-loop vs closed-loop performance
8. Provide tuning rationale in comments

Plant model: [TRANSFER FUNCTION OR STATE SPACE]
Performance requirements: [RISE TIME, OVERSHOOT, SETTLING TIME]
```

## Usage Tips

1. **Provide plant model:** Transfer function, state-space, or physical parameters
2. **Specify requirements:** Concrete performance metrics help tuning
3. **Mention constraints:** Actuator limits, robustness needs, disturbance rejection
4. **Request specific analyses:** Sensitivity, disturbance response, etc.

## Example Usage

### Example 1: Basic PID Design

```
Design a PID controller for the given system in MATLAB:

Requirements:
1. Define the plant transfer function
2. Use pidTuner for automatic tuning
3. Create closed-loop system
4. Analyze step response (rise time, settling time, overshoot)
5. Analyze stability margins (gain and phase margins)
6. Plot Bode diagram and root locus
7. Compare open-loop vs closed-loop performance
8. Provide tuning rationale in comments

Plant model: G(s) = 1/(s^2 + 2s + 1)
Performance requirements:
- Settling time < 5 seconds
- Overshoot < 10%
- Zero steady-state error to step input
```

### Example 2: DC Motor Position Control

```
Design a PID controller for DC motor position control:

Plant model:
- Motor transfer function: θ(s)/V(s) = K/(s(Js + b))
- Parameters: J = 0.01 kg·m², b = 0.1 N·m·s, K = 0.01 N·m/A

Performance requirements:
- Rise time < 0.5 seconds
- Settling time < 2 seconds
- Overshoot < 5%
- No steady-state error

Include:
- PID tuning using Ziegler-Nichols or manual method
- Step response analysis
- Disturbance rejection analysis (step disturbance)
- Bode plot with gain/phase margins
- Closed-loop pole locations
```

### Example 3: Temperature Control with Constraints

```
Design a PI controller for temperature control system:

Plant model: First-order with delay G(s) = 2*exp(-5s)/(10s + 1)

Performance requirements:
- Settling time < 30 seconds
- No overshoot (critical damping preferred)
- Reject disturbances effectively

Constraints:
- Control effort limited to ±10 units
- Must be robust to 20% plant uncertainty

Include:
- PI tuning (no derivative to avoid noise amplification)
- Step response with and without disturbance
- Sensitivity function analysis
- Robustness analysis (gain/phase margins)
- Control effort plot
```

## PID Design Pattern

```matlab
% Define plant
num = [1];
den = [1 2 1];
G = tf(num, den);

% Design PID using pidTuner
C = pidTuner(G, 'PID');
% Or manual design:
Kp = 10; Ki = 5; Kd = 2;
C = pid(Kp, Ki, Kd);

% Closed-loop system
T = feedback(C*G, 1);

% Step response
figure;
step(T);
grid on;
stepinfo(T)

% Bode plot with margins
figure;
margin(C*G);
grid on;

% Root locus
figure;
rlocus(G);
grid on;
```

## Tuning Methods

### PID Tuner (Interactive)
```matlab
pidTuner(G, 'pid')  % Opens interactive GUI
```

### Ziegler-Nichols
```matlab
% Find ultimate gain and period
[Gm, Pm, Wcg, Wcp] = margin(G);
Ku = Gm;  % Ultimate gain
Tu = 2*pi/Wcp;  % Ultimate period

% ZN tuning rules
Kp = 0.6*Ku;
Ki = 2*Kp/Tu;
Kd = Kp*Tu/8;
```

### IMC Tuning
```matlab
% Internal Model Control tuning (good for first-order + delay)
tau = 10;  % Plant time constant
lambda = tau/3;  % Desired closed-loop time constant
Kp = (2*tau + delay)/(2*K*lambda);
Ki = Kp/tau;
```

## Analysis Functions

```matlab
% Step response characteristics
info = stepinfo(T);

% Stability margins
[Gm, Pm, Wcg, Wcp] = margin(L);

% Sensitivity functions
S = feedback(1, L);  % Sensitivity
T = feedback(L, 1);  % Complementary sensitivity

% Pole locations
poles = pole(T);

% Steady-state error
dcgain(T)  % Should be 1 for zero error
```

## Performance Comparison

```matlab
figure;
step(G, 'b', T, 'r');
legend('Open-Loop', 'Closed-Loop');
title('Step Response Comparison');
grid on;
```

## Related Prompts

- [Optimize MATLAB Code Performance](../programming/optimize-code-performance.md) - For real-time control
- [Create Unit Tests](../programming/create-unit-tests.md) - For controller validation

## References

- [MATLAB Documentation: PID Controller](https://www.mathworks.com/help/control/ref/pid.html)
- [MATLAB Documentation: PID Tuning](https://www.mathworks.com/help/control/ug/introduction-pid-controller-types.html)