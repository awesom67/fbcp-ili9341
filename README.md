## kind of a guide for using 240x240 ST7789 SPI display on RPi zero
###### Wiring
```
GND -> Ground
VCC -> 3v3
SCL -> BCM 11
SDA -> BCM 10
RES -> BCM 25
DC  -> BCM 24
BLK -> BCM 27
```

###### Compiling
```
cmake -DST7789VW=ON -DGPIO_TFT_DATA_CONTROL=24 -DGPIO_TFT_RESET_PIN=25 -DGPIO_TFT_BACKLIGHT=27 -DSTATISTICS=0 -DSPI_BUS_CLOCK_DIVISOR=8 -DUSE_DMA_TRANSFERS=OFF .. && make -j
```

###### Configuring
Go to `/boot/config.txt` and add/change these:
```
hdmi_group=2
hdmi_mode=87
hdmi_cvt=240 240 60 1 0 0 0
hdmi_force_hotplug=1
```