

![[image1.png]]

| R (kΩ) | ζ    | t\_d Sim (µs) | t\_d Exp (µs) | t\_r Sim (µs) | t\_r Exp (µs) | M\_p Sim (%) | M\_p Exp (%) | t\_p Sim (µs) | t\_p Exp (µs) | t\_s Sim (µs) | t\_s Exp (µs) |
| ------ | ---- | ------------- | ------------- | ------------- | ------------- | ------------ | ------------ | ------------- | ------------- | ------------- | ------------- |
| 1.0    | 0.50 | **10.35**     | 10.3          | **13.10**     | 13.6          | **16.30**    | **16.0**     | **29.02**     | 28.8          | **64.61**     | 64.4          |
| 2.0    | 1.00 | **13.43**     | 15.2          | **26.86**     | 26.4          | **0**        | **0**        | **N/A**       | **N/A**       | **46.67**     | 61.2          |
| 7.5    | 3.75 | **41.93**     | 40.4          | **129.45**    | 120           | **0**        | **0**        | **N/A**       | **N/A**       | **231.57**    | 192           |
| 4.5    | 2.25 | **25.58**     | 26.5          | **75.10**     | 70.8          | **0**        | **0**        | **N/A**       | **N/A**       | **135.43**    | 112           |

| R | ζ | Response |
| ----- | ----- | ----- |
| 1 kΩ | 0.50 | **Underdamped** |
| 2 kΩ | 1.00 | **Critically damped** |
| 4.5 kΩ | 2.25 | **Overdamped** |
| 7.5 kΩ | 3.75 | **Overdamped** |

| R range | ζ range | Expected response |
| ----- | ----- | ----- |
| (R\<2,k\\Omega) | (0\<\\zeta\<1) | Underdamped |
| (R=2,k\\Omega) | (\\zeta=1) | Critically damped |
| (R\>2,k\\Omega) | (\\zeta\>1) | Overdamped |

### **Observations**

1. At **R \= 1 kΩ**, the damping ratio is 0.5, producing an **underdamped response** with visible oscillations and approximately **16% maximum overshoot**.  
2. Increasing resistance increases the damping ratio and reduces the oscillations and overshoot.  
3. At **R \= 2 kΩ**, the damping ratio becomes 1, giving a **critically damped response** with no overshoot and the fastest non-oscillatory response.  
4. For **R \> 2 kΩ**, the circuit becomes **overdamped**. Increasing R further makes the response slower and increases the settling time.  
5. At **R \= 4.5 kΩ and 7.5 kΩ**, there is no overshoot or peak, so Mp​=0% and tp​ is not applicable.  
6. Small differences between simulation and experimental values are expected because of resistor/capacitor/inductor tolerances


# PART 3


### Observations

#### i) Default second-order system

1. For ( \omega_n=3) rad/s and (\zeta=1), the system is **critically damped** and reaches steady state without oscillations or overshoot.
2. Increasing the damping ratio generally reduces oscillations and overshoot, while increasing the natural frequency makes the response faster.

#### ii) Variation of damping ratio with (ζ\omega_n=6)

1. As (\zeta) decreases from 0.8 to 0.2, the system becomes more underdamped, resulting in **increased overshoot and oscillations**.
2. The pole locations move closer to the imaginary axis as damping decreases.
3. Rise time and peak time generally decrease with increasing natural frequency, while the peak overshoot increases as (\zeta) decreases.

#### iii) Variation of natural frequency with (\zeta=0.4)

1. Increasing (\omega_n) from 3 to 8 rad/s makes the system response **faster**, reducing rise time and peak time.
2. The damping ratio remains constant, so the **percentage overshoot remains approximately the same** for all cases.
3. The poles move farther from the origin as (\omega_n) increases.

#### iv) Variation of damping ratio with (ω_d=3) rad/s

1. Decreasing (\zeta) from 0.9 to 0.2 increases oscillations and peak overshoot significantly.
2. Since the damped frequency (ω_d) is kept constant, the oscillation frequency remains approximately the same for all cases.
3. Lower damping causes the poles to move closer to the imaginary axis, resulting in a more oscillatory response and longer settling time.

