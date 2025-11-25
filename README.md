# FREQUENCY-DIVISION-MULTIPLEXING

## AIM
To simulate Frequency Division Multiplexing (FDM) using Scilab and observe the multiplexing and demultiplexing of multiple message signals transmitted over different carrier frequencies.

## APPARATUS REQUIRED
A computer system

Scilab (Latest stable version)

Signal Processing Toolbox (inbuilt functions)

## THEORY
```
Frequency Division Multiplexing is a technique in which multiple message signals are transmitted simultaneously over a communication channel by allocating different carrier frequencies to each signal. Each
signal modulates its own carrier → modulated signals are added → transmitted together → separated at the receiver using band-pass filters or carrier synchronization.

```

## ALGORITHM
```
1.Start Scilab.
2.Define simulation parameters:
3.Time vector
4.Carrier frequencies
5.Amplitude values
6.Generate two or more message signals (e.g., sine waves).
7.Generate carrier signals corresponding to each message.
8.Modulate each message using image
6. Add all modulated signals to obtain FDM signal.
7. Plot: - Message signals - Carrier signals - Individual modulated signals - Final FDM signal
8. Multiply FDM signal with each respective carrier.
9. Apply a Low-Pass Filter (LPF) to retrieve the baseband message.
10. Plot the recovered signals.
11. End.

```

## CODE
```
Fs = 50000;
t = 0:1/Fs:0.02;

m1 = 3.6 * sin(2*%pi*499*t);
m2 = 3.8 * sin(2*%pi*509*t);
m3 = 4.1 * sin(2*%pi*519*t);
m4 = 4.2 * sin(2*%pi*529*t);
m5 = 4.4 * sin(2*%pi*539*t);
m6 = 4.6 * sin(2*%pi*549*t);

c1 = 7000; 
c2 = 95000; 
c3 = 12500; 
c4 = 17000; 
c5 = 22000; 
c6 = 27000;

carrier1 = cos(2*%pi*c1*t);
carrier2 = cos(2*%pi*c2*t);
carrier3 = cos(2*%pi*c3*t);
carrier4 = cos(2*%pi*c4*t);
carrier5 = cos(2*%pi*c5*t);
carrier6 = cos(2*%pi*c6*t);

s1 = m1 .* carrier1;
s2 = m2 .* carrier2;
s3 = m3 .* carrier3;
s4 = m4 .* carrier4;
s5 = m5 .* carrier5;
s6 = m6 .* carrier6;

s_total = s1 + s2 + s3 + s4 + s5 + s6;

r1 = s_total .* carrier1;
r2 = s_total .* carrier2;
r3 = s_total .* carrier3;
r4 = s_total .* carrier4;
r5 = s_total .* carrier5;
r6 = s_total .* carrier6;

function y = ideal_lowpass_fft(x, Fs, fc)
    N = length(x);
    X = fft(x);
    f = Fs*(0:N-1)/N;
    mask = (f <= fc) | (f >= Fs-fc);
    Y = X .* mask;
    y = real(ifft(Y));
endfunction

fc = 1000; 

dm1 = ideal_lowpass_fft(r1, Fs, fc);
dm2 = ideal_lowpass_fft(r2, Fs, fc);
dm3 = ideal_lowpass_fft(r3, Fs, fc);
dm4 = ideal_lowpass_fft(r4, Fs, fc);
dm5 = ideal_lowpass_fft(r5, Fs, fc);
dm6 = ideal_lowpass_fft(r6, Fs, fc);

figure(1);
subplot(3,2,1); plot(t,m1); title("Message Signal 1");
subplot(3,2,2); plot(t,m2); title("Message Signal 2");
subplot(3,2,3); plot(t,m3); title("Message Signal 3");
subplot(3,2,4); plot(t,m4); title("Message Signal 4");
subplot(3,2,5); plot(t,m5); title("Message Signal 5");
subplot(3,2,6); plot(t,m6); title("Message Signal 6");

figure(2);
plot(t, s_total); title("Multiplexed FDM Signal");
figure(3);

subplot(3,2,1); plot(t,dm1); title("Recovered Signal 1");
subplot(3,2,2); plot(t,dm2); title("Recovered Signal 2");
subplot(3,2,3); plot(t,dm3); title("Recovered Signal 3");
subplot(3,2,4); plot(t,dm4); title("Recovered Signal 4");
subplot(3,2,5); plot(t,dm5); title("Recovered Signal 5");
subplot(3,2,6); plot(t,dm6); title("Recovered Signal 6");
```
## OUTPUT:


## TABULAR COLUMN:


## RESULT:
Frequency Division Multiplexing (FDM) using Scilab and observe the multiplexing and demultiplexing of multiple message signals transmitted over different carrier frequencies is stimulated.
