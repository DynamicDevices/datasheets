# Contents

## 1 Introduction ......................................................2

## 2 Acronyms ......................................................... 2

## 3 i.MX 93 power architecture .............................4

## 4 i.MX 93 power overview ..................................5

### 4.1 i.MX 93 power domains overview ......................5

### 4.2 i.MX 93 power mode overview .......................... 6

#### 4.2.1 Low-power modes ............................................. 7

## 5 i.MX 93 processor power measurement ........ 8

### 5.1 Hardware and software requirements ................8

### 5.2 Build the i.MX Yocto Project .............................. 8

### 5.3 Power consumption measurement .................... 9

## 6 Use cases and measurement results .............9

### 6.1 Core benchmark use cases .............................11

#### 6.1.1 Dhrystone .........................................................11

#### 6.1.2 CoreMark ......................................................... 12

### 6.2 Memory use cases .......................................... 13

#### 6.2.1 memset ............................................................ 13

#### 6.2.2 memcpy ........................................................... 14

#### 6.2.3 Stream ............................................................. 15

### 6.3 Audio/video playback use cases ......................16

#### 6.3.1 Audio playback (gplay) .................................... 16

#### 6.3.2 Audio low-bus playback (gplay) .......................17

#### 6.3.3 Video playback local (gplay) ............................18

#### 6.3.4 Video playback streaming (gplay) ....................19

### 6.4 Graphic use case ............................................ 20

### 6.5 Machine learning use cases ............................21

#### 6.5.1 eIQ benchmark ................................................ 21

#### 6.5.2 Machine vision .................................................22

### 6.6 Storage use cases ...........................................23

#### 6.6.1 DD_WRITE_eMMC ..........................................23

#### 6.6.2 DD_READ_eMMC ........................................... 24

#### 6.6.3 DD_WRITE_SD ............................................... 25

#### 6.6.4 DD_READ_SD .................................................26

### 6.7 Low-power mode use cases ............................27

#### 6.7.1 System Idle with display in OD mode with DDRC auto clock gating ..................................27

#### 6.7.2 System Idle with display in ND mode .............. 28

#### 6.7.3 System Idle with display in LD mode (DDR to half speed) .................................................. 29

#### 6.7.4 System Idle with display in LD mode (DDR to lowest speed with SWFFC) ......................... 30

#### 6.7.5 System Idle without display in OD mode with DDRC auto clock gating ...........................30

#### 6.7.6 System Idle without display in ND mode with DDRC auto clock gating ...........................31

#### 6.7.7 System Idle without display in LD mode with DDRC auto clock gating (DDR to half speed) ..............................................................32

#### 6.7.8 System Idle without display in LD mode with DDRC auto clock gating (DDR to lowest speed with SWFFC) ............................. 33

#### 6.7.9 System in DSM ................................................34

#### 6.7.10 Battery ..............................................................35

### 6.8 Stress test use cases ...................................... 36

#### 6.8.1 2 x CA55 Dhrystone + PXP + CM33 CoreMark + NPU .............................................36

#### 6.8.2 2 x CA55 Stream + PXP + CM33 CoreMark + NPU ..............................................................37

### 6.9 Product use cases ...........................................38

#### 6.9.1 Linux Suspend + CM33 CoreMark (TCM) ........38

#### 6.9.2 Linux Suspend + CM33 in wait for interrupt ..... 39

#### 6.9.3 Linux Suspend + CM33 FlexCAN transaction ....................................................... 40

#### 6.9.4 Smart doorbell ................................................. 41

## 7 Reducing power consumption ..................... 42

### 7.1 Run fast and idle ............................................. 43

### 7.2 Clock gating .....................................................43

### 7.3 DDRC auto clock gating ..................................44

### 7.4 PLL reduction .................................................. 44

### 7.5 Core VFS and system bus scaling .................. 44

### 7.6 Lower DDR frequencies .................................. 44

### 7.7 DDR interface optimization ..............................44

### 7.8 Power gating of PHYs ..................................... 45

### 7.9 Distribution of workloads ................................. 45

### 7.10 Use OCRAM to minimize DDR access ............45

### 7.11 Thermal management to reduce leakage ........ 45

### 7.12 Nominal drive mode ........................................ 45

## 8 Important commands .................................... 45

## 9 Note about the source code in the document ........................................................48

## 10 Revision history .............................................49

## Legal information ...........................................50

---

**Document Information:**

Please be aware that important notices concerning this document and the product(s) described herein, have been included in section 'Legal information'.

© 2024 NXP B.V.  
All rights reserved.

For more information, please visit: https://www.nxp.com

Date of release: 29 February 2024  
Document identifier: AN13917