#### v) Variation of (a_o)  zeros near/far from origin

1. Changing (a_o) changes the location of the zero at (s=-a_o), significantly affecting the transient response.
2. When the zero is close to the origin, it has a stronger influence on the response and can significantly alter overshoot and settling behavior.
3. When the zero is far from the origin, its influence on the transient response becomes smaller and the response is increasingly dominated by the system's complex poles.

#### vi) Variation of (a_o) additional pole

1. Changing (a_o) introduces a pole at (s=-a_o); as (a_o) decreases, this pole moves closer to the origin.
2. A pole close to the origin becomes **dominant** and makes the system response slower, increasing the settling time.
3. For large (a_o), the additional pole is far from the origin and has less influence, so the original complex poles dominate the response.

## Code and Plots

i) 

ans =  

RiseTime: 1.1194  
TransientTime: 1.9447  
SettlingTime: 1.9447  
SettlingMin: 0.9019  
SettlingMax: 0.9999  
Overshoot: 0  
Undershoot: 0  
Peak: 0.9999  
PeakTime: 3.9758

```matlab
wn = 3;
zeta = 1;
G = tf(wn^2,[1 2*zeta*wn wn^2])
figure;
step(G);
grid on;
title('Second Order System - Default');
xlabel('Time (s)');
ylabel('Amplitude');
figure;
pzmap(G);
grid on;
title('Pole-Zero Map - Default');
disp('Step Information:');
stepinfo(G)
```

![[Pasted image 20260822102018.png]]


ii) 
```matlab
%% ii) Vary damping ratio
% zeta = 0.8,0.6,0.4,0.2
% zeta*wn = 6

zeta_values = [0.8 0.6 0.4 0.2];
wn_values = 6./zeta_values;

figure;
hold on;

for k = 1:length(zeta_values)
    zeta = zeta_values(k);
    wn = wn_values(k);

    G = tf(wn^2,[1 2*zeta*wn wn^2]);

    pzmap(G);
    hold on;

    fprintf('\nzeta = %.1f, wn = %.2f\n',zeta,wn);
    disp(G);
end

grid on;
title('Pole-Zero Map for Different Damping Ratios');
axis([-10 1 -10 10]);

figure;
hold on;

for k = 1:length(zeta_values)
    zeta = zeta_values(k);
    wn = wn_values(k);

    G = tf(wn^2,[1 2*zeta*wn wn^2]);
    step(G);
end

grid on;
legend('\zeta=0.8','\zeta=0.6','\zeta=0.4','\zeta=0.2');
title('Step Responses for Different Damping Ratios');
xlabel('Time (s)');
ylabel('Amplitude');

% Performance specifications

tr = zeros(1,length(zeta_values));
tp = zeros(1,length(zeta_values));
mp = zeros(1,length(zeta_values));

for k = 1:length(zeta_values)

    zeta = zeta_values(k);
    wn = wn_values(k);

    G = tf(wn^2,[1 2*zeta*wn wn^2]);
    info = stepinfo(G);

    tr(k) = info.RiseTime;
    tp(k) = info.PeakTime;
    mp(k) = info.Overshoot;
end

figure;
plot(zeta_values,tr,'o-','LineWidth',2);
grid on;
xlabel('\zeta');
ylabel('Rise Time (s)');
title('Rise Time vs Damping Ratio');

figure;
plot(zeta_values,mp,'o-','LineWidth',2);
grid on;
xlabel('\zeta');
ylabel('Peak Overshoot (%)');
title('Peak Overshoot vs Damping Ratio');

figure;
plot(zeta_values,tp,'o-','LineWidth',2);
grid on;
xlabel('\zeta');
ylabel('Peak Time (s)');
title('Peak Time vs Damping Ratio');
```


![[Pasted image 20260822102227.png]]

![[Pasted image 20260822102246.png]]

![[Pasted image 20260822102321.png]]

![[Pasted image 20260822102337.png]]

![[Pasted image 20260822102355.png]]

iii)

