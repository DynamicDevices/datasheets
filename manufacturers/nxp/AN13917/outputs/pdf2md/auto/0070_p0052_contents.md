# Contents

## 1. Introduction
Page 2

## 2. Acronyms
Page 2

## 3. i.MX 93 power architecture
Page 4

## 4. i.MX 93 power overview
Page 5

### 4.1 i.MX 93 power domains overview
Page 5

### 4.2 i.MX 93 power mode overview
Page 6

#### 4.2.1 Low-power modes
Page 7

## 5. i.MX 93 processor power measurement
Page 8

### 5.1 Hardware and software requirements
Page 8

### 5.2 Build the i.MX Yocto Project
Page 8

### 5.3 Power consumption measurement
Page 9

## 6. Use cases and measurement results
Page 9

### 6.1 Core benchmark use cases
Page 11

#### 6.1.1 Dhrystone
Page 11

#### 6.1.2 CoreMark
Page 12

### 6.2 Memory use cases
Page 13

#### 6.2.1 memset
Page 13

#### 6.2.2 memcpy
Page 14

#### 6.2.3 Stream
Page 15

### 6.3 Audio/video playback use cases
Page 16

#### 6.3.1 Audio playback (gplay)
Page 16

#### 6.3.2 Audio low-bus playback (gplay)
Page 17

#### 6.3.3 Video playback local (gplay)
Page 18

#### 6.3.4 Video playback streaming (gplay)
Page 19

### 6.4 Graphic use case
Page 20

### 6.5 Machine learning use cases
Page 21

#### 6.5.1 eIQ benchmark
Page 21

#### 6.5.2 Machine vision
Page 22

### 6.6 Storage use cases
Page 23

#### 6.6.1 DD_WRITE_eMMC
Page 23

#### 6.6.2 DD_READ_eMMC
Page 24

#### 6.6.3 DD_WRITE_SD
Page 25

#### 6.6.4 DD_READ_SD
Page 26

### 6.7 Low-power mode use cases
Page 27

#### 6.7.1 System Idle with display in OD mode with DDRC auto clock gating
Page 27

#### 6.7.2 System Idle with display in ND mode
Page 28

#### 6.7.3 System Idle with display in LD mode (DDR to half speed)
Page 29

#### 6.7.4 System Idle with display in LD mode (DDR to lowest speed with SWFFC)
Page 30

#### 6.7.5 System Idle without display in OD mode with DDRC auto clock gating
Page 30

#### 6.7.6 System Idle without display in ND mode with DDRC auto clock gating
Page 31

#### 6.7.7 System Idle without display in LD mode with DDRC auto clock gating (DDR to half speed)
Page 32

#### 6.7.8 System Idle without display in LD mode with DDRC auto clock gating (DDR to lowest speed with SWFFC)
Page 33

#### 6.7.9 System in DSM
Page 34

#### 6.7.10 Battery
Page 35

### 6.8 Stress test use cases
Page 36

#### 6.8.1 2 x CA55 Dhrystone + PXP + CM33 CoreMark + NPU
Page 36

#### 6.8.2 2 x CA55 Stream + PXP + CM33 CoreMark + NPU
Page 37

### 6.9 Product use cases
Page 38

#### 6.9.1 Linux Suspend + CM33 CoreMark (TCM)
Page 38

#### 6.9.2 Linux Suspend + CM33 in wait for interrupt
Page 39

#### 6.9.3 Linux Suspend + CM33 FlexCAN transaction
Page 40

#### 6.9.4 Smart doorbell
Page 41

## 7. Reducing power consumption
Page 42

### 7.1 Run fast and idle
Page 43

### 7.2 Clock gating
Page 43

### 7.3 DDRC auto clock gating
Page 44

### 7.4 PLL reduction
Page 44

### 7.5 Core VFS and system bus scaling
Page 44

### 7.6 Lower DDR frequencies
Page 44

### 7.7 DDR interface optimization
Page 44

### 7.8 Power gating of PHYs
Page 45

### 7.9 Distribution of workloads
Page 45

### 7.10 Use OCRAM to minimize DDR access
Page 45

### 7.11 Thermal management to reduce leakage
Page 45

### 7.12 Nominal drive mode
Page 45

## 8. Important commands
Page 45

## 9. Note about the source code in the document
Page 48

## 10. Revision history
Page 49

---

## Legal information
Page 50

**Please be aware that important notices concerning this document and the product(s) described herein, have been included in section 'Legal information'.**

© 2024 NXP B.V.  
All rights reserved.

For more information, please visit: https://www.nxp.com

**Date of release:** 29 February 2024  
**Document identifier:** AN13917