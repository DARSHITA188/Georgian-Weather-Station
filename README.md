# Georgian-Weather-Station

For prototyping, the P1 header pins should be connected as follows:

Board Pin	Name	Remarks	RPi Pin	RPi Function
1	VIN	+3.3V Power	P01-1	3V3
2	GND	Ground	P01-6	GND
3	SCL	Clock	P01-5	GPIO 3 (SCL)
4	SDA	Data	P01-3	GPIO 2 (SDA)

Ensure that the I2C kernel driver is enabled:
or:
 
If you have no kernel modules listed and nothing is showing using dmesg then this implies the kernel I2C driver is not loaded. Enable the I2C as follows:
•	Run sudo raspi-config
•	Use the down arrow to select 9 Advanced Options
•	Arrow down to A7 I2C
•	Select yes when it asks you to enable I2C
•	Also select yes when it asks about automatically loading the kernel module
•	Use the right arrow to select the <Finish> button
•	Select yes when it asks to reboot
After rebooting re-check that the dmesg | grep i2c command shows whether I2C driver is loaded before pro- ceeding.

Optionally, to improve permformance, increase the I2C baudrate from the default of 100KHz to 400KHz by altering
/boot/config.txt to include:

# dtparam=i2c_arm=on,i2c_baudrate=400000

Then reboot.
Then add your user to the i2c group:

# $ sudo adduser pi i2c

Install some packages:

# $ sudo apt-get install i2c-tools python-pip
 
Next check that the device is communicating properly (if using a rev.1 board, use 0 for the bus not 1):

# $ i2cdetect	-y	1	
0	1	2	3	4	5	6	7	8	9	a	b	c	d	e	f
00:		--	--	--	--	--	--	--	--	--	--	--	--	--
10: -- --	--	--	--	--	--	--	--	--	--	--	--	--	--	--
20: -- --	--	--	--	--	--	--	--	--	--	--	--	--	--	--
30: -- --	--	--	--	--	--	--	--	--	--	--	--	--	--	--
40: -- --	--	--	--	--	--	--	--	--	--	--	--	--	--	--
50: -- --	--	--	--	--	--	--	--	--	--	--	--	--	--	--
60: -- --	--	--	--	--	--	--	--	--	--	--	--	--	--	--
70: -- --	--	--	--	--	76	--								
