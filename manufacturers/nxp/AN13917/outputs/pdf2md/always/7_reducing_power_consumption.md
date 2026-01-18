# 7 Reducing power consumption

The overall system power consumption depends on the software optimization and the system hardware implementation. The following list of suggestions can help reduce system power consumption. Some of these suggestions are already implemented in the Linux BSP and/or SDK. The system of each individual user can undergo further optimizations.

*Note: Further power optimizations are planned in future software releases. To obtain the latest software releases, refer i.MX Software and Development Tools.*

• Apply clock gating by configuring registers in the CCM, whenever clocks or modules are not used.
• For Run modes, use the slowest frequency that can still meet the application requirements.
• Minimize the number of operating PLLs. Enabled PLLs can consume a few milliamps of current.
• Applying voltage and frequency scaling (VFS) for the Arm cores and scaling the frequencies of the AXI, AHB, and IPG bus clocks can significantly reduce power consumption. However, the operation frequency reduction causes longer access times to the DDR, which increases the power consumption of the DDR I/O and memories. Consider this trade-off for each mode to quantify the overall effect on system power.
• Put the SoC into Low-power modes whenever possible, as long as it can still support the application requirements. Consider the following example:
  - Put the system into Suspend mode when it can enter deep sleep.
  - Put the system into Low-power run mode by only using the CM33 core.
  - Power off the CA55 cores and other domains for low-load use cases.
• For each operating mode, use the lowest voltage (with the power supply tolerance) that can still meet the requirements of voltage specifications in the data sheet.
• DDR interface optimization:
  - Use careful board routing of the DDR memories, maintaining PCB trace lengths as short as possible.
  - Use the proper output driver impedance for DDR interface pins that provides good impedance matching. To save current through DDR I/O pins, select the lowest possible drive strength that provides the required performance.
  - Use of LPDDR4/LPDDR4x memory offerings in the latest process technology can significantly reduce the power consumption of the DDR devices and the DDR I/O.

The following sections provide more details for system optimization. These sections are not exhaustive lists of features that can provide power reductions, but they are the easiest and most common ones.

• Run fast and idle
• Clock gating
• DDRC auto clock gating
• PLL reduction
• Core VFS and system bus scaling
• Lower DDR frequencies
• DDR interface optimization
• Power gating of PHYs
• Distribution of workloads
• Use OCRAM to minimize DDR access
• Thermal management to reduce leakage
• Nominal drive mode

## 7.1 Run fast and idle

NXP testing and various research have shown that for most customer use cases, the best power/energy management protocol is to run the cores at maximum speeds for the workload and then drop to the lowest power mode as soon as possible. This strategy cannot provide optimal energy savings for the use cases where constant data is being processed, for example, low-latency audio playback. However, this strategy does work for other standard workloads. Consider this trade-off for each application to quantify the overall effect on the system power/energy consumption.

Users must place the i.MX 93 into the Low-power mode as far as possible.

## 7.2 Clock gating

The CCM inside the i.MX 93 provides a programmable method to disable the clock sources for modules when the modules are not used. To reduce energy waste, always configure the CCM registers. Driving any inactive signal, whether on the SoC or the PCB, is simply charging and discharging the line and the load capacitance of this signal. The NXP BSP-released software implements clock gating by default.

## 7.3 DDRC auto clock gating

When the bus is idle after the number of cycles configured in the `ssi_idle_strap` field in the DDR BLK_CTRL module, the DDRC does auto clock gating to save power. This feature can be used to balance DDR subsystem performance and power significantly. The number of idle cycles before clock gating can be adjusted dynamically based on the actual use case to fine-tune the power saving.

In the i.MX 93, auto_clk_gating is used to enable the DDRC auto clock gating. Therefore, power is saved when there is no access to the DDR after the programmed idle count expires. "Write 0" disables the auto clock gating and the "write non-zero" value sets the `ssi_idle_strip` to this non-zero value and enable the auto clock gating. A value < 256 has some significant side effort for DDR performance, so a value >=256 is suggested when the user wants to enable it. When the auto clock gating is enabled, a high-resolution display like 1080 P 60 fps can flicker at lower DDR frequency. It is recommended not to adjust the auto_clk_gating when the display/NPU is running.

## 7.4 PLL reduction

Each PLL block consumes significant energy when active. Each application has unique requirements, but, if possible, reduce the number of operating PLLs. The CCM within the i.MX 93 provides Root Clock mux and programmable control to each PLL either by direct control mode or CPU Low-power mode. As a result, the Root Clocks source is allowed to modify to limit the PLL source and reduce the number of active PLLs when operating. Ensure that the application considers the PLL relock time when transitioning back to full operation.

## 7.5 Core VFS and system bus scaling

Applying VFS for the Arm cores and scaling (not dynamic) the frequencies of the NOC, AXI, AHB, and IPG system bus clocks can significantly reduce the power consumption of the VDD_SOC domains. However, the operation of system frequency reduction causes longer access times to the DDR, which can increase the energy consumption for specific use cases. Consider this trade-off for each mode to quantify the overall effect on the system power consumption.

## 7.6 Lower DDR frequencies

As explained previously, the DDR I/O bus frequency also contributes to the DDR I/O current. Software interfaces allow for the use of the HWFFC/SWFFC technology of DDRC, which allows for the significant reduction of power consumption by lowering the DDR frequency.

## 7.7 DDR interface optimization

To optimize the DDR interface, the suggestions are as follows:

• Employ careful board routing of the DDR memories, maintaining the PCB trace lengths as short as possible. Longer trace lengths and more vias create more PCB capacitance for the signal, resulting in more energy wastage along the signal path.
• Keep the on-die termination (ODT) value as low as possible. The termination used greatly influences the power consumption of the DDR interface pins. To ensure the ODT variance does not reduce the bus signal integrity, simulate the DDR interface.
• Use an appropriate output driver impedance for the DDR interface pins that provide good impedance matching. Select the lowest possible drive strength that provides the required performance to reduce the current flowing through the DDR I/O pins. Remember that simulation must be done to ensure signal integrity.