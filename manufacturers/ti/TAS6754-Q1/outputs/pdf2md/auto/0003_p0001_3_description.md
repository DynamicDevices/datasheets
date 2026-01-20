# 3 Description

The TAS6754-Q1 is a four-channel digital-input Class-D audio amplifier that implements 1L modulation only requiring one inductor per BTL channel reducing system size and cost by removing four inductors compared to a traditional design. Additionally, 1L modulation lowers switching losses compared to traditional Class-D modulation schemes.

The TAS6754-Q1 integrates DC and AC Load Diagnostics to determine the status of the connected loads. During audio playback this status can be monitored through output current sense which is available for each channel and reports the measurement to a host processor through TDM with minimal delay. The device monitors the output load condition while playing audio through real-time load diagnostics independent of the host and audio input.

The TAS6754-Q1 device features an additional low latency signal path for each channel, providing up to 70% faster signal processing at 48kHz which enables time-sensitive Active Noise Cancellation (ANC), Road Noise Cancellation (RNC) applications.

The device supports global temperature, channel temperature and PVDD values via I²C readout for easy system level thermal management.

The device is offered in a 56 pin HSSOP package with the exposed thermal pad up.

## Device Information

| PART NUMBER | PACKAGE⁽¹⁾ | PACKAGE SIZE⁽²⁾ |
|-------------|-----------|------------------|
| TAS6754-Q1 | HSSOP (56) | 18.42mm × 10.35mm |

(1) For all available packages, see the orderable addendum at the end of the data sheet.

(2) The package size (length × width) is a nominal value and includes pins, where applicable.

## Simplified Channel Schematic

![Figure: 1L Modulation Channel Schematic](./images/page_1_diagram.png)

**1L Modulation Channel Schematic Description:**

The diagram illustrates the simplified channel architecture of the TAS6754-Q1 showing the key advantage of 1L modulation. The schematic shows:

- **PVDD** power supply connection at the top
- **OUTP** (positive output) and **OUTM** (negative output) terminals forming a bridge-tied load (BTL) configuration
- **Only 1 inductor needed per channel** - A single inductor is placed in the output path, highlighted as the primary benefit of this architecture
- The schematic demonstrates how the 1L modulation eliminates the need for four additional inductors compared to traditional Class-D designs
- A capacitor is shown in the output filter network
- The speaker/load is connected between OUTP and OUTM

This simplified schematic emphasizes the cost and space-saving benefits of the 1L modulation approach, requiring only one inductor per BTL channel instead of the multiple inductors typically required in conventional Class-D amplifier designs.

---

## Verbatim tables

<!-- VERBATIM_TABLE_START -->
![Table (page 1)](./images/page_1_table_1.png)

|PART NUMBER|PACKAGE(1)|PACKAGE SIZE(2)|
|---|---|---|
|TAS6754-Q1|HSSOP (56)|18.42mm × 10.35mm|
<!-- VERBATIM_TABLE_END -->
