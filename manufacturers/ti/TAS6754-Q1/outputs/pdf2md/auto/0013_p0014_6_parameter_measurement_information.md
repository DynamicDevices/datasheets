# 6 Parameter Measurement Information

For measurements, the LC reconstruction filter Cyntec VCMT053T-3R3MN5 3.3µH inductor + 1µF capacitor is used.

When enabling Real-Time Load Diagnostics with the integrated pilot tone, an analog balanced input filter must be used to avoid misleading measurement results. An elliptic high pass filter as provided by the APx500 series with a cutoff frequency of 20Hz and a low-pass filter such as AES17 (20kHz) are recommended. If the test equipment does not support this filter type, TI recommends to turn off the Real-Time Load Diagnostics for accurate performance measurements.