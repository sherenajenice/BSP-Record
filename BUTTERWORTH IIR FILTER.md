## EXP NO:03	DESIGN OF DIGITAL BUTTERWORTH IIR FILTER 
## DATE :
## AIM:

To design a digital Butterworth filter using bilinear method satisfying the constraints using matlab. Assume T=1 sec

		          0.707 ≤│H(w)│≤ 1.0        ; 0 ≤w ≤ 0.2 π
                                             │H(w)│≤  0.08     ; 0.4π ≤ w ≤ π

## ALGORITHM:
	Start the matlab software
	Assign the variable for pass band ripple ,stop band ripple, pass band and stopband frequency
	Determine the order of filter using the required formula.
	Find the filter co-efficient a and b
	Assign the time and amplitude
	Plot the magnitude and phase angle.
	Give the x label and ylabel and title it
	Save and run the program

## PROGRAM:
clear all
clc

AP = 0.707;                 % Gain at passband edge frequency
AS = 0.08;                  % Gain at stopband edge frequency

PEF_D = 0.2*pi;             % Passband edge digital frequency
SEF_D = 0.4*pi;             % Stopband edge digital frequency

T = 1;                      % Sampling time

% Passband and stopband attenuation in dB
alpha_P = -20*log10(AP)
alpha_S = -20*log10(AS)

% Prewarping of digital frequencies to analog frequencies
PEF_A = (2/T)*tan(PEF_D/2)
SEF_A = (2/T)*tan(SEF_D/2)

% Order and cutoff frequency calculation
[N, CF] = buttord(PEF_A, SEF_A, alpha_P, alpha_S, 's')

% Normalized Butterworth Transfer Function
[Bn, An] = butter(N, 1, 's');
disp('Normalized Transfer Function is:')
Hsn = tf(Bn, An)

% Unnormalized Butterworth Transfer Function
[B, A] = butter(N, CF, 's');
disp('Unnormalized Transfer Function is:')
Hs = tf(B, A)

% Bilinear Transformation for Digital Filter
[num, den] = bilinear(B, A, 1/T);

% Digital Transfer Function
disp('Digital Transfer Function is:')
Hz = tf(num, den, T)

% Frequency Response
w = 0:pi/16:pi;

disp('Frequency Response is:')
Hw = freqz(num, den, w);

% Magnitude Response
disp('Magnitude Response is:')
Hw_mag = abs(Hw);

% Plot Magnitude Response
plot(w/pi, Hw_mag, 'k');
grid on;

title('Magnitude Response of Butterworth Lowpass Filter', ...
    'fontweight', 'bold');

xlabel('Normalized Frequency, \omega/\pi', ...
    'fontweight', 'bold');

ylabel('Magnitude', ...
    'fontweight', 'bold');




## OUTPUT

<img width="918" height="472" alt="image" src="https://github.com/user-attachments/assets/a5fb3293-26f4-4ff8-9fa5-ff3ff7701906" />



## RESULT:

Thus, digital Butterworth IIR filter with the given specifications was designed using MatLab.
 
