I have  documented how-to to enable all the eqep pins:
https://github.com/adafruit/adafruit-beaglebone-io-python/commit/c418cdae9a2a2c0d52412561c0125b0d227af4eb

BeagleBone must boot with cape-universal enabled and load the `cape-universala` overlay in order to
use all the eQEP pins:

### Install the latest Device Tree overlays:
```
sudo apt-get upgrade bb-cape-overlays
```

### File: /boot/uEnv.txt
```
uname_r=4.4.62-ti-r99
cmdline=coherent_pool=1M quiet cape_universal=enable
cape_enable=bone_capemgr.enable_partno=cape-universala
```

### File: /sys/devices/platform/bone_capemgr/slots
```
0: PF----  -1 
1: PF----  -1 
2: PF----  -1 
3: PF----  -1 
4: P-O-L-   0 Override Board Name,00A0,Override Manuf,cape-universala
```

### eqep0: P9_27, P9_92
```
config-pin P9_27 qep
config-pin P9_92 qep # alias for P9_42.1
cat /sys/devices/platform/ocp/48300000.epwmss/48300180.eqep/position
```

### eqep1: P8.33, P8.35
```
config-pin P8.33 qep 
config-pin P8.35 qep
cat /sys/devices/platform/ocp/48302000.epwmss/48302180.eqep/position
```

### eqep2: P8.11, P8.12
```
config-pin P8.11 qep 
config-pin P8.12 qep 
cat /sys/devices/platform/ocp/48304000.epwmss/48304180.eqep/position
```

### eqep2b: P8.41, P8.42
_alternate pins for eqep2 (mutually exclusive)_
```
config-pin P8.41 qep 
config-pin P8.42 qep 
cat /sys/devices/platform/ocp/48304000.epwmss/48304180.eqep/position
```

### TODO: implement in corresponding methods in `Encoder.py`
