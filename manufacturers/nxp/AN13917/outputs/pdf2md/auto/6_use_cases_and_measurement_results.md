# 6  Use cases and measurement results

The main use cases and subcases that form the benchmarks for the i.MX 93 internal power measurements on the EVK platform are described in the following sections.

**Note:**
- Before running a use case, `<configuration_script>.sh` must be run to configure the environment, see Section 8.
- For all use cases except TBD cases, the platform is booted from eMMC with the default DTB configuration (imx93-11x11-evk.dtb) in the U-Boot stage.
- The current sample resistors on the power path create a drop in the voltage on each power rail.

Table 7 summarizes the power measurement results of various use cases performed on the MCIMX93ULP-EVK board.

## Table 7. i.MX 93-EVK power summary report

| Use cases category | Use cases | Total power (sum of average powers in GROUP_SOC_FULL) (mW) |
|-------------------|-----------|-----------------------------------------------------------|
| Core benchmark use cases | Dhrystone | 805.9 |
| | CoreMark | 691.9 |
| Memory use cases | memset | 908.0 |
| | memcpy | 913.9 |
| | Stream | 1222.8 |
| Audio/video playback use cases | Audio playback (gplay) | 458.6 |
| | Audio low-bus playback (gplay) | 255.4 |
| | Video playback local (gplay) | 636.4 |
| | Video playback streaming (gplay) | 664.6 |
| Graphic use case | PXP | 544.0 |
| Machine learning use cases | eIQ benchmark | 725.5 |
| | Machine vision | 780.5 |
| Storage use cases | DD_WRITE_eMMC | 420.4 |
| | DD_READ_eMMC | 644.9 |
| | DD_WRITE_SD | 527.6 |
| | DD_READ_SD | 518.2 |
| Low-power mode use cases | System Idle with display in OD mode with DDRC auto clock gating | 482.5 |
| | System Idle with display in ND mode | 382.0 |
| | System Idle with display in LD mode (DDR to half speed) | 315.2 |
| | System Idle with display in LD mode (DDR to lowest speed with SWFFC) | 275.3 |
| | System Idle without display in OD mode with DDRC auto clock gating | 345.6 |
| | System Idle without display in ND mode with DDRC auto clock gating | 288.1 |
| | System Idle without display in LD mode with DDRC auto clock gating (DDR to half speed) | 227.2 |
| | System Idle without display in LD mode with DDRC auto clock gating (DDR to lowest speed with SWFFC) | 199.9 |
| | System in DSM | 7.6 |
| | Battery | 0.1 |
| Stress test use cases | 2 x A55 Dhrystone + PXP + M33 Core Mark + NPU | 1230.5 |
| | 2 x A55 Stream + PXP + M33 Core Mark + NPU | 1264.1 |
| Product use cases | Linux Suspend + M33 CoreMark (TCM) | 128.2 |
| | Linux Suspend + M33 in WFI | 122.4 |
| | Linux Suspend + M33 FlexCAN Transaction | 132.3 |
| | Smart doorbell | 772.1 |

## 6.1  Core benchmark use cases

The following use cases scenarios have been tested with Cortex A55 cores:

- Dhrystone
- CoreMark

### 6.1.1  Dhrystone

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

#### Table 8. Measurement results for i.MX 93-11x11-EVK_B_Dhrystone_loop (average value)

| Rail label | Average voltage (V) | Average current (mA) | Average power (mW) | Sum of average powers (mW) | Zone 0 die temperature (°C) |
|-----------|---------------------|----------------------|--------------------|---------------------------|-----------------------------|
| lpd4x_vdd1 | 1.8 | 0.6 | 1.1 | GROUP_DRAM: 6.72 | 40.35 |
| GROUP_DRAM lpd4x_vdd2 | 1.1 | 5.1 | 5.6 | | |
| lpd4x_vddq | 0.6 | 0 | 0 | | |
| nvcc_1p8 | 1.8 | 0.3 | 0.6 | | |
| nvcc_3p3 | 3.3 | 3.6 | 12 | | |
| nvcc_bbsm_1p8 | 1.79 | 0.11 | 0.2 | | |
| nvcc_sd2 | 3.3 | 0.9 | 3.1 | | |
| vdd2_ddr | 1.1 | 17.3 | 18.9 | | |
| vdd_ana_0p8 | 0.79 | 16.5 | 13 | | |
| vdd_ana_1p8 | 1.79 | 12.5 | 22.4 | | |
| GROUP_SOC_FULL vdd_soc | 0.89 | 821.2 | 731.4 | 805.87 | |
| vdd_usb_3p3 | 3.3 | 0.03 | 0.1 | | |
| vddq_ddr | 0.6 | 6.8 | 4.1 | | |

