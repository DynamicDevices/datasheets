# 8  Important commands

Before running a use case, the `<configuration_script>.sh` script must be run to configure the environment. Details for these scripts are as follows:

## setup.sh

The CPU frequency is set to the maximum value of 1.7 GHz to achieve the best performance. Disable the Ethernet, stop the Weston service, and blank the display. Set 512 kB as the maximum amount of data the kernel reads ahead for a single file.

```bash
#!/bin/bash
systemctl stop weston.service 
echo 1 > /sys/class/graphics/fb0/blank 
partitions=`lsblk |awk '$1 !~/-/{print $1}' |grep 'blk\|sd'` 
for partition in $partitions; do
  echo 512 > /sys/block/$partition/queue/read_ahead_kb 
done
eth_int=`ifconfig -a | grep 'eth[0-9]'|awk {'print substr($1, 0, 4)'}`
for eth in $eth_int; do
  ifconfig $eth down
done
```

## setup_video.sh

The CPU frequency is set to the maximum value of 1.7 GHz to achieve the best performance. Disable the Ethernet and awake the display. Set 512 kB as the maximum amount of data the kernel reads ahead for a single file.

```bash
#!/bin/bash
partitions=`lsblk |awk '$1 !~/-/{print $1}' |grep 'blk\|sd'`
for partition in $partitions; do
  echo 512 > /sys/block/$partition/queue/read_ahead_kb 
done
eth_int=`ifconfig -a | grep 'eth[0-9]'|awk {'print substr($1, 0, 4)'}`
for eth in $eth_int; do
  ifconfig $eth down
done
echo 1 > /sys/class/graphics/fb0/blank
echo 0 > /sys/class/graphics/fb0/blank
```

## setup_video_stream.sh

The CPU frequency is set to the maximum value of 1.7 GHz to achieve the best performance. To play the video online, open the Ethernet and awake the display. Set 512 kB as the maximum amount of data the kernel reads ahead for a single file.

```bash
#!/bin/bash
partitions=`lsblk |awk '$1 !~/-/{print $1}' |grep 'blk\|sd'`
for partition in $partitions; do
  echo 512 > /sys/block/$partition/queue/read_ahead_kb
done
eth_int=`ifconfig -a | grep 'eth[0-9]'|awk {'print substr($1, 0, 4)'}`
for eth in $eth_int;do
  ifconfig $eth up
done
echo 1 > /sys/class/graphics/fb0/blank
echo 0 > /sys/class/graphics/fb0/blank
```

## DDRC_625MTS_setup.sh

After running the shell scripts below, the DDR frequency switches to Low-bus mode 312.5 MHz (data rate is 625 MT/s). The CPU frequency is set to the minimum value of 1400 MHz. DDR VFS aims at saving power. Disable the Ethernet, stop the Weston service, and blank the display.

```bash
#!/bin/bash
systemctl stop weston.service
if [ -f /sys/class/graphics/fb0/blank ]; then
  echo 1 > /sys/class/graphics/fb0/blank
fi
eth_int=`ifconfig -a | grep 'eth[0-9]'|awk {'print substr($1, 0, 4)'}`
for eth in $eth_int; do
  ifconfig $eth down
done
echo 3 > /sys/devices/platform/imx93-lpm/mode
```

## dd_read.sh

This script is used to run the dd read command on the memory device.

```bash
#!/bin/bash
# Since we're dealing with dd, abort if any errors occur
set -e
TEST_FILE=${1:-dd_ibs_testfile}
if [ $EUID -ne 0 ]; then
echo "NOTE: Kernel cache will not be cleared between tests without sudo. This will
 likely cause inaccurate results." 1>&2 ;fi
count=$COUNT conv=fsync > /dev/null 2>&1
# Header
PRINTF_FORMAT="%8s : %s\n"
printf "$PRINTF_FORMAT" 'block size' 'transfer rate'
while true
BLOCK_SIZE=4096
do
# Clear kernel cache to ensure more accurate test
[ $EUID -eq 0 ] && [ -e /proc/sys/vm/drop_caches ] && echo 3 > /proc/sys/vm/drop_caches
# Read test file out to /dev/null with specified block size
DD_RESULT=$(dd if=$TEST_FILE of=/dev/null bs=$BLOCK_SIZE 2>&1 1>/dev/null)
# Extract transfer rate
TRANSFER_RATE=$(echo $DD_RESULT | \grep --only-matching -E '[0-9.]+ ([MGk]?B|bytes)/
s(ec)?')
printf "$PRINTF_FORMAT" "$BLOCK_SIZE" "$TRANSFER_RATE"
done
```

## dd_write.sh

This script is used to run the dd write command on the memory device.

```bash
#!/bin/bash
# Since we're dealing with dd, abort if any errors occur
set -e
TEST_FILE=${1:-dd_obs_testfile}
TEST_FILE_EXISTS=0
if [ -e "$TEST_FILE" ]; then TEST_FILE_EXISTS=1; fi
TEST_FILE_SIZE=1024000000
if [ $EUID -ne 0 ]; then
echo "NOTE: Kernel cache will not be cleared between tests without sudo. This will
 likely cause inaccurate results." 1>&2
fi
# Header
PRINTF_FORMAT="%8s: %s\n"
printf "$PRINTF_FORMAT" 'block size' 'transfer rate'
while true
BLOCK_SIZE=4096
do
# Calculate number of segments required to copy
COUNT=$(($TEST_FILE_SIZE / $BLOCK_SIZE))
if [ $COUNT -le 0 ]; then
echo "Block size of $BLOCK_SIZE estimated to require $COUNT blocks, aborting further
 tests."
break
fi
# Clear kernel cache to ensure more accurate test
[ $EUID -eq 0 ] && [ -e /proc/sys/vm/drop_caches ] && echo 3 > /proc/sys/vm/drop_caches
# Create a test file with the specified block size
DD_RESULT=$(dd if=/dev/zero of=$TEST_FILE bs=$BLOCK_SIZE count=$COUNT conv=fsync 2>&1
 1>/dev/null)
# Extract the transfer rate from dd's STDERR output
TRANSFER_RATE=$(echo $DD_RESULT | \grep --only-matching -E '[0-9.]+ ([MGk]?B|bytes)/
s(ec)?')
# Output the result
printf "$PRINTF_FORMAT" "$BLOCK_SIZE" "$TRANSFER_RATE"
done
```

## dhrystone_loop.sh

The script starts the Dhrystone example:

```bash
while true; do
 taskset -c 0 ./dhry2 & 
 taskset -c 1 ./dhry2
done
```

## ML_vela.sh

The script starts the machine learning example:

```bash
#!/bin/bash
```