```matlab
%% iii) Vary natural frequency
% wn = 3,4,6,8
% zeta = 0.4
wn_values = [3 4 6 8];
zeta = 0.4;

figure;
hold on;

for k = 1:length(wn_values)
    wn = wn_values(k);
    G = tf(wn^2,[1 2*zeta*wn wn^2]);
    pzmap(G);
    hold on;
    fprintf('\nwn = %.1f, zeta = %.1f\n',wn,zeta);
    disp(G);
end

grid on;
title('Pole-Zero Map for Different Natural Frequencies');
axis([-4 1 -5 5]);
figure;
hold on;

for k = 1:length(wn_values)
    wn = wn_values(k);
    G = tf(wn^2,[1 2*zeta*wn wn^2]);
    step(G);
end

grid on;
legend('\omega_n=3','\omega_n=4','\omega_n=6','\omega_n=8');
title('Step Responses for Different Natural Frequencies');
xlabel('Time (s)');
ylabel('Amplitude');
```

![[Pasted image 20260822102552.png]]

![[Pasted image 20260822102607.png]]


iv)

- **ζ = 0.9:** heavily damped, very small overshoot, slowest oscillatory response.
- **ζ = 0.7:** moderate damping and small overshoot.
- **ζ = 0.5:** noticeable overshoot and oscillation.
- **ζ = 0.2:** highly underdamped, large overshoot and sustained-looking oscillations.
- Since ωd​=3 rad/s is kept constant, the **oscillation frequency remains the same** for all four cases.
- Decreasing ζ moves the poles closer to the imaginary axis, resulting in greater oscillation and larger overshoot.

Performance specifications for Part iv  
  
zeta = 0.9  
wn = 6.8825 rad/s  
Rise Time = 0.4190 s  
Peak Time = 1.0483 s  
Overshoot = 0.15 %  
Settling Time = 0.6829 s  
  
zeta = 0.7

wn = 4.2008 rad/s  
Rise Time = 0.5063 s  
Peak Time = 1.0493 s  
Overshoot = 4.60 %  
Settling Time = 1.4233 s  
  
zeta = 0.5  
wn = 3.4641 rad/s  
Rise Time = 0.4731 s  
Peak Time = 1.0369 s  
Overshoot = 16.29 %  
Settling Time = 2.3313 s  
  
zeta = 0.2  
wn = 3.0619 rad/s  
Rise Time = 0.3938 s  
Peak Time = 1.0528 s  
Overshoot = 52.65 %  
Settling Time = 6.4001 s

```matlab
%% iv) Vary damping ratio
% wd = wn*sqrt(1-zeta^2) = 3 rad/s

zeta_values = [0.9 0.7 0.5 0.2];
wd = 3;

figure;
hold on;

for k = 1:length(zeta_values)
    zeta = zeta_values(k);
    wn = wd/sqrt(1-zeta^2);
    G = tf(wn^2,[1 2*zeta*wn wn^2]);
    pzmap(G);
    hold on;
    fprintf('\nzeta = %.1f, wn = %.4f\n',zeta,wn);
    disp(G);
end

grid on;
title('Pole-Zero Map - Constant Damped Frequency');
axis([-7 1 -5 5]);

figure;
hold on;

for k = 1:length(zeta_values)
    zeta = zeta_values(k);
    wn = wd/sqrt(1-zeta^2);
    G = tf(wn^2,[1 2*zeta*wn wn^2]);
    step(G);
end

grid on;
legend('\zeta=0.9','\zeta=0.7','\zeta=0.5','\zeta=0.2');
title('Step Responses - Constant \omega_d');
xlabel('Time (s)');
ylabel('Amplitude');

disp('Performance specifications for Part iv');

for k = 1:length(zeta_values)
    zeta = zeta_values(k);
    wn = wd/sqrt(1-zeta^2);
    G = tf(wn^2,[1 2*zeta*wn wn^2]);
    info = stepinfo(G);
    fprintf('\nzeta = %.1f\n',zeta);
    fprintf('wn = %.4f rad/s\n',wn);
    fprintf('Rise Time = %.4f s\n',info.RiseTime);
    fprintf('Peak Time = %.4f s\n',info.PeakTime);
    fprintf('Overshoot = %.2f %%\n',info.Overshoot);
    fprintf('Settling Time = %.4f s\n',info.SettlingTime);
end

```


