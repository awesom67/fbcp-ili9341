## kind of a guide for using 240x240 ST7789 SPI display on RPi zero
*Note:* If you get an error when you try to run the driver, try disabling the GL driver using `raspi-config`.
#### Wiring
```
GND -> Ground
VCC -> 3v3
SCL -> BCM 11
SDA -> BCM 10
RES -> BCM 25
DC  -> BCM 24
BLK -> BCM 27
```
#### Compiling
```
mkdir build && cd build && cmake -DST7789VW=ON -DGPIO_TFT_DATA_CONTROL=24 -DGPIO_TFT_RESET_PIN=25 -DGPIO_TFT_BACKLIGHT=27 -DSTATISTICS=0 -DSPI_BUS_CLOCK_DIVISOR=8 -DUSE_DMA_TRANSFERS=OFF .. && make -j
```
#### Configuring
Go to `/boot/config.txt` and add/change these:
```
hdmi_group=2
hdmi_mode=87
hdmi_cvt=240 240 60 1 0 0 0
hdmi_force_hotplug=1
```
#### Launching the driver at startup
To set up the driver to launch at startup, edit the file `/etc/rc.local` in sudo mode, and add a line:

```
sudo /path/to/fbcp-ili9341/build/fbcp-ili9341 &
```

to the end. Make note of the needed ampersand & at the end of that line.

For example, if you used the command line steps listed above to build, the file /etc/rc.local would receive a line

```
sudo /home/pi/fbcp-ili9341/build/fbcp-ili9341 &
```