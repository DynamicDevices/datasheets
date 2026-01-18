# 6 Use cases and measurement results

The main use cases and subcases that form the benchmarks for the i.MX 93 internal power measurements on the EVK platform are described in the following sections.

**Note:**

- Before running a use case, `<configuration_script>.sh` must be run to configure the environment, see Section 8.
- For all use cases except TBD cases, the platform is booted from eMMC with the default DTB configuration (imx93-11x11-evk.dtb) in the U-Boot stage.
- The current sample resistors on the power path create a drop in the voltage on each power rail.

Table 7 summarizes the power measurement results of various use cases performed on the MCIMX93ULP-EVK board.

![Table 7: i.MX 93-EVK power summary report - Part 1](./images/page_10_table_1.png)

**Table 7. i.MX 93-EVK power summary report**

<!-- VERBATIM_TABLE_START -->
![Table (page 10)](./images/page_10_table_1.png)

|Use cases category|Use cases|Total power (sum of average powers in GROUP_SOC_FULL) (mW)|
|---|---|---|
|Core benchmark use cases|Dhrystone|805.9|
||CoreMark|691.9|
|Memory use cases|memset|908.0|
||memcpy|913.9|
||Stream|1222.8|
|Audio/video playback use cases|Audio playback (gplay)|458.6|
||Audio low&amp;#45;bus playback (gplay)|255.4|
||Video playback local (gplay)|636.4|
||Video playback streaming (gplay)|664.6|
|Graphic use case|PXP|544.0|
|Machine learning use cases|eIQ benchmark|725.5|
||Machine vision|780.5|
|Storage use cases|DD_WRITE_eMMC|420.4|
||DD_READ_eMMC|644.9|
||DD_WRITE_SD|527.6|
||DD_READ_SD|518.2|
|Low&amp;#45;power mode use cases|System Idle with display in OD mode with DDRC auto clock gating|482.5|
||System Idle with display in ND mode|382.0|
||System Idle with display in LD mode (DDR to half speed)|315.2|
||System Idle with display in LD mode (DDR to lowest speed with SWFFC)|275.3|
||System Idle without display in OD mode with DDRC auto clock gating|345.6|
||System Idle without display in ND mode with DDRC auto clock gating|288.1|
||System Idle without display in LD mode with DDRC auto clock gating (DDR to half speed)|227.2|
||System Idle without display in LD mode with DDRC auto clock gating (DDR to lowest speed with SWFFC)|199.9|
||System in DSM|7.6|
||Battery|0.1|
|Stress test use cases|2 x A55 Dhrystone + PXP + M33 Core Mark + NPU|1230.5|
||2 x A55 Stream + PXP + M33 Core Mark + NPU|1264.1|
<!-- VERBATIM_TABLE_END -->

---

![Table 7: i.MX 93-EVK power summary report - Part 2](./images/page_11_table_1.png)

**Table 7. i.MX 93-EVK power summary report...continued**

<!-- VERBATIM_TABLE_START -->
![Table (page 11)](./images/page_11_table_1.png)

|Use cases category|Use cases|Total power (sum of average powers in GROUP_SOC_FULL) (mW)|
|---|---|---|
|Product use cases|Linux Suspend + M33 CoreMark (TCM)|128.2|
||Linux Suspend + M33 in WFI|122.4|
||Linux Suspend + M33 FlexCAN Transaction|132.3|
||Smart doorbell|772.1|
<!-- VERBATIM_TABLE_END -->

---

## 6.1 Core benchmark use cases

The following use cases scenarios have been tested with Cortex A55 cores:

- Dhrystone
- CoreMark

### 6.1.1 Dhrystone

Dhrystone is a synthetic benchmark used to measure the integer computational performance of processors and compilers. The small size of the Dhrystone benchmark enables it to fit into the L1 cache and minimizes access to the L2 cache and DDR.

In this use case, the two Cortex-A55 cores perform the Dhrystone test. Because Dhrystone is a single thread benchmark, two instances have been started. All Cortex-A55 cores run the test in a loop at a frequency of 1.7 GHz.

When the use case is running, the state of the system is as follows:

1. The CPU frequency is set to the maximum value of 1.7 GHz.
2. The DDR data rate is set to 3733 MT/s.
3. The display is OFF.
4. The CM33 is in reset hold, waiting for the reset signal release.

