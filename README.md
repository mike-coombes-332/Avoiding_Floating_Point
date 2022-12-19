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
uint32_t Vout_mV = 0;

Vout_mV = (ADC_Count * 825) >> 10;
                                          Remembering >>10 = / 1024
 
                                          uint32_t toDevide1 = 131072;
                                          uint32_t toDevide2 = 131072;
                                          printf("%d   %d \n\n",(toDevide1/1024),(toDevide2>>10));

                                          Output = 128   128 

So the calcualtion we now have for Vout_mV has a multiplication and binary shift (bit shift division)

uint32_t Vout_mV = 0;
uint32_t ADC_Count = 2048;

Vout_mV = (ADC_Count * 825) >> 10;
printf("%d   %d \n\n",Vout_mV,ADC_Count);

What do we expect the output to be? Wel ADC_Count is half way between max and min, and so with vref = 3300mV I would expect the value to be half that...

1650   2048

So now we have a method of calculating the VOUT voltage to mV resolution without using Floating point using a multiplication and binary shift. So how did id choose * 825 and >>1024