### 6.1.2  CoreMark

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

#### Table 9. Measurement results for i.MX 93-11x11-EVK_B_CoreMark_loop (average value)

| Rail label | Average voltage (V) | Average current (mA) | Average power (mW) | Sum of average powers (mW) | Zone 0 die temperature (°C) |
|-----------|---------------------|----------------------|--------------------|---------------------------|-----------------------------|
| GROUP_DRAM lpd4x_vdd1 | 1.8 | 0.44 | 0.8 | 5.91 | 38 |
| lpd4x_vdd2 | 1.1 | 4.7 | 5.2 | | |
| lpd4x_vddq | 0.6 | 0 | 0 | | |
| nvcc_1p8 | 1.8 | 0.56 | 1 | | |
| nvcc_3p3 | 3.3 | 4.1 | 13.4 | | |
| nvcc_bbsm_1p8 | 1.79 | 0.11 | 0.2 | | |
| nvcc_sd2 | 3.3 | 0.9 | 3.1 | | |
| vdd2_ddr | 1.1 | 17.5 | 19.2 | | |
| vdd_ana_0p8 | 0.79 | 16.5 | 13 | | |
| vdd_ana_1p8 | 1.79 | 12.5 | 22.4 | | |
| GROUP_SOC_FULL vdd_soc | 0.89 | 689.8 | 615.5 | 691.85 | |
| vdd_usb_3p3 | 3.3 | 0.03 | 0.1 | | |
| vddq_ddr | 0.6 | 6.7 | 4 | | |

## 6.2  Memory use cases

The following memory-centric use case scenarios have been tested:

- memset
- memcpy
- Stream

The memset and memcpy are part of a perf-bench, which is a general framework for benchmark suites.

### 6.2.1  memset

The memset use case is for evaluating the performance of a simple memory set in various ways.

When the use case is running, the state of the system is as follows:

1. The CPU frequency is set to the maximum value of 1.7 GHz.
2. The DDR data rate is set to 3733 MT/s.
3. The size for the memory buffers is set to 1024 MB.
4. The CM33 is in reset hold, waiting for the reset signal release.

To measure the power consumption of the memset, the steps are as follows:

1. Boot the Linux image with imx93-11x11-evk.dtb.
2. Run setup.sh, see Section 8.
3. Run memset_loop.sh:

```bash
while true; do
  buff_size=`cat /proc/meminfo | grep CmaFree | awk '{print$2}'`
  perf bench -f simple mem memset -l 20000 -s ${buff_size}KB
done
```

4. Measure the power and record the results.

Table 10 shows the measurement results when this use case is applied to the i.MX 93 processor.

#### Table 10. Measurement results for i.MX 93-11x11-EVK_B_memset_loop (average value)

| Rail label | Average voltage (V) | Average current (mA) | Average power (mW) | Sum of average powers (mW) | Zone 0 die temperature (°C) |
|-----------|---------------------|----------------------|--------------------|---------------------------|-----------------------------|
| lpd4x_vdd1 | 1.8 | 3.4 | 6 | | |
| lpd4x_vdd2 | 1.09 | 60.2 | 65.8 | | |
| GROUP_DRAM lpd4x_vddq | 0.6 | 0 | 0 | 71.77 | |
| nvcc_1p8 | 1.8 | 0.28 | 0.5 | | |
| nvcc_3p3 | 3.3 | 3.7 | 12.3 | | |
| nvcc_bbsm_1p8 | 1.79 | 0.11 | 0.2 | | |
| nvcc_sd2 | 3.3 | 0.9 | 3.1 | | |
| vdd2_ddr | 1.09 | 44.4 | 48.5 | | |
| vdd_ana_0p8 | 0.79 | 16.6 | 13.1 | | |
| vdd_ana_1p8 | 1.79 | 12.5 | 22.4 | | |
| GROUP_SOC_FULL vdd_soc | 0.89 | 863.2 | 768.6 | 907.97 | 41 |
| vdd_usb_3p3 | 3.3 | 0.06 | 0.2 | | |
| vddq_ddr | 0.59 | 66.2 | 39.2 | | |

### 6.2.2  memcpy

The memcpy use case is for evaluating the performance of a simple memory copy in various ways.

When the use case is running, the state of the system is as follows:

1. The CPU frequency is set to the maximum value of 1.7 GHz.
2. The DDR data rate is set to 3733 MT/s.
3. The size for the memory buffers is set to 1024 MB.
4. The CM33 is in reset hold, waiting for the reset signal release.