To measure the power consumption of Dhrystone, the steps are as follows:

1. Boot the Linux image with imx93-11x11-evk.dtb.
2. Run setup.sh, see Section 8.
3. Run dhrystone_loop.sh:

```bash
while [ "1" == "1" ]; do
  taskset -c 0 ./dhry2 &
  taskset -c 1 ./dhry2
done
```

4. Measure the power and record the results.

Table 8 shows the measurement results when this use case is applied to the i.MX 93 processor.

![Table 8: Measurement results for i.MX 93-11x11-EVK_B_Dhrystone_loop - Part 1](./images/page_11_table_2.png)

**Table 8. Measurement results for i.MX 93-11x11-EVK_B_Dhrystone_loop (average value)**

<!-- VERBATIM_TABLE_START -->
![Table (page 11)](./images/page_11_table_2.png)

|Rail label|Col2|Average voltage (V)|Average current (mA)|Average power (mW)|Sum of average powers (mW)|Zone 0 die temperature (°C)|
|---|---|---|---|---|---|---|
|GROUP_DRAM|lpd4x_vdd1|1.8|0.6|1.1|6.72|40.35|
||lpd4x_vdd2|1.1|5.1|5.6|||
<!-- VERBATIM_TABLE_END -->

---

![Table 8: Measurement results for i.MX 93-11x11-EVK_B_Dhrystone_loop - Part 2](./images/page_12_table_1.png)

**Table 8. Measurement results for i.MX 93-11x11-EVK_B_Dhrystone_loop (average value)...continued**

<!-- VERBATIM_TABLE_START -->
![Table (page 12)](./images/page_12_table_1.png)

|Rail label|Col2|Average voltage (V)|Average current (mA)|Average power (mW)|Sum of average powers (mW)|Zone 0 die temperature (°C)|
|---|---|---|---|---|---|---|
||lpd4x_vddq|0.6|0|0|||
|GROUP_SOC_ FULL|nvcc_1p8|1.8|0.3|0.6|805.87||
||nvcc_3p3|3.3|3.6|12|||
||nvcc_bbsm_ 1p8|1.79|0.11|0.2|||
||nvcc_sd2|3.3|0.9|3.1|||
||vdd2_ddr|1.1|17.3|18.9|||
||vdd_ana_0p8|0.79|16.5|13|||
||vdd_ana_1p8|1.79|12.5|22.4|||
||vdd_soc|0.89|821.2|731.4|||
||vdd_usb_3p3|3.3|0.03|0.1|||
||vddq_ddr|0.6|6.8|4.1|||
<!-- VERBATIM_TABLE_END -->

---

### 6.1.2 CoreMark

CoreMark is a modern, sophisticated benchmark that lets you accurately measure the processor performance and is intended to replace the older Dhrystone benchmark. Arm recommends using CoreMark over Dhrystone.

When the use case is running, the state of the system is as follows:

1. The CPU frequency is set to the maximum value of 1.7 GHz.
2. The DDR data rate is set to 3733 MT/s.
3. The display is OFF.
4. The CM33 is in reset hold, waiting for the reset signal release.

To measure the power consumption of CoreMark, the steps are as follows:

1. Boot the Linux image with imx93-11x11-evk.dtb.
2. Run setup.sh, see Section 8.
3. Run coremark_loop.sh:

```bash
while true; do
  ./coremark > /dev/null 2>&1
done
```

**Note:** For the best performance, compile as follows:

```bash
make XCFLAGS="-DMULTITHREAD=2 -DUSE_PTHREAD -pthread"
```

4. Measure the power and record the results.

Table 9 shows the measurement results when this use case is applied to the i.MX 93 processor.

![Table 9: Measurement results for i.MX 93-11x11-EVK_B_CoreMark_loop](./images/page_12_table_2.png)

**Table 9. Measurement results for i.MX 93-11x11-EVK_B_CoreMark_loop (average value)**

<!-- VERBATIM_TABLE_START -->
![Table (page 12)](./images/page_12_table_2.png)

|Rail label|Col2|Average voltage (V)|Average current (mA)|Average power (mW)|Sum of average powers (mW)|Zone 0 die temperature (°C)|
|---|---|---|---|---|---|---|
|GROUP_DRAM|lpd4x_vdd1|1.8|0.44|0.8|5.91|38|
<!-- VERBATIM_TABLE_END -->