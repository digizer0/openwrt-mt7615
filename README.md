# OpenWrt MT7615 closed source driver 5.0.2.0

MT7615 closed source driver for OpenWrt latest snapshot (post 19.07)

Tested on Netgear R6350 with 5G 11ac HT80 and HT160 working on 4.14 kernel.  
Since Netgear R6260, R6350 and R6850 are identical, all these models are expected to work with this driver.  
(MT7603 is used for 2.4G 11n and runs perfectly with open source mt76 driver.)

## How to use

```
cp -a mtk ${OPENWRT_PATH}/package
make menuconfig
```

During menuconfig, make sure
- the open source `kmod-mt7615e` driver is unselected under `Kernel modules|Wireless Drivers`
- closed source driver modules `kmod-mt_wifi` and `wifi-l1profile` are selected under `MTK Properties|Drivers`
- under `wifi-l1profile`, enable only 1st card and input the parameters for profile, driver, eeprom and SKU correctly. For R6350, use these values:
  - 1st card name: MT7615E
  - profile path: /etc/wireless/mt7615e/mt7615e.1.dat
  - compatible driver: mt_wifi
  - eeprom data offset: 0x8000
  - eeprom data size: 0x8000
  - single SKU data path: /etc/wireless/mt7615e/mt7615e-sku.dat
  - beam forming SKU data path: /etc/wireless/mt7615e/mt7615e-sku-bf.dat

The eeprom offset (relative to mtd factory partition) is essential to proper driver initialization. For other routers, check the dts files for hints.