To measure the power consumption of memcpy, the steps are as follows:

1. Boot the Linux image with imx93-11x11-evk.dtb.
2. Run setup.sh, see Section 8.
3. Run memcpy_loop.sh:

```bash
while true; do
  buff_size=`cat /proc/meminfo | grep CmaFree | awk '{print$2}'`
  perf bench -f simple mem memcpy -l 20000 -s ${buff_size}KB
done
```

4. Measure the power and record the results.

Table 11 shows the measurement results when this use case is applied to the i.MX 93 processor.

#### Table 11. Measurement results for i.MX 93-11x11-EVK_B_memcpy_loop (average value)

| Rail label | Average voltage (V) | Average current (mA) | Average power (mW) | Sum of average powers (mW) | Zone 0 die temperature (°C) |
|-----------|---------------------|----------------------|--------------------|---------------------------|-----------------------------|
| lpd4x_vdd1 | 1.79 | 3.7 | 6.7 | | |
| lpd4x_vdd2 | 1.09 | 73.8 | 80.4 | | |
| GROUP_DRAM lpd4x_vddq | 0.6 | 4.8 | 2.8 | 89.93 | |
| nvcc_1p8 | 1.8 | 0.17 | 0.3 | | |
| nvcc_3p3 | 3.3 | 3.7 | 12.3 | | |
| nvcc_bbsm_1p8 | 1.79 | 0.11 | 0.2 | | |
| nvcc_sd2 | 3.3 | 0.9 | 3.1 | | |
| vdd2_ddr | 1.09 | 41.1 | 45 | | |
| vdd_ana_0p8 | 0.79 | 16.6 | 13.1 | | |
| vdd_ana_1p8 | 1.79 | 12.4 | 22.3 | | |
| GROUP_SOC_FULL vdd_soc | 0.89 | 905.7 | 805.8 | 913.93 | 41 |
| vdd_usb_3p3 | 3.3 | 0.06 | 0.2 | | |
| vddq_ddr | 0.6 | 19.7 | 11.7 | | |

### 6.2.3  Stream

The stream benchmark is a simple synthetic benchmark program that measures the sustainable memory bandwidth (in MB/s) and the corresponding computation rate for simple vector kernels.

When the use case is running, the state of the system is as follows:

1. The CPU frequency is set to the maximum value of 1.7 GHz.
2. The DDR data rate is set to 3733 MT/s.
3. All phases, such as Copy, Scale, Add, and Triad, are included.
4. The CM33 is in reset hold, waiting for the reset signal release.

To measure the power consumption of the stream, the steps are as follows:

1. Boot the Linux image with imx93-11x11-evk.dtb.
2. Run setup.sh, see Section 8.
3. Run streamcpy_loop.sh:

```bash
while [ "1" == "1" ]; do
  taskset -c 0 stream -M 200M -N 1000 & 
  taskset -c 1 stream -M 200M -N 1000
done
```

4. Measure the power and record the results.

Table 12 shows the measurement results when this use case is applied to the i.MX 93 processor.

#### Table 12. Measurement results for i.MX 93-11x11-EVK_B_stream_loop (average value)

| Rail label | Average voltage (V) | Average current (mA) | Average power (mW) | Sum of average powers (mW) | Zone 0 die temperature (°C) |
|-----------|---------------------|----------------------|--------------------|---------------------------|-----------------------------|
| GROUP_DRAM lpd4x_vdd1 | 1.79 | 4.9 | 8.8 | 109.65 | 45 |
| lpd4x_vdd2 | 1.09 | 87.1 | 94.9 | | |
| lpd4x_vddq | 0.6 | 10 | 6 | | |
| nvcc_1p8 | 1.8 | 0.11 | 0.2 | | |
| nvcc_3p3 | 3.3 | 3.8 | 12.5 | | |
| nvcc_bbsm_1p8 | 1.79 | 0.11 | 0.2 | | |
| nvcc_sd2 | 3.3 | 0.9 | 3.1 | | |
| vdd2_ddr | 1.09 | 50.7 | 55.5 | | |
| vdd_ana_0p8 | 0.79 | 16.8 | 13.2 | | |
| vdd_ana_1p8 | 1.79 | 12.4 | 22.3 | | |
| GROUP_SOC_FULL vdd_soc | 0.89 | 1241.6 | 1100.4 | 1222.81 | |
| vdd_usb_3p3 | 3.3 | 0.03 | 0.1 | | |
| vddq_ddr | 0.6 | 25.6 | 15.2 | | |