![[Pasted image 20260822102733.png]]

![[Pasted image 20260822102748.png]]

v)

```matlab
%% v-a) Vary ao from 1 to -1
% G(s) = 9(s+ao) / [ao(s^2+3s+9)]

ao_values = 1:-0.1:-1;
figure;
hold on;

for k = 1:length(ao_values)
    ao = ao_values(k);
    if ao == 0
        continue;
    end
    G = tf(9*[1 ao],ao*[1 3 9]);
    step(G);
end

grid on;
title('Step Responses - a_o from 1 to -1');
xlabel('Time (s)');
ylabel('Amplitude');

figure;
hold on;

for k = 1:length(ao_values)
    ao = ao_values(k);
    if ao == 0
        continue;
    end
    G = tf(9*[1 ao],ao*[1 3 9]);
    pzmap(G);
    hold on;
end

grid on;
title('Pole-Zero Map - a_o from 1 to -1');

figure;
hold on;

for k = 1:length(ao_values)
    ao = ao_values(k);
    if ao == 0
        continue;
    end
    G = tf(9*[1 ao],ao*[1 3 9]);
    impulse(G);
end

grid on;
title('Impulse Responses - a_o from 1 to -1');
xlabel('Time (s)');
ylabel('Amplitude');
```


![[Pasted image 20260822102907.png]]

![[Pasted image 20260822102920.png]]

![[Pasted image 20260822102932.png]]


V) ii)

```matlab
%% v-b) Vary ao from 10 to -10
% G(s) = 9(s+ao) / [ao(s^2+3s+9)]

ao_values = 10:-0.5:-10;

figure;
hold on;

for k = 1:length(ao_values)
    ao = ao_values(k);
    if ao == 0
        continue;
    end
    G = tf(9*[1 ao],ao*[1 3 9]);
    step(G);
end

grid on;
title('Step Responses - a_o from 10 to -10');
xlabel('Time (s)');
ylabel('Amplitude');

figure;
hold on;

for k = 1:length(ao_values)
    ao = ao_values(k);
    if ao == 0
        continue;
    end
    G = tf(9*[1 ao],ao*[1 3 9]);
    pzmap(G);
    hold on;
end

grid on;
title('Pole-Zero Map - a_o from 10 to -10');

figure;
hold on;

for k = 1:length(ao_values)
    ao = ao_values(k);
    if ao == 0
        continue;
    end
    G = tf(9*[1 ao],ao*[1 3 9]);
    impulse(G);
end

grid on;
title('Impulse Responses - a_o from 10 to -10');
xlabel('Time (s)');
ylabel('Amplitude');

```

![[Pasted image 20260822103124.png]]


![[Pasted image 20260822103150.png]]

![[Pasted image 20260822103202.png]]

vi)

```matlab
%% vi) Vary ao from 20 to 0
% G(s) = 9 / [ao(s+ao)(s^2+3s+9)]

ao_values = 20:-0.2:0.2;

figure;
hold on;

for k = 1:length(ao_values)
    ao = ao_values(k);
    G = tf(9,ao*conv([1 ao],[1 3 9]));
    step(G);
end

grid on;
title('Step Responses - Varying a_o');
xlabel('Time (s)');
ylabel('Amplitude');

figure;
hold on;

for k = 1:length(ao_values)
    ao = ao_values(k);
    G = tf(9,ao*conv([1 ao],[1 3 9]));
    pzmap(G);
    hold on;
end

grid on;
title('Pole-Zero Map - Varying a_o');

figure;
hold on;

for k = 1:length(ao_values)
    ao = ao_values(k);
    G = tf(9,ao*conv([1 ao],[1 3 9]));
    impulse(G);
end

grid on;
title('Impulse Responses - Varying a_o');
xlabel('Time (s)');
ylabel('Amplitude');
```

![[Pasted image 20260822103415.png]]

![[Pasted image 20260822103428.png]]

![[Pasted image 20260822103439.png]]

