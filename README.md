# Avoiding_Floating_Point
Hints and Tips on how to avoid using Floating Point, especially useful on resource constrained Microcontrollers

Let us consider a 12bit ADC, with a 3V3 reference voltage

Vout_V is the converted voltage, in volts.
ADC_Count is the measured ADC conversion value
ADC_Steps is the number of possible conversion values  (2 rasied to the power of 12 for a 12bit ADC)

double Vout_V =0.0;
Vout_V = (3.3 / 4096 ) * ADC_Count;
Vout_V = 0.0008056640625 * ADC_Count;

So we cannot eliminate floating point unless we change the scale of Vout

Good options would be Vout_mV or Vout_uV

[AT THIS POINT WE NEED TO UNDERSTAND OUR REQUIREMENT, ACCURACY + ERROR BUDGET etc....]

Let us say 
Vout_mV