## 6.3  Audio/video playback use cases

The following audio use case scenarios have been tested:

- Audio playback (gplay)
- Audio low-bus playback (gplay)
- Video playback local (gplay)
- Video playback streaming (gplay)

### 6.3.1  Audio playback (gplay)

For this use case, the audio file is an MP3 file with a 128 kbit/s bit rate and a 44 kHz sample rate. CA55 handles audio decoding, I2S, and audio codec.

When the use case is running, the state of the system is as follows:

1. The CPU frequency is set to the maximum value of 1.7 GHz.
2. The DDR data rate is set to 3733 MT/s.
3. The CM33 is in reset hold, waiting for the reset signal release.

To measure the power consumption of the audio playback, the steps are as follows:

1. Boot the Linux image with imx93-11x11-evk.dtb.
2. Run setup.sh, see Section 8.
3. Run gplay_audio.sh:

```bash
gplay-1.0 Mpeg1L3_44kHz_128kbps_s_Ed_Rush_Sabotage_mplayer.mp3 
```

**Note:** Prepare your own MP3 file. To obtain similar results in this document, ensure that the audio bit rate is about 128 kbit/s.

4. Measure the power and record the results.

**Note:**

If there is no sound, use the following command to query and set the sound card:

```bash
pacmd list-sinks
pacmd set-default-sink $index #Select the item index with the wm8962 keyword
```

Table 13 shows the measurement results when this use case is applied to the i.MX 93 processor.

#### Table 13. Measurement results for i.MX 93-11x11-EVK_B_gplay_audio-default (average value)

| Rail label | Average voltage (V) | Average current (mA) | Average power (mW) | Sum of average powers (mW) | Zone 0 die temperature (°C) |
|-----------|---------------------|----------------------|--------------------|---------------------------|-----------------------------|
| lpd4x_vdd1 | 1.8 | 1 | 1.8 | | |
| lpd4x_vdd2 | 1.1 | 8.9 | 9.7 | | |
| GROUP_DRAM lpd4x_vddq | 0.6 | 0.5 | 0.3 | 11.76 | |
| nvcc_1p8 | 1.8 | 0.17 | 0.3 | | |
| nvcc_3p3 | 3.3 | 6.2 | 20.4 | | |
| nvcc_bbsm_1p8 | 1.79 | 0.11 | 0.2 | | |
| nvcc_sd2 | 3.3 | 0.9 | 3.1 | | |
| vdd2_ddr | 1.1 | 17.8 | 19.5 | | |
| vdd_ana_0p8 | 0.79 | 20.2 | 15.9 | | |
| vdd_ana_1p8 | 1.79 | 13.7 | 24.5 | | |
| GROUP_SOC_FULL vdd_soc | 0.89 | 414.1 | 370.5 | 458.63 | 34 |
| vdd_usb_3p3 | 3.3 | 0.06 | 0.2 | | |
| vddq_ddr | 0.6 | 6.8 | 4.1 | | |

### 6.3.2  Audio low-bus playback (gplay)

For this use case, the audio file is a WAV file with a 24 bit and a 32 kHz sample rate. CA55 handles audio decoding, I2S, and audio codec.

When the use case is running, the state of the system is as follows:

1. The CPU frequency is set to 1.4 GHz.
2. The DDR data rate is set to 625 MT/s.
3. The CM33 is in reset hold, waiting for the reset signal release.

To measure the power consumption of the audio low-bus playback, the steps are as follows:

1. Boot the Linux image with imx93-11x11-evk-ld.dtb.
2. Run DDRC_625MTS_setup.sh (625 MT/s data rate), see Section 8.
3. Run gplay_audio.sh:

```bash
gplay-1.0 Mpeg1L3_44kHz_128kbps_s_Ed_Rush_Sabotage_mplayer.mp3
```

**Note:** Prepare your own MP3 file. To obtain similar results in this document, ensure that the audio bit rate is about 128 kbit/s.

4. Measure the power and record the results.

Table 14 shows the measurement results when this use case is applied to the i.MX 93 processor.

#### Table 14. Measurement results for i.MX 93-11x11-EVK_B_audio_low_power_50 MHz (average value)

