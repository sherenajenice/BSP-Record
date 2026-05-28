## EXP NO: 4	DESIGN OF DIGITAL CHEBYSHEV IIR FILTER

## DATE :

## AIM:

To design a digital Chebyshev filter using bilinear method satisfying the constraints using matlab. Assume T=1 sec

0.8 ≤│H(w)│≤ 1.0               ; 0 ≤w ≤ 0.2 π
                                                      │H(w)│≤  0.2              ; 0.32 ≤ w ≤ π

## ALGORITHM:
	Start the  matlab software
	Assign the variable for pass band ripple ,stop band ripple, pass band and stop band frequency
	Determine the order of filter using the required formula.
	Find the filter co-efficient a and b
	Assign the time and amplitude
	Plot the magnitude and phaseangle.
	Give the x labe land ylabel and title it
	Save and run the program.

## PROGRAM:
clear all
clc

AP=0.8;						% Gain at passband edge frequency
AS=0.2;						% Gain at stopband edge frequency
PEF_D=0.2*pi;					% Passband edge digital frequency
SEF_D=0.32*pi;					% Stopband edge digital frequncy
T=1;						% Sampling time
alpha_P=-20*log10(AP)				% Passband attenuation in dB
alpha_S=-20*log10(AS)				% Stopband atenuation on dB

PEF_A=(2/T)*tan(PEF_D/2)
SEF_A=(2/T)*tan(SEF_D/2)

[N,CF]=cheb1ord(PEF_A,SEF_A,alpha_P,alpha_S,'s')	% Order and cutoff frequency

[Bn,An]=cheby1(N,alpha_P,1,'s');			% Normalised transfer function
display('Normalized Transfer Function is,')
Hsn=tf(Bn,An)

[B,A]=cheby1(N,alpha_P,CF,'s');			% Unnormalised transfer function
display('Unnormalised Transfer Function is,')
Hs=tf(B,A)

[num,den]=impinvar(B,A,1/T);			% Digital Transfer function
display('Digital Transfer Function is,')
Hz=tf(num,den,T)

w=0:pi/16:pi;
display('Frequency Response is,')
Hw=freqz(num,den,w)				% Frequency response
display('Magnitude Response is,')
Hw_mag=abs(Hw)				% Magnitude response
plot(w/pi,Hw_mag,'k');grid;

title('Magnitude Response of Chebyshev 3rd order Lowpass Filter','fontweight','b');
xlabel('Normalised frequency, \omega/\pi','fontweight','b');
ylabel('Magnitude','fontweight','b');




## OUTPUT

<img width="891" height="468" alt="image" src="https://github.com/user-attachments/assets/f140d618-495c-4094-81ff-89d4142552d1" />



##  RESULT:

Thus,the digital Chebyshev filter with the given specifications was designed using MatLab.
 