| Rail label | Average voltage (V) | Average current (mA) | Average power (mW) | Sum of average powers (mW) | Zone 0 die temperature (°C) |
|-----------|---------------------|----------------------|--------------------|---------------------------|-----------------------------|
| lpd4x_vdd1 | 1.8 | 1.3 | 2.4 | | |
| lpd4x_vdd2 | 1.1 | 7.7 | 8.4 | | |
| GROUP_DRAM lpd4x_vddq | 0.6 | 2.5 | 1.5 | 12.25 | |
| nvcc_1p8 | 1.8 | 0.22 | 0.4 | | |
| nvcc_3p3 | 3.3 | 6.2 | 20.6 | | |
| nvcc_bbsm_1p8 | 1.79 | 0.11 | 0.2 | | |
| nvcc_sd2 | 3.3 | 0.9 | 3.1 | | |
| vdd2_ddr | 1.1 | 4.7 | 5.1 | | |
| vdd_ana_0p8 | 0.79 | 20.2 | 15.9 | | |
| vdd_ana_1p8 | 1.79 | 9.9 | 17.7 | | |
| GROUP_SOC_FULL vdd_soc | 0.8 | 235.1 | 187.6 | 255.39 | 30 |
| vdd_usb_3p3 | 3.3 | 0.06 | 0.2 | | |
| vddq_ddr | 0.6 | 7.9 | 4.7 | | |

### 6.3.3  Video playback local (gplay)

For this use case, the i.MX 93 EVK board is connected to an HDMI display through the MIPI-to-HDMI converter card (IMX-MIPI-HDMI).

The video file used for playback is an MP4 file format compressed using the H.264 480 p resolution at 24 frames per second (fps). The audio encoding is AACL with a 44.1 kHz sample rate in a two-channel configuration.

**Note:** In this SoC, there is no hardware decoder, so a software decoder is used.

When the use case is running, the state of the system is as follows:

1. The CPU frequency is set to the maximum value of 1.7 GHz.
2. The DDR data rate is set to 3733 MT/s.
3. The CM33 is in reset hold, waiting for the reset signal release.

To measure the power consumption of video playback local, the steps are as follows:

1. Connect the HDMI display to the board through the MIPI-to-HDMI converter card (IMX-MIPI-HDMI).
2. Boot the Linux image with imx93-11x11-evk.dtb.
3. To put the system into Idle mode, run setup_video.sh. See Section 8.
4. Run gplay_videoplayback.sh:

```bash
gplay-1.0 ./480p24.mp4
```

**Note:** Prepare your own MP4 file. To obtain similar results, ensure that this file is 480 p with a 24-frame rate, bit rate of about 1200 kbit/s, and encoded in H.264 format.

5. Measure the power and record the results.

Table 15 shows the measurement results when this use case is applied to the i.MX 93 processor.

#### Table 15. Measurement results for i.MX 93-11x11-EVK_B_ gplay_videoplayback (average value)

| Rail label | Average voltage (V) | Average current (mA) | Average power (mW) | Sum of average powers (mW) | Zone 0 die temperature (°C) |
|-----------|---------------------|----------------------|--------------------|---------------------------|-----------------------------|
| lpd4x_vdd1 | 1.79 | 2.9 | 5.2 | | |
| lpd4x_vdd2 | 1.09 | 44.3 | 48.3 | | |
| GROUP_DRAM lpd4x_vddq | 0.6 | 5.7 | 3.4 | 56.85 | |
| nvcc_1p8 | 1.79 | 0 | 0.7 | | |
| nvcc_3p3 | 3.3 | 6.3 | 20.9 | | |
| nvcc_bbsm_1p8 | 1.79 | 0.11 | 0.2 | | |
| nvcc_sd2 | 3.3 | 0.9 | 3.1 | | |
| vdd2_ddr | 1.09 | 25.4 | 27.8 | | |
| vdd_ana_0p8 | 0.78 | 34.4 | 26.8 | | |
| vdd_ana_1p8 | 1.78 | 23 | 41 | | |
| GROUP_SOC_FULL vdd_soc | 0.89 | 569.7 | 508.7 | 636.4 | 37 |
| vdd_usb_3p3 | 3.3 | 0.06 | 0.2 | | |
| vddq_ddr | 0.6 | 11.8 | 7 | | |

### 6.3.4  Video playback streaming (gplay)

For this use case, the i.MX 93 EVK board is connected to an HDMI display through the MIPI-to-HDMI converter card (IMX-MIPI-HDMI).

The video file used for playback is streamed through HTTP. An MP4 file format compressed using the H.264 480 p resolution at 24 fps. The audio encoding is AACL with a 44.1 kHz sample rate in a two-channel configuration.

When the use case is running, the state of the system is as follows:

1. The CPU frequency is set to the maximum value of 1.7 GHz.
2. The DDR data rate is set to 3733 MT